---
description: >-
  End-to-end Fulfilment API steps from Get Offer Price through order follow-up
  with a strict 5-minute payment and ticketing window.
---

# 🆕 Fulfilment API

Path: `Get Offer Price → Order → Payment → Query Order`

{% hint style="warning" %}
**🆕 New product:** Use Fulfilment API for the new `getOfferPrice.do` booking path and immediate payment after order creation.
{% endhint %}

Use this page when you need Fulfilment API and your system can move to payment immediately.

This page defines the end-to-end sequence.

Use [Booking steps](../booking-step-guides/) when you need endpoint-level detail for one step.

### When to use Fulfilment API

Use Fulfilment API when you need to:

* use `getOfferPrice.do` as the entry point
* use broader display rules
* add optional ancillaries before order when the product needs seat or baggage upsell
* create and pay the order without delay

### Full sequence

{% stepper %}
{% step %}
### Get Offer Price

Call [Get Offer Price](../booking-step-guides/get-offer-price.md).

Keep the returned `OfferId`.
{% endstep %}

{% step %}
### Optional ancillaries

This step is optional.

Use [Optional ancillaries](../optional-ancillaries/) before order creation when seat or baggage upsell is part of your product.
{% endstep %}

{% step %}
### Create Order

Call [Create Order](../booking-step-guides/create-order.md) with `OfferId` only when payment can start immediately.

Keep `orderNo`.
{% endstep %}

{% step %}
### Payment & Ticketing

Call [Payment & Ticketing](../booking-step-guides/payment-and-ticketing/) without delay.

Treat the 5-minute payment and ticketing window as strict.
{% endstep %}

{% step %}
### Query Order

Use [Query Order](../booking-step-guides/query-order/) as the standard follow-up step after payment.

Keep following the order until it is ticketed or cancelled.

Use [Post-payment polling](../booking-step-guides/query-order/post-payment-polling.md) for polling timing and retry guidance.
{% endstep %}
{% endstepper %}

### Key rules

* Keep `OfferId` from `getOfferPrice.do` until `order.do`
* Start payment immediately after order creation
* Treat the 5-minute Fulfilment API window as strict
* Keep `orderNo` after `order.do`
* Follow the final state through order query or webhook
* Keep airline PNR and `ticketNos` after ticketing completes

### Decision support

Use [Get Offer vs Fulfilment API](../booking-overview/booking-decisions/get-offer-vs-get-offer-price.md) when you are choosing between Get Offer and Fulfilment API.

Use [API Request Limits](../booking-overview/api-request-limits.md) when you need request-limit guidance for pre-booking APIs.

Use [API Reference](../../../api-reference/) when you need exact request and response fields.
