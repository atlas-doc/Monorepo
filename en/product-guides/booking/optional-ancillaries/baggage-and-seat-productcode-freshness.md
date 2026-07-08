---
description: >-
  How long ancillary productCode values stay usable, when they become stale, and
  how to avoid reusing baggage or seat selections from an old booking context.
---

# Baggage and seat productCode freshness

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when seat or baggage selection fails because the ancillary mapping may be stale.

### Short answer

Treat baggage and seat `productCode` values as booking-context data, not as reusable catalog IDs.

If the verify context, offer context, itinerary, passenger mix, or booking timing changed, refresh ancillaries before `order.do`.

### FAQ

#### Can I reuse an old baggage `productCode`?

Not safely.

Use the `productCode` returned by the current ancillary response for the current booking context.

#### Can I reuse an old seat selection?

Not safely.

Seat availability can change before booking or ticketing.

#### When should I refresh ancillaries?

Refresh them when the booking context changed or when booking was delayed.

### What freshness means here

A `productCode` is only meaningful inside the current booking context.

That context includes:

* current itinerary
* current passenger mix
* current verify or offer state
* current ancillary response

Do not treat ancillary codes as long-lived static values.

### What makes ancillary selection stale

Refresh baggage or seat selection when any of these changed:

* `sessionId`
* `OfferId`
* target flight
* segment structure
* passenger count or passenger type
* fare or inventory state
* booking delay long enough to make the old context unreliable

### Baggage freshness rules

#### Use the latest baggage response

Use the baggage `productCode` from the current `getLuggage.do` response.

#### Keep segment mapping exact

Make sure each baggage selection still matches the correct segment.

#### Keep connected-direction selection consistent

For connecting flights, baggage may need to stay consistent across connected segments in the same direction.

### Seat freshness rules

#### Use the latest seat response

Use seat data from the current `seatAvailability.do` response.

#### Do not assume the seat still exists later

Seat inventory can change before booking and again at ticketing.

#### Keep fulfillment behavior explicit

Set the seat handling mode in `order.do`.

This controls what happens if the selected seat is gone at fulfillment time.

### Common failure signals

Typical stale-ancillary failures include:

* `309` — ancillary `productCode` is invalid or stale
* `409` — baggage `productCode` does not match the segment
* seat or baggage mismatch after the session or offer changed

### Quick decision rule

Use this rule in production:

* new `sessionId` or new `OfferId` — refresh ancillaries
* changed itinerary or passenger mix — refresh ancillaries
* delayed booking — refresh ancillaries before `order.do`

### Common mistakes

#### Reusing baggage `productCode` across a new verify session

Do not do this.

A new `sessionId` means the old ancillary context may be stale.

#### Reusing seat selections after itinerary changes

Do not do this.

Even small flight changes can break seat mapping.

#### Treating `productCode` like a permanent SKU

Do not do this.

It is context-bound booking data.

### Best practice

Keep ancillary selection close to order creation.

If booking is delayed, rerun ancillary lookup before `order.do`.

### Related pages

* [Seats](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/3ujCySdZ8OYYLfGI3iF3)
* [Baggage](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ftzqh42LAaE6QYzklv67)
* [Verify](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm)
* [Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FSGess6buGE1P02WnVNu)
* [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE)
* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)
