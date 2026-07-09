---
description: >-
  Atlas API Get Offer flow for real-time price checks, OfferId handling,
  recommended ancillary upsell, and downstream order creation.
---

# Get Offer

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when you need an independent offer lookup flow.

{% hint style="info" %}
Use OpenAPI naming as the source of truth.

Use `getOffers.do` in docs and integration.
{% endhint %}

Start here when you need to:

* price a known itinerary without the standard search flow
* fetch a fresh `OfferId` before order creation
* run baggage or seat lookup before booking

### FAQ

#### When should I use `getOffers.do`?

Use `getOffers.do` when you already know the target itinerary or need an independent price check before booking.

This flow is a good fit when shopping happens outside Atlas and Atlas is used as the booking and pricing layer.

Do not use this page as the source of truth for the fulfillment-specific `getOfferPrice.do` path.

Use [Get Offer Price](get-offer-price.md) when the flow needs broader display rules and a 5-minute ticketing window.

#### What should I keep from the Get Offer response?

Keep `OfferId`.

Use it as the key identifier for downstream order creation.

Use the same `OfferId` for `seatAvailability.do` when seat lookup is needed before booking.

#### What request limit applies to `getOffers.do`?

`getOffers.do` shares one `60 QPM` fulfillment pool with `verify.do`.

Over-limit requests return Atlas error code `429`.

Honor the returned `retryAfter` value before retrying.

### Fulfillment request limits

Atlas counts `getOffers.do` and `verify.do` together in a rolling 60-second window.

The default shared limit is `60 QPM`.

One busy API can consume the shared pool for the other.

#### What counts

These requests count:

* successful responses
* no-result responses
* business failures, airline failures, and cache-hit responses

#### How to reduce limit pressure

Reuse fresh offer data when the booking context did not change.

Avoid repeated price checks for the same itinerary in a short window.

Honor `retryAfter` when `429` is returned.

### Main API

* `getOffers.do`

### Inputs

* Accurate itinerary details
* Passenger mix when required by the request
* Any fields required by the current API reference

### Key outputs

* Latest bookable fare
* Inventory status
* `OfferId` for downstream order creation
* `OfferId` for `seatAvailability.do` in the Get Offer path

### What comes next?

#### Minimal path

Continue with [Create Order](create-order.md), then [Payment & Ticketing](payment-and-ticketing/).

#### Path with seats and baggage

Use [Seats](../optional-ancillaries/seats-and-baggage/) and [Baggage](../optional-ancillaries/baggage.md) before order creation.

### How this differs from standard search

#### Standard search flow

Use `search.do` when Atlas is your primary shopping entry point.

That flow is best when you want Atlas to return available offers first.

#### Get Offer flow

Use `getOffers.do` when you already know the target itinerary.

This flow is better for direct price checks, independent validation, and external shopping paths.

#### Practical difference

The standard search flow usually continues through `verify.do`.

The Get Offer flow is designed around the returned `OfferId` for downstream order creation.

### Use this when you need

* An offer lookup flow without standard search
* A secondary price check before order creation
* Lowest-price validation before ticketing
* A flow driven by your own flight data source

### Common scenarios

#### Use your own flight data source

Use `getOffers.do` when flight selection happens outside the standard Atlas search flow.

This lets you fetch the latest bookable fare and `OfferId` directly.

#### Run a final price check before order creation

Use `getOffers.do` to re-check the latest bookable price before you create the order.

This helps reduce fare drift between quote and booking.

#### Compare channels before ticketing

Use `getOffers.do` when you need a real-time validation point before sending the order into ticketing.

This is useful when you optimize for the latest available price before completion.

### Recommended business chain

#### Minimal chain

Use this path when you only need fare retrieval and ticketing:

1. Call `getOffers.do`
2. Keep the returned `OfferId`
3. Call `order.do`
4. Call `pay.do`

#### Chain with seats and baggage

Use this path when baggage and seat upsell are part of the booking flow:

1. Call `getOffers.do`
2. Confirm the fare and target flight
3. Query `getLuggage.do` or `seatAvailability.do` if needed
4. Create the order with `order.do`
5. Complete payment with `pay.do`

#### When to stop and re-check

Stop and refresh the offer if any of these change:

* target flight
* passenger mix
* expected fare
* ancillary requirement that changes the booking plan

### Best practice

Refresh the offer when booking-critical input changed or when booking was delayed.

Do not build the order from stale offer assumptions.

### Typical flow

{% stepper %}
{% step %}
### Get Offer

Call `getOffers.do` with the target itinerary.

Keep the returned `OfferId`.
{% endstep %}

{% step %}
### Seats and baggage

Query `getLuggage.do` or `seatAvailability.do`.

Run this after the offer matches your target flight and price.

For seat lookup, pass the returned `OfferId`.
{% endstep %}

{% step %}
### Create Order

