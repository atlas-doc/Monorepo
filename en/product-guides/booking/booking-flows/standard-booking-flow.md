---
description: >-
  End-to-end Atlas booking steps from Search through order follow-up for
  partners who use Atlas as the main shopping and booking layer.
---

# Standard booking

Path: `Search → Verify → Order → Payment → Query Order`

Use this page when Atlas is your main shopping and booking layer.

This page defines the end-to-end sequence for this path.

Use [Booking steps](../booking-step-guides/) when you need endpoint-level detail for one step.

### When to use Standard booking

Use Standard booking when you need to:

* start from Atlas search results
* recheck fare and booking requirements before order creation
* follow the standard booking sequence from search to ticketing

### Full sequence

{% stepper %}
{% step %}
### Search

Call [Search](../booking-step-guides/search.md).

Keep `routingIdentifier`.
{% endstep %}

{% step %}
### Verify

Call [Verify](../booking-step-guides/verify.md) before order creation.

Keep `sessionId`.
{% endstep %}

{% step %}
### Optional ancillaries

This step is optional.

Use [Optional ancillaries](../optional-ancillaries/) before order creation when seat or baggage upsell is part of your product.
{% endstep %}

{% step %}
### Create Order

Call [Create Order](../booking-step-guides/create-order.md).

Keep `orderNo`.
{% endstep %}

{% step %}
### Optional FR confirmation

This step is airline-specific.

Use [Confirm Order (FR only)](../booking-step-guides/confirm-order.md) before payment when the airline requires it.
{% endstep %}

{% step %}
### Payment & Ticketing

Call [Payment & Ticketing](../booking-step-guides/payment-and-ticketing/).

Payment success does not always mean final ticketing is already complete.
{% endstep %}

{% step %}
### Query Order

Use [Query Order](../booking-step-guides/query-order/) as the standard follow-up step after payment.

Keep following the order until it is ticketed or reaches another terminal state.

Use [Post-payment polling](../booking-step-guides/query-order/post-payment-polling.md) for polling timing and retry guidance.
{% endstep %}
{% endstepper %}

### Key identifiers

* Keep `routingIdentifier` after `search.do`
* Keep `sessionId` after `verify.do`
* Keep `orderNo` after `order.do`
* Keep airline PNR and `ticketNos` after ticketing completes

### Decision support

Use [Booking decisions](../booking-overview/booking-decisions/) when you need to compare this path with Get Offer or Fulfilment.

Use [API Reference](../../../api-reference/) when you need exact request and response fields.
