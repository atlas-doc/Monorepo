---
description: >-
  Ryanair-specific booking flow with order confirmation, price transparency, and
  child seating rules.
---

# FR Integration

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when you integrate Ryanair booking flows.

### When to use this flow

Use the FR flow when:

* the airline is FR
* order confirmation is required before final payment
* you need popup or iframe confirmation
* Ryanair-specific display and child seating rules apply

### How FR differs from the standard flow

Compared with the normal booking flow, FR adds extra requirements:

* price transparency for fare and ancillary charges
* explicit passenger consent on the FR confirmation page
* a mandatory `orderCommit.do` step before payment
* special handling for child seating scenarios
* FR-specific UAT and IP allowlisting

### FR workflow diagram

```mermaid
sequenceDiagram
    actor User as End user
    participant OTA as Subscriber
    participant Atlas
    participant FRAPI as RYR_API
    participant FRUI as RYR_POPUP

    User->>OTA: Search
    OTA->>Atlas: search.do
    Atlas->>FRAPI: GET /availability
    FRAPI-->>Atlas: Fares for selected route and date
    Atlas-->>OTA: Search.do RS
    OTA-->>User: Search result

    User->>OTA: Verify
    OTA->>Atlas: verify.do
    Atlas->>FRAPI: /flight
    FRAPI-->>Atlas: 200 OK
    Atlas-->>OTA: Verify.do RS
    OTA-->>User: Verify result

    opt Optional seat selection
        User->>OTA: Select seat
        OTA->>Atlas: seatAvailability.do
        Atlas->>FRAPI: Seat availability
        FRAPI-->>Atlas: Available seats and seat map
        Atlas-->>OTA: Seats and seat map
        OTA-->>User: Available seats and seat map
    end

    User->>OTA: Book
    OTA->>Atlas: order.do
    Atlas->>FRAPI: /booking
    FRAPI-->>Atlas: Order number
    Atlas-->>OTA: Order.do RS
    OTA-->>User: Order number

    User->>OTA: Pay on OTA
    OTA->>Atlas: orderCommit.do
    Atlas->>FRAPI: Book commit
    FRAPI-->>Atlas: confirmationUrl
    Atlas-->>OTA: confirmationUrl
    OTA->>FRUI: Open popup or iframe

    User->>FRUI: Confirm flights
    FRUI-->>OTA: Redirect after confirmation

    alt Order confirmed
        OTA->>Atlas: pay.do
        Atlas->>FRAPI: POST /encrypt + POST /payment
        FRAPI-->>Atlas: 200 OK
        Atlas-->>OTA: Success
    else Order not confirmed
        OTA->>Atlas: pay.do
        Atlas->>FRAPI: POST /encrypt + POST /payment
        FRAPI-->>Atlas: Failure (order unconfirmed)
        Atlas->>Atlas: Cancel order
        Atlas-->>OTA: Failure
    end
```

This flow adds an FR confirmation page between `order.do` and `pay.do`.

### FR booking flow

{% stepper %}
{% step %}
### Search

Call [Search](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/9K7uEnLGfEbpjGjni5gD) and keep the selected `routingIdentifier`.
{% endstep %}

{% step %}
### Verify

Call [Verify](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm) and keep the returned `sessionId`.
{% endstep %}

{% step %}
### Optional seat selection

If you support FR seat selection, call [Seats](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/3ujCySdZ8OYYLfGI3iF3) before booking.

Skip this step if you use the FR child-seat simplification.
{% endstep %}

{% step %}
### Create the order

Call [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE) with passenger, contact, and required FR fields.

Make sure the order request includes:

* passenger email
* subscriber email
* subscriber company name in `clientContact`
* `locale`
{% endstep %}

{% step %}
### Collect payment and commit the order

At this stage, the OTA collects payment from the user.\
Do **not** call `pay.do` yet.

Then call [Confirm Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/cyd69uDJk3ulct18V6QB).

Atlas returns `confirmationUrl` for popup mode or iframe mode.
{% endstep %}

{% step %}
### User confirms on the FR page

