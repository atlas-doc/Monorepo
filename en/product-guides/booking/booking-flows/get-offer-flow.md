---
description: >-
  End-to-end booking steps for known itineraries and independent offer pricing
  from Get Offer through order follow-up.
---

# Get Offer

Path: `Get Offer → Order → Payment → Query Order`

Use this page when the itinerary is already known or when you need an independent price check.

This page defines the end-to-end sequence for this path.

Use [Booking step guides](../booking-step-guides/) when you need endpoint-level detail for one step.

### When to use Get Offer

Use Get Offer when you need to:

* skip Atlas search as the main shopping entry point
* price or validate a known itinerary
* create the order directly from `OfferId`

### Full sequence

{% stepper %}
{% step %}
### Get Offer

Call [Get Offer](../booking-step-guides/get-offer.md).

Keep `OfferId`.
{% endstep %}

{% step %}
### Optional ancillaries

This step is optional.

Use [Optional ancillaries](../optional-ancillaries/) before order creation when seat or baggage upsell is part of your product.
{% endstep %}

{% step %}
### Create Order

Call [Create Order](../booking-step-guides/create-order.md) with `OfferId`.

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

* Keep `OfferId` after `getOffers.do`
* Keep `orderNo` after `order.do`
* Keep airline PNR and `ticketNos` after ticketing completes

### Decision support

Use [Search vs Offer](../booking-overview/booking-decisions/search-vs-offer.md) when you are choosing between the standard search path and Get Offer.

Use [API Reference](../../../api-reference/) when you need exact request and response fields.
