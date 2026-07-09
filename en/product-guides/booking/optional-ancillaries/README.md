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

Start with [Seats](seats-and-baggage/).

Then use [Seat fallback modes](seats-and-baggage/seat-fallback-modes.md) when order-time seat handling needs a business rule.

#### Add baggage

Start with [Baggage](baggage.md).

Use it when baggage quote and segment mapping are part of the booking flow.

#### Validate freshness before booking

Use [Baggage and seat productCode freshness](baggage-and-seat-productcode-freshness.md) before `order.do` when the session, offer, itinerary, or passenger mix changed.

### Pages in this section

* [Seats](seats-and-baggage/)
* [Baggage](baggage.md)
* [Baggage and seat productCode freshness](baggage-and-seat-productcode-freshness.md)

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

* [Seats](seats-and-baggage/)
* [Seat fallback modes](seats-and-baggage/seat-fallback-modes.md)

#### Add baggage before booking

Use:

* [Baggage](baggage.md)
* [Create Order](../booking-step-guides/create-order.md)

#### Fix stale ancillary failures

Use:

* [Baggage and seat productCode freshness](baggage-and-seat-productcode-freshness.md)
* [Error Codes](../../../support-and-reference/troubleshooting-and-support/errors-handing/)

### Related pages

* [Booking Overview](../booking-overview/)
* [Get Offer](../booking-step-guides/get-offer.md)
* [Get Offer Price](../booking-step-guides/get-offer-price.md)
* [Verify](../booking-step-guides/verify.md)
* [Create Order](../booking-step-guides/create-order.md)
