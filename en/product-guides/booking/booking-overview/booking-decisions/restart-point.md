---
description: Choose where to restart the flow.
---

# Restart point

{% include "../../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when a booking flow broke and you need to know the earliest step that must be rerun.

### Short answer

Restart from `search.do` when search-stage context is gone.

Restart from `verify.do` when search is still usable but booking validation must be refreshed.

Restart from `getOffers.do` when you are in the Get Offer flow and the offer context is stale.

### FAQ

#### When should I restart from `search.do`?

Restart from `search.do` when `routingIdentifier` expired or when inventory changed before verify or order creation.

#### When should I restart from `verify.do`?

Restart from `verify.do` when the `sessionId` expired or when the booking was delayed and you need a fresh booking context.

#### When should I restart from `getOffers.do`?

Restart from `getOffers.do` when you are using the Get Offer flow and the current `OfferId` or price context is stale.

### Decision by flow

#### Standard search flow

Use this path:

1. `search.do`
2. `verify.do`
3. `order.do`
4. `pay.do`

Restart from the earliest broken step.

#### Get Offer flow

Use this path:

1. `getOffers.do`
2. `order.do`
3. `pay.do`

Restart from the offer step when the offer context is stale.

### Restart from `search.do` when

These cases usually require a new search:

* `202`
* `206`
* `207`
* `210`
* `302`
* search-stage itinerary or inventory changed

Use a new `routingIdentifier` before moving forward.

### Restart from `verify.do` when

These cases usually require a new verify:

* `301`
* delayed booking with still-usable search context
* need a fresh `sessionId`
* need the latest `bookingRequirement`
* need the latest ancillary context before order creation

Use the refreshed `sessionId` for `order.do`.

### Restart from `getOffers.do` when

These cases usually require a new offer lookup:

* Get Offer path price drift
* stale `OfferId`
* delayed booking in the Get Offer flow
* ancillary context tied to an old offer

Use the refreshed `OfferId` for `order.do` and `seatAvailability.do` in that flow.

### `308` and price drift handling

`308` means the old booking price context is no longer safe.

In the standard search flow, restart from `search.do`.

In the Get Offer flow, restart from `getOffers.do`.

### Ancillary refresh rule

If you restart from `verify.do` or `getOffers.do`, refresh baggage and seat selection too.

Do not carry old ancillary `productCode` values into the new booking context.

### Quick decision rule

Use this rule in production:

* expired `routingIdentifier` — restart from `search.do`
* expired `sessionId` — restart from `verify.do`
* stale `OfferId` in Get Offer flow — restart from `getOffers.do`
* stale ancillary context — restart from the current validation step, then refresh ancillaries

### Common mistakes

#### Restarting too late in the flow

Do not do this.

If the earlier identifier is stale, later-step retries will keep failing.

#### Restarting too early for `301`

Do not do this by default.

If search context is still usable, start again from `verify.do`.

#### Keeping old ancillaries after a restart

Do not do this.

Refresh baggage and seat context after a new verify or offer lookup.

### Related pages

* [Identifiers](../identifiers.md)
* [Search vs Offer](search-vs-offer.md)
* [202 vs 301 vs 308](../../../../support-and-reference/troubleshooting-and-support/errors-handing/202-vs-301-vs-308.md)
* [Verify](../../booking-step-guides/verify.md)
* [Get Offer](../../booking-step-guides/get-offer.md)
* [Baggage and seat productCode freshness](../../optional-ancillaries/baggage-and-seat-productcode-freshness.md)