Display `confirmationUrl` to the user.

The FR confirmation page contains the required T\&Cs and consent checkbox. The user must complete this step before ticketing.
{% endstep %}

{% step %}
### Pay and issue

Only after the user completes confirmation, call [Payment & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB).

Payment can use `VCC` or `Deposit`.
{% endstep %}

{% step %}
### Poll final status

Use [Query Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n) until `orderStatus=2` and `ticketStatus=0`.
{% endstep %}
{% endstepper %}

### Confirm Order modes

#### Popup mode

Send the order number and a `redirectUri`.\
Atlas returns `confirmationUrl`.\
Redirect the end user to that page.

Prepare a redirect page URL and share it with Atlas.\
This page should accept `AtlasOrderNumber` as an input parameter.

After the user confirms, FR redirects the user back to your `redirectUri`.

#### Iframe mode

Send the order number with `iframe=true`.\
Atlas returns `confirmationUrl`.\
Display that page inside your iframe flow.

In iframe mode, `redirectUri` is ignored.

### Payment timing rule

Do not call `pay.do` before order confirmation finishes.

If the user does not confirm within 30 minutes after order creation:

* the order status becomes `Expired`
* Atlas will not issue tickets
* the OTA should refund the end user if payment was already collected

If `pay.do` is attempted before the user completes FR confirmation, airline payment can fail and the order can be canceled.

### Required FR business rules

#### Price transparency

Display airline fare separately from:

* airline payment fees
* Atlas service fees
* subscriber markup
* ancillary charges

Read payment-fee data from `cardChargeList` in search and verify responses.

Make sure the user can clearly identify Ryanair's actual price.

#### Passenger consent

The FR confirmation page must collect user consent for:

* terms of service
* privacy policy
* cookie policy
* myRyanair account acknowledgement

#### Contact details

Pass both:

* the passenger email
* the subscriber email and company name in `clientContact`
* the required booking `locale`

This helps ensure both sides receive airline communication.

For supported locale values, see [Locale Reference](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Iqbnh1NWCgycDIzPka7l).

### Child seating rule

FR applies special rules when children under 12 are included.

#### Important behavior

* up to 4 children per adult
* at least one adult may need a paid seat
* children must sit in the same row as the accompanying adult
* seat selection may become mandatory before payment

#### Atlas simplification option

If you are not ready to support full seat selection logic for FR with children:

1. disable seat selection
2. charge the mandatory seating fee
3. let Atlas auto-allocate seats for the first adult and the children

Use `childMandatorySeatingFee` from search and verify responses.

Also ensure that one booking never contains more than 4 children.

{% hint style="warning" %}
If your FR child-seat handling is not ready, block FR child bookings until support is complete.
{% endhint %}

### UI guidance

Recommended maximum width:

* popup: `1028px`
* iframe: `1028px`

Suggested desktop/mobile breakpoint:

* `768px`

### UAT requirements

#### IP allowlisting

Provide a static IP address for Ryanair allowlisting before live FR booking tests.

#### FR sandbox VCC test cards

| Card number      | Type                 |
| ---------------- | -------------------- |
| 5200000000002235 | Mastercard, approved |
| 4000000000002701 | Visa, approved       |
| 5476850000000002 | Declined card        |
| 5100000014101198 | Declined card        |

Use declined cards to validate payment-failure handling.

{% hint style="danger" %}
Do not use real cards in test environments.
{% endhint %}

#### FR test routes

* `DUB-KIR`
* `KIR-DUB`
* `DUB-LON`
* `LON-DUB`
* `MAN-DUB`
* `DUB-MAN`

#### UAT scenarios

Use the FR-specific UAT file below.

{% file src="../../../.gitbook/assets/Ryan Air (FR) Atlas UAT Test Shopping & Ticketing Services Only Template.xlsx" %}

### Related pages

* [Confirm Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/cyd69uDJk3ulct18V6QB)
* [Payment & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB)
* [UAT Submission Guide](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/aH2Shbpf2B9zZldFkBrT)
* [Special Integrations](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/rJmf4QqhDHnkZLTdu1Io)
