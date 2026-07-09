---
description: >-
  Atlas API booking flow overview for search, getOffers, verify, order creation,
  payment, ticketing, identifiers, and order follow-up.
---

# Booking Overview

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this section to choose the correct Atlas API booking flow and keep the right identifier at each step.

<figure><img src="../../../.gitbook/assets/FlowChart_2_IssueTicket.png" alt=""><figcaption><p>Booking flow from search to payment and follow-up</p></figcaption></figure>

Start here when you need to:

* understand the standard Atlas API booking flow
* choose between `search.do` and `getOffers.do`
* see which identifier to keep at each step
* evaluate route coverage and raw prices in pre-sale

### FAQ

#### Which identifier should I keep after each step?

Keep `routingIdentifier` after `search.do`.

Keep `sessionId` after `verify.do`.

Keep `orderNo` after `order.do`.

Keep airline PNR and `ticketNos` after ticketing.

For the Get Offer flow, keep `OfferId` from `getOffers.do`.

#### How long are `routingIdentifier` and `sessionId` valid?

`routingIdentifier` is valid for up to 6 hours after `search.do`.

`sessionId` is valid for up to 2 hours after `verify.do`.

Shorter is safer in both cases because fare and inventory can change earlier.

#### What is the standard Atlas API booking flow?

The standard flow is `search.do` → `verify.do` → `order.do` → `pay.do` → `queryOrderDetails.do`.

`Post-payment polling` is not a separate API step.

It explains how to keep using `queryOrderDetails.do` until ticketing reaches a final state.

If the airline is FR, add `orderCommit.do` before payment.

#### When should I use `getOffers.do` instead of `search.do`?

Use `search.do` when Atlas is your main shopping entry point.

Use `getOffers.do` when you already know the target itinerary or need an independent price check.

Use `getOfferPrice.do` when you need the fulfillment path with broader display rules and a strict 5-minute ticketing window.

#### When should I use `priceCompareSearch.do`?

Use `priceCompareSearch.do` for pre-sale route coverage checks and raw price discovery.

It is not part of the standard booking flow.

Do not treat it as a production booking price source.

#### Which flow should I choose first?

Use `search.do` when Atlas is your main shopping and booking layer.

Use `getOffers.do` when the target itinerary is already known or when you need an independent price check.

Use `priceCompareSearch.do` for pre-sale route coverage checks and raw price discovery only.

### API request limits

Atlas applies request-limit governance to selected pre-booking APIs.

Over-limit requests return Atlas error code `429`.

#### Default limits

* `search.do` uses `10 QPS`
* `verify.do` and `getOffers.do` share `60 QPM`
* `getOfferPrice.do` uses its own fulfillment QPM policy
* `seatAvailability.do` and `getLuggage.do` share `60 QPM`

#### APIs not covered by this policy

`order.do` and `pay.do` are not part of this QPS and QPM policy.

#### What counts toward the limit

These requests count:

* successful requests
* no-result requests
* business failures and airline failures
* cache-hit responses

These requests do not count:

* requests already rejected by QPS or QPM
* authentication, permission, or validation failures
* idempotency-blocked duplicates that never enter business processing

#### What to do on `429`

Reduce request frequency.

Wait for the returned `retryAfter` value before retrying.

Avoid immediate retry loops.

Use [API Request Limits](api-request-limits.md) for the full policy.

### Key booking pages

* [Identifiers](identifiers.md)
* [Search](../booking-step-guides/search.md)
* [Price Compare Search](../../../api-reference/booking-apis/price-compare-search.md)
* [Get Offer](../booking-step-guides/get-offer.md)
* [Get Offer Price](../booking-step-guides/get-offer-price.md)
* [Verify](../booking-step-guides/verify.md)
* [Create Order](../booking-step-guides/create-order.md)
* [Confirm Order](../booking-step-guides/confirm-order.md)
* [Payment & Ticketing](../booking-step-guides/payment-and-ticketing/)
* [Query Order](../booking-step-guides/query-order/)
* [Optional ancillaries](../optional-ancillaries/)
* [Booking decisions](booking-decisions/)

### Key identifiers in the booking flow

Keep and reuse the right identifier at each stage:

* `routingIdentifier` from `search.do`
* `sessionId` from `verify.do`
* `orderNo` from `order.do`
* airline PNR and `ticketNos` from `queryOrderDetails.do` after ticketing

For the Get Offer path, keep `OfferId` from `getOffers.do`.

For seat and baggage queries, keep `sessionId` from `verify.do` or `OfferId` from `getOffers.do` or `getOfferPrice.do`.

### What this section covers

* Search for flight offers
* Retrieve offers through an independent Get Offer flow
* Verify fares and routing
* Create orders
* Confirm FR orders when required
* Pay and issue tickets
* Retrieve booking details
* Run advanced search flows
* Query seats
* Query baggage

### Which flow should you choose?

#### Standard search flow

Use this when Atlas is your main shopping and booking layer.

This path uses `search.do` first, then `verify.do` before booking.

#### Get Offer flow

Use this when the itinerary is already known or when you need an independent price check before order creation.

This path starts with `getOffers.do` and uses `OfferId`.

#### Fulfillment flow

