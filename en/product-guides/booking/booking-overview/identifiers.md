---
description: >-
  Atlas API booking-flow identifiers, including routingIdentifier, sessionId,
  OfferId, orderNo, and retryAfter.
---

# Identifiers

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when you need to keep the right Atlas API identifier at the right stage.

Start here when you need to:

* know which identifier each API returns
* know how long each identifier stays valid
* know which downstream API uses it next
* avoid retrying with stale identifiers

### FAQ

#### Which identifier should I keep after `search.do`?

Keep `routingIdentifier`.

Use it for `verify.do` in the standard search flow.

#### Which identifier should I keep after `verify.do`?

Keep `sessionId`.

Use it for `order.do` and for `seatAvailability.do` in the standard booking flow.

#### Which identifier should I keep after `getOffers.do`?

Keep `OfferId`.

Use it for `order.do` in the Get Offer flow.

Use the same `OfferId` for `seatAvailability.do` in that flow.

#### Which identifier should I keep after `getOfferPrice.do`?

Keep `OfferId`.

Use it for `order.do` in the fulfillment flow.

Use the same `OfferId` for ancillary lookup in that flow.

After `order.do`, keep `orderNo` as the main operational identifier.

Use `orderNo` for payment, order query, and ticketing follow-up.

#### How long is each identifier valid?

`routingIdentifier` is valid for up to 6 hours after `search.do`.

`sessionId` is valid for up to 2 hours after `verify.do`.

`OfferId` should be treated as short-lived booking context.

Refresh it when booking-critical input changed or booking was delayed.

The `OfferId` from `getOfferPrice.do` is also short-lived.

Use it immediately because the fulfillment flow is built for fast payment and ticketing.

### Main identifiers

#### `routingIdentifier`

**What it is**

The route token returned by `search.do`.

**Use it for**

Use it for `verify.do`.

**Validity**

Up to 6 hours after search.

**Do not use it for**

Do not use it for `order.do`.

**Typical failure**

`202` usually means the `routingIdentifier` expired.

#### `sessionId`

**What it is**

The verification context returned by `verify.do`.

**Use it for**

Use it for `order.do` in the standard flow.

Use it for `seatAvailability.do` in the standard flow.

**Validity**

Up to 2 hours after verify.

**Do not use it for**

Do not reuse it after timeout.

Do not use it across unrelated bookings.

**Typical failure**

`301` usually means the `sessionId` expired.

#### `OfferId`

**What it is**

The offer token returned by `getOffers.do`.

**Use it for**

Use it for `order.do` in the Get Offer flow.

Use it for `seatAvailability.do` in the Get Offer flow.

**Validity**

Treat it as short-lived and refresh it when the booking context changed.

**Do not use it for**

Do not assume it stays valid after long delays or itinerary changes.

**Typical failure**

If order creation fails because fare or inventory changed, refresh the offer and rebuild from the latest `OfferId`.

#### `OfferId` from `getOfferPrice.do`

**What it is**

The short-lived offer context returned by `getOfferPrice.do`.

**Use it for**

Use it for `order.do` in the fulfillment flow.

Use it for ancillary lookup before `order.do` when needed.

Then switch to `orderNo` for payment and follow-up.

**Validity**

Treat it as immediate-use context.

Do not hold it for delayed booking decisions.

**Do not use it for**

Do not treat it as a long-lived shopping identifier.

Do not reuse it after the fulfillment window has already shifted.

#### `orderNo`

**What it is**

The Atlas order identifier returned after order creation.

**Use it for**

Use it for `pay.do`, order lookup, payment follow-up, and post-booking flows.

**Validity**

Keep it for the full order lifecycle.

**Do not use it for**

Do not use it as a substitute for search or verify identifiers.

#### `retryAfter`

**What it is**

The wait time returned with `HTTP 429 Too Many Requests`.

**Use it for**

Use it to decide how long to wait before retrying.

**Validity**

It applies to the current rate-limit event.

**Do not use it for**

Do not ignore it and retry immediately.

### Which identifier comes next?

#### Standard search flow

1. `search.do` returns `routingIdentifier`
2. `verify.do` returns `sessionId`
3. `order.do` returns `orderNo`
4. `queryOrderDetails.do` returns airline PNR and ticket data

#### Get Offer flow

1. `getOffers.do` returns `OfferId`
2. `order.do` returns `orderNo`
3. `queryOrderDetails.do` returns airline PNR and ticket data

#### Fulfillment flow

1. `getOfferPrice.do` returns `OfferId`
2. `order.do` returns `orderNo`
3. `pay.do` uses `orderNo`
4. `queryOrderDetails.do` returns airline PNR and ticket data

### Fresh-identifier rules

Start earlier in the flow when these conditions apply:

* `202` — run `search.do` again and get a fresh `routingIdentifier`
* `301` — run `verify.do` again and get a fresh `sessionId`
* `308` or inventory drift after Get Offer — run `getOffers.do` again and get a fresh `OfferId`

### Best practice

Store the returned identifier together with:

* request time
* itinerary summary
* passenger mix
* current flow type
* fulfillment-flow marker when your integration tracks one

This makes expiry and retry decisions easier.

### Related pages

* [Booking Overview](./)
* [Search](../booking-step-guides/search.md)
* [Get Offer](../booking-step-guides/get-offer.md)
* [Fulfillment API](../booking-step-guides/get-offer-price.md)
* [Get Offer vs Fulfillment API](booking-decisions/get-offer-vs-get-offer-price.md)
* [Verify](../booking-step-guides/verify.md)
* [Create Order](../booking-step-guides/create-order.md)
* [Get Offer Price](../../../api-reference/booking-apis/get-offer-price.md)
* [Error Codes](../../../support-and-reference/troubleshooting-and-support/errors-handing/)