Call `order.do` with the returned `OfferId` and required booking data.
{% endstep %}

{% step %}
### Pay and ticket

Call `pay.do` to complete ticketing.
{% endstep %}
{% endstepper %}

### When to use ancillary queries

#### Use `getLuggage.do`

Use it to surface baggage price and baggage options before booking.

Run it after you confirm the target offer.

#### Use `seatAvailability.do`

Use it to surface seat availability and paid seat selection before booking.

Use the returned `OfferId` as the request context in this flow.

Do not call it with flight data alone.

#### Treat ancillaries as recommended

Include ancillary queries when your booking product supports seat and baggage upsell.

The shortest technical path is still `getOffers.do` → `order.do` → `pay.do`.

### Implementation guidance

#### Best fit

This flow fits partners who already control shopping logic.

It also fits flows where a final Atlas-side price check is needed before booking.

#### Data to retain

Retain the exact itinerary context used for `getOffers.do`.

Retain the returned `OfferId` until order creation is completed.

#### Suggested validation

Before `order.do`, confirm:

* flight matches the intended itinerary
* fare matches the expected sell logic
* passenger mix is still correct
* ancillary selection is complete when required

### Operational notes

#### Source of truth

Use the OpenAPI schema as the source of truth for request fields and response fields.

#### Naming

Use `getOffers.do` in implementation material, support replies, and customer-facing guidance.

#### Error handling

If the order or payment step fails because fare or availability changed, restart from a fresh offer lookup.

Use the latest returned data instead of retrying with stale assumptions.

### FAQ

#### Does `getOffers.do` replace `search.do`?

No.

Use `search.do` when Atlas is the main shopping entry point.

Use `getOffers.do` when you already know the target itinerary or need an independent price check.

#### Do I still need `verify.do` in this flow?

Not in the standard Get Offer path described on this page.

This flow is centered on `OfferId` and downstream order creation.

#### Is ancillary lookup mandatory?

Seat and baggage lookup is strongly recommended when your product includes ancillary upsell.

Use `getLuggage.do` or `seatAvailability.do` before `order.do` to improve conversion and traveler clarity.

#### When should I refresh the offer?

Refresh the offer when any booking-critical input changes.

Typical triggers:

* passenger count changes
* target flight changes
* expected fare changes
* booking is delayed and current pricing may be stale

#### Can I use Get Offer with my own shopping engine?

Yes.

This is one of the main use cases for this flow.

Keep your itinerary mapping consistent with the request fields defined in OpenAPI.

### Failure handling

#### If `getOffers.do` fails

Check request completeness first.

Then confirm itinerary data, passenger data, and any required fields defined in OpenAPI.

If the issue is transient, retry with controlled backoff.

#### If `order.do` fails after Get Offer

Do not assume the returned offer is still valid.

If the failure points to fare, inventory, or booking-state drift, call `getOffers.do` again and rebuild the order request from fresh data.

#### If `pay.do` fails

Check whether the order was already paid or is still processing.

Do not send duplicate payment blindly.

Query order state when needed before retrying.

#### When not to retry immediately

Avoid instant retries when the issue may be caused by:

* stale fare data
* unsupported payment method
* invalid passenger or contact data
* airline-side restrictions

Fix the root cause first.

### Logging and support guidance

#### Keep these values in logs

Capture the minimum fields needed for troubleshooting:

* request timestamp
* itinerary summary
* passenger mix
* `OfferId`
* `orderNo` after order creation
* payment method type
* final response status and message

#### Keep request linkage clear

Log the Get Offer request and the downstream order request as one business chain.

This makes fare drift and state mismatch easier to trace.

#### Escalation readiness

When escalating, provide:

* API name
* request time
* key identifier such as `OfferId` or `orderNo`
* response code
* response message

This speeds up support review.

### Notes

* This flow does not start from the standard `search.do` path.
* Use the current API reference as the source of truth for required fields.
* Use OpenAPI naming as the source of truth for interface names.
* Use `getOffers.do` as the official interface name in implementation material.

### Related pages

* [Search](search.md)
* [Get Offer Price](get-offer-price.md)
* [Get Offer vs Get Offer Price](../booking-overview/booking-decisions/get-offer-vs-get-offer-price.md)
* [Create Order](create-order.md)
* [Payment & Ticketing](payment-and-ticketing/)
* [Seats](../optional-ancillaries/seats-and-baggage/)
* [Baggage](../optional-ancillaries/baggage.md)

### Full API reference

See endpoint-level details here:

* [Get Offer](../../../api-reference/booking-apis/get-offer.md)
* [Seat](../../../api-reference/booking-apis/inflow-seat-and-baggage.md)
* [Baggage](../../../api-reference/booking-apis/baggage.md)
* [Create Order](../../../api-reference/booking-apis/create-order.md)
* [Payment & Ticketing](../../../api-reference/booking-apis/payment-and-ticketing.md)
