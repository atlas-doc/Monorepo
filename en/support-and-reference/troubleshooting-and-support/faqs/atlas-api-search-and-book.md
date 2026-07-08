---
description: >-
  Common Atlas API booking flow questions about search.do, getOffers.do, verify
  pricing, identifiers, passenger count, timing, and offer refresh.
---

# Search & Booking

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page for search response, pricing, and booking timing questions.

Start here when you need to:

* choose between `search.do` and `getOffers.do`
* keep the right identifier for the next step
* understand why displayed price changed before booking
* confirm safe timing between search, verify, and order

### FAQ

#### Which identifier should we keep from each booking step?

Keep `routingIdentifier` from `search.do` for `verify.do`.

Keep `sessionId` from `verify.do` for `order.do` and seat lookup in the standard flow.

Keep `OfferId` from `getOffers.do` for the Get Offer order flow.

#### When should we use `search.do` and when should we use `getOffers.do`?

Use `search.do` when Atlas is your main shopping entry point.

Use `getOffers.do` when you already know the target itinerary or need an independent price check.

#### How should we choose between `search.do`, `getOffers.do`, and `priceCompareSearch.do`?

Use `search.do` for the standard booking flow.

Use `getOffers.do` when the itinerary is already known or when you need an independent price check.

Use `priceCompareSearch.do` for pre-sale route coverage and raw price discovery.

Do not use `priceCompareSearch.do` as a production booking price source.

#### Why do we still need `verify.do` after `search.do`?

`search.do` can return cached pricing.

`verify.do` checks live fare, inventory, and booking conditions before order creation.

Treat the verify response as the current source of truth before booking.

### Can users switch display currency?

No.\
Pricing is returned in the agreed contractual currency.

### Why is tax breakdown missing in some search results?

Many LCCs do not provide tax split data during booking or in the PNR.\
Atlas can only expose the breakdown when the airline provides it.

### What does `TransactionFeePerPax` mean?

It is the Atlas technical service fee charged per passenger.\
It is separate from airfare and tax.\
It is non-refundable.

### Why are fields like `bookingclass` or `farebasis` missing?

Many LCCs do not return those values.\
Use `cabin` when available.\
Do not assume GDS-style fare data exists for every airline.

### How many results does search return?

Search returns all available offers by default.\
Default sorting is lowest fare first.

### When should we use `getOffers.do` instead of `search.do`?

Use `search.do` when Atlas is your main shopping entry point.\
Use `getOffers.do` when you already know the target itinerary or need an independent price check.

`getOffers.do` is a better fit for external shopping engines and final price validation flows.

### Why can search and verify return different prices?

Search may use cached data.\
Verify checks live fare and availability before order creation.

If the price changed, use the verify result as the current source of truth.\
For Get Offer flows, refresh the offer before ordering when needed.

#### What is the safest timing between search, verify, and order?

Up to 6 hours between search and verify is allowed.

Up to 2 hours between verify and order is allowed.

Shorter is safer in both cases.

### What does `seatCount` mean?

It is the remaining seat count for the fare.\
Atlas caps the practical maximum at 4 because larger LCC bookings fail more often.

### How long can we wait between search and verification?

Up to 6 hours is allowed.\
Shorter is better because prices may change.

### Does Atlas support fare families?

Yes.\
Enable `includeMultipleFareFamily` in search when you need fare-family results.

Availability still depends on airline support and current inventory.

### Can we filter baggage during search?

No.\
Choose the itinerary first.

Then query baggage options with `getLuggage.do` when baggage matters before booking.

See [Baggage](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ftzqh42LAaE6QYzklv67).

### What seat selection scenarios are supported?

Atlas supports seat selection for airlines that support Atlas API seat capability.

Atlas supports Atlas-issued orders and seat selection purchased with the ticket in the booking flow.

Atlas does not support non-Atlas-issued orders or post-ticketing seat selection.

See [Seats](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/3ujCySdZ8OYYLfGI3iF3) for the current support scope.

### Can we call `seatAvailability.do` with flight information only?

No.

Use a valid `sessionId` from `verify.do` or `OfferId` from `getOffers.do`.

`seatAvailability.do` no longer supports independent mode.

If your upstream seat request only contains flight data, match it to a cached `sessionId` first.

### How long can we wait between verification and order?

Up to 2 hours is allowed.\
Shorter is better because pricing and availability may change.

### Can passenger count change between search and order?

Yes, if there is still at least one adult traveler.\
But keeping the same count across search, verification, and order is safer.

Changing count after verification increases failure risk because verification checks live inventory.

### Does `getOffers.do` require `verify.do`?

Not in the standard Get Offer flow.\
That path is built around the returned `OfferId` and then continues to `order.do`.

Use the Get Offer guide and current API reference when implementing that path.

#### When should we refresh a Get Offer result?

Refresh it when passenger count, target flight, expected fare, or booking timing changed.

Do not create an order from stale offer assumptions.

### Does Atlas apply request limits to booking APIs?

Yes.

Atlas applies request-limit governance to selected pre-booking APIs.

Default limits:

* `search.do` — `10 QPS`
* `verify.do` + `getOffers.do` — shared `60 QPM`
* `seatAvailability.do` + `getLuggage.do` — shared `60 QPM`

`order.do` and `pay.do` are not part of this policy.

### What does `429` mean?

It means the current request frequency exceeded the configured limit.

It does not mean the account is banned.

It does not cancel an order already in progress.

### How should we handle `429`?

Read the returned `retryAfter` value.

Wait for that delay before retrying.

Reduce burst traffic and avoid immediate retry loops.

### Are `verify.do` and `getOffers.do` counted separately?

No.

They share one fulfillment pool.

The default shared limit is `60 QPM`.

### Are `seatAvailability.do` and `getLuggage.do` counted separately?

No.

They share one ancillary pool.

The default shared limit is `60 QPM`.

### Do cache-hit requests count toward the limit?

Yes.

If the request enters Atlas business processing and returns a result, it counts toward the pool.

Use [API Request Limits](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV) for the full limit model.

### Related pages

* [Identifiers](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ns5eKoKIPFUTFhjJkPyC)
* [Search vs Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Pcq0icGceiiiaVBThnzx)
* [Search](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/9K7uEnLGfEbpjGjni5gD)
* [Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FSGess6buGE1P02WnVNu)
* [Verify](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm)
* [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE)
