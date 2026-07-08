---
description: >-
  Optional seat and baggage guidance for supported booking flows, including
  selection timing, freshness rules, and fallback handling.
---

# Optional ancillaries

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this section when you need to add optional seats or baggage to a booking safely.

This is not a mandatory booking step.

Use it only when ancillary upsell is part of your product and the booking flow supports it.

Supported booking contexts are:

* `sessionId` after `verify.do`
* `OfferId` after `getOffers.do`
* `OfferId` after `getOfferPrice.do`

This section helps you:

* choose the right ancillary lookup step
* keep seat and baggage data fresh before `order.do`
* handle seat fallback behavior explicitly
* avoid stale `productCode` failures

### Short answer

Seats and baggage are optional add-ons in the booking flow.

Add them only when needed.

Use seat and baggage data close to order creation.

Refresh ancillaries when the booking context changed or booking was delayed.

Do not treat seat or baggage `productCode` values as reusable catalog IDs.

### When to use this section

Use this section when:

* you want to add seat upsell before booking
* you want to add baggage upsell before booking
* `order.do` fails because ancillary data may be stale
* you need to decide what happens if a selected seat is no longer available

Skip this section when the booking does not include seat or baggage upsell.

### Reading order

#### Add seats

Start with [Seats](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/3ujCySdZ8OYYLfGI3iF3).

Then use [Seat fallback modes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/gwnqga4Hd9HkYrjG8NVb) when order-time seat handling needs a business rule.

#### Add baggage

Start with [Baggage](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ftzqh42LAaE6QYzklv67).

Use it when baggage quote and segment mapping are part of the booking flow.

#### Validate freshness before booking

Use [Baggage and seat productCode freshness](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Cxdx0FWp0CbRm6vH8YZg) before `order.do` when the session, offer, itinerary, or passenger mix changed.

### Pages in this section

* [Seats](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/3ujCySdZ8OYYLfGI3iF3)
* [Baggage](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ftzqh42LAaE6QYzklv67)
* [Baggage and seat productCode freshness](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Cxdx0FWp0CbRm6vH8YZg)

### Quick decision rules

#### When should you query seats?

Query seats only from a valid booking context.

Use `sessionId` after `verify.do` or `OfferId` after `getOffers.do` or `getOfferPrice.do`.

#### When should you query baggage?

Query baggage after the target itinerary is confirmed.

Keep the segment mapping exact.

#### When should you refresh ancillaries?

Refresh them when:

* `sessionId` changed
* `OfferId` changed
* itinerary changed
* passenger count or passenger type changed
* booking was delayed long enough to make the old context unreliable

### Common risks

#### Reusing stale ancillary data

Old seat or baggage selections may no longer match the current booking context.

This can cause ancillary mismatch failures during `order.do`.

#### Treating `productCode` like a stable SKU

Do not do this.

Seat and baggage `productCode` values are context-bound.

#### Ignoring seat fallback behavior

If a selected seat disappears before fulfillment, the order outcome depends on the seat handling mode you send.

Make that behavior explicit.

### Recommended next pages by task

#### Add seats before booking

Use:

* [Seats](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/3ujCySdZ8OYYLfGI3iF3)
* [Seat fallback modes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/gwnqga4Hd9HkYrjG8NVb)

#### Add baggage before booking

Use:

* [Baggage](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ftzqh42LAaE6QYzklv67)
* [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE)

#### Fix stale ancillary failures

Use:

* [Baggage and seat productCode freshness](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Cxdx0FWp0CbRm6vH8YZg)
* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)

### Related pages

* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FSGess6buGE1P02WnVNu)
* [Get Offer Price](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/e7tapaArEz0MBOv62dxZ)
* [Verify](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm)
* [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE)
