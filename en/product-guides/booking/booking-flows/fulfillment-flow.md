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

Fulfilment API is a fast ticketing path for confirmed itineraries.

Use it when your system can create an order and begin payment immediately.

It starts with `getOfferPrice.do` and uses a strict 5-minute payment and ticketing window.

### Is Fulfilment API right for you?

Use Fulfilment API when you need:

* `getOfferPrice.do` as the entry point
* broader offer display rules
* immediate payment after order creation
* optional seat or baggage upsell before order creation

### Typical use cases

#### Near-departure ticketing

Use Fulfilment API when customers need tickets close to departure.

It supports a fast fulfilment path without the same cache-expiry pressure after submission.

#### Risky inventory and harder-to-display offers

Use this path when inventory is at risk of selling out.

It can return offers that the standard path may filter, including near-departure flights and some higher round-trip prices.

#### Multi-passenger price confirmation

Use Fulfilment API when price accuracy matters for multi-passenger bookings.

It verifies the fare in real time before ticketing. This reduces late price-change risk.

#### Bring-your-own fare fulfilment

Use this path when your system already sources the fare or holds the order context.

Atlas can then complete fare verification, payment, and ticketing without replacing your shopping layer.

#### Automated fulfilment and payment fallback

Use Fulfilment API when you need a dedicated, automation-friendly ticketing path.

It supports deposit and VCC pass-through. Atlas continues fulfilment after it accepts the request.

#### When to use the standard flow

Use the standard booking flow when payment cannot start immediately.

Use it when you need the normal order-hold timing.

See [Get Offer vs Fulfilment API](../booking-overview/booking-decisions/get-offer-vs-get-offer-price.md) for a detailed comparison.

### Core operational rules

{% hint style="warning" %}
Create the order only when payment can start immediately.

Fulfilment API has a strict 5-minute payment and ticketing window.
{% endhint %}

* Keep `OfferId` from `getOfferPrice.do` until `order.do`.
* Keep `orderNo` after `order.do`.
* Do not treat payment success as final ticketing confirmation.
* Follow the order through query or webhook until ticketed or cancelled.
* Keep the airline PNR and `ticketNos` after ticketing completes.

### Integration flow

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

### Follow-up and recovery

Query the order until ticketing reaches a final state.

Do not retry payment blindly when payment may already be processing.

Check the remaining window before every retry.

Use [Post-payment polling](../booking-step-guides/query-order/post-payment-polling.md) for polling timing and retry guidance.

### Related guidance

* **Choose a path:** [Get Offer vs Fulfilment API](../booking-overview/booking-decisions/get-offer-vs-get-offer-price.md)
* **Follow each step:** [Booking steps](../booking-step-guides/)
* **Check request limits:** [API Request Limits](../booking-overview/api-request-limits.md)
* **Check fields:** [API Reference](../../../api-reference/)