Use this when you need broader offer visibility and your system can execute payment immediately.

This path starts with `getOfferPrice.do` and applies a 5-minute payment and ticketing window after order creation.

#### Price compare search

Use this when you need pre-sale coverage visibility and raw price signals.

This path uses `priceCompareSearch.do`.

It does not replace the standard booking flow.

### Flow summaries

#### Standard booking flow

Use `search.do` → `verify.do` → `order.do` → `pay.do` → `queryOrderDetails.do`.

Insert ancillaries before order only when needed.

Insert `orderCommit.do` before payment for FR only.

Use [Standard booking flow](../booking-flows/standard-booking-flow.md) for the full step-by-step sequence.

#### How to include seats and baggage

Treat seats and baggage as optional add-ons in the booking flow.

Use `getLuggage.do` and `seatAvailability.do` only when ancillary upsell is part of the product and the flow supports it.

Use them before payment to improve traveler clarity and order conversion.

Call `seatAvailability.do` only with a valid `sessionId` or `OfferId`.

Do not call it from flight data alone.

#### Get Offer flow

Use `getOffers.do` → `order.do` → `pay.do` → `queryOrderDetails.do`.

Insert ancillaries before order only when needed.

Insert `orderCommit.do` before payment for FR only.

Use [Get Offer flow](../booking-flows/get-offer-flow.md) for the full step-by-step sequence.

#### Fulfillment flow

Use `getOfferPrice.do` → `order.do` → `pay.do` → `queryOrderDetails.do`.

Insert ancillaries before order only when needed.

Treat the 5-minute payment and ticketing window as strict.

Use [Fulfillment flow](../booking-flows/fulfillment-flow.md) for the full step-by-step sequence.

#### What happens after `pay.do`?

Do not assume payment and final ticketing happen at the same moment.

Use `queryOrderDetails.do` until the order reaches the final ticketed state.

Webhook can help, but it should not be your only confirmation path.

### Main APIs

* `search.do`
* `priceCompareSearch.do`
* `getOffers.do`
* `getOfferPrice.do`
* `verify.do`
* `order.do`
* `orderCommit.do`
* `pay.do`
* `queryOrderDetails.do`
* `smartSearch.do`
* `seatAvailability.do`
* `getLuggage.do`

### Recommended next pages by task

#### Choose the right booking path

Use:

* [Booking decisions](booking-decisions/)
* [Search vs Offer](booking-decisions/search-vs-offer.md)
* [Get Offer vs Get Offer Price](booking-decisions/get-offer-vs-get-offer-price.md)

#### Build the standard flow

Use:

* [Identifiers](identifiers.md)
* [Standard booking flow](../booking-flows/standard-booking-flow.md)
* [Search](../booking-step-guides/search.md)
* [Verify](../booking-step-guides/verify.md)
* [Create Order](../booking-step-guides/create-order.md)

#### Build payment and follow-up

Use:

* [Payment & Ticketing](../booking-step-guides/payment-and-ticketing/)
* [Post-payment polling](../booking-step-guides/query-order/post-payment-polling.md)
* [Query Order](../booking-step-guides/query-order/)

#### Add seats and baggage

Use:

* [Optional ancillaries](../optional-ancillaries/)
* [Seats](../optional-ancillaries/seats-and-baggage/)
* [Baggage](../optional-ancillaries/baggage.md)
* [Baggage and seat productCode freshness](../optional-ancillaries/baggage-and-seat-productcode-freshness.md)

Treat ancillaries here as optional add-ons, not as mandatory booking steps.

#### Build the alternate offer path

Use:

* [Booking decisions](booking-decisions/)
* [Get Offer flow](../booking-flows/get-offer-flow.md)
* [Get Offer](../booking-step-guides/get-offer.md)
* [Optional ancillaries](../optional-ancillaries/)

#### Build the fulfillment path

Use:

* [Fulfillment flow](../booking-flows/fulfillment-flow.md)
* [Get Offer Price](../booking-step-guides/get-offer-price.md)
* [Get Offer vs Get Offer Price](booking-decisions/get-offer-vs-get-offer-price.md)
* [Optional ancillaries](../optional-ancillaries/)
* [Payment & Ticketing](../booking-step-guides/payment-and-ticketing/)
* [API Request Limits](api-request-limits.md)

#### Evaluate pre-sale route coverage

Use:

* [Price Compare Search](../../../api-reference/booking-apis/price-compare-search.md)
* [Search](../booking-step-guides/search.md)

### Use this when you need

* A standard search-to-ticket flow
* An independent offer lookup and price-check flow
* A pre-sale route coverage and raw-price check
* FR order confirmation support when applicable
* Seat and baggage upsell
* Real-time or smart search options

### Full API reference

Use endpoint-level details here:

[Booking APIs](../../../api-reference/booking-apis/)

### Related pages

* [Quick Start](../../../readme-1/quick-start.md)
* [Get Sandbox Credentials](../../../readme-1/making-requests.md)
* [Identifiers](identifiers.md)
* [Optional ancillaries](../optional-ancillaries/)
* [Booking decisions](booking-decisions/)
* [Error Codes](../../../support-and-reference/troubleshooting-and-support/errors-handing/)
