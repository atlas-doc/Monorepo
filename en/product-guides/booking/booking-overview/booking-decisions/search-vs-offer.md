---
description: >-
  Choose the Atlas API booking entry flow between search-based and offer-based
  booking paths.
---

# Search vs Offer

{% include "../../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when you need to choose between `search.do` and `getOffers.do`.

### Short answer

Use `search.do` when Atlas is your main shopping entry point.

Use `getOffers.do` when the target itinerary is already known or when you need an independent price check.

### FAQ

#### When should I use `search.do`?

Use `search.do` when you want Atlas to return available offers first.

This is the standard Atlas booking flow.

#### When should I use `getOffers.do`?

Use `getOffers.do` when shopping happens outside Atlas or when you already know the target itinerary.

This is also the right path for a final independent price check.

#### Which identifier does each flow return?

`search.do` returns `routingIdentifier`.

`getOffers.do` returns `OfferId`.

#### Does `getOffers.do` still need `verify.do`?

Not in the standard Get Offer flow on this site.

That flow is centered on `OfferId` and then continues to `order.do`.

### Core difference

#### `search.do`

Use it for offer discovery.

Atlas returns available options for the route and date.

Then the standard path continues to `verify.do`.

#### `getOffers.do`

Use it for targeted price retrieval.

Atlas returns the current offer context for a known itinerary.

Then the flow continues with `OfferId`.

### Which flow should you choose?

#### Choose `search.do` when

* Atlas is your main shopping layer
* users need a list of available offers
* you want the standard search → verify → order path

#### Choose `getOffers.do` when

* your own system already selected the flight
* you need an independent price check before order creation
* you want Atlas as the pricing and booking layer, not the shopping layer

### What comes next?

#### After `search.do`

1. Keep `routingIdentifier`
2. Call `verify.do`
3. Keep `sessionId`
4. Call `order.do`

#### After `getOffers.do`

1. Keep `OfferId`
2. Optionally query seats or baggage
3. Call `order.do`

### How seats and baggage differ

#### Standard search flow

Use `sessionId` from `verify.do` for `seatAvailability.do`.

#### Get Offer flow

Use `OfferId` from `getOffers.do` for `seatAvailability.do`.

In both flows, query baggage only after the target itinerary is confirmed.

### Timing and refresh rules

#### Search flow

`routingIdentifier` is valid for up to 6 hours.

`sessionId` is valid for up to 2 hours.

#### Get Offer flow

Refresh the offer when the itinerary, passenger mix, expected fare, or booking timing changed.

Do not build orders from stale offer assumptions.

### Common mistakes

#### Mixing identifiers across flows

Do not use `OfferId` as if it were `routingIdentifier`.

Do not use `routingIdentifier` as if it were `OfferId`.

#### Skipping the right next step

Do not call `order.do` from the standard search flow before `verify.do`.

Do not add `verify.do` to the standard Get Offer path unless your implementation specifically requires it.

### Recommended page by use case

#### Need standard shopping and booking

Use [Search](../../booking-step-guides/search.md).

#### Need independent price retrieval

Use [Get Offer](../../booking-step-guides/get-offer.md).

#### Need the full booking sequence

Use [Booking Overview](../).

### Related pages

* [Booking Overview](../)
* [Identifiers](../identifiers.md)
* [Search](../../booking-step-guides/search.md)
* [Get Offer](../../booking-step-guides/get-offer.md)
* [Verify](../../booking-step-guides/verify.md)
* [Create Order](../../booking-step-guides/create-order.md)
