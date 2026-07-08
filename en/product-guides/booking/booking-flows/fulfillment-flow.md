---
description: >-
  Fulfillment booking path from Get Offer Price through order follow-up with a
  strict 5-minute payment and ticketing window.
---

# Fulfillment flow

Path: `Get Offer Price → Order → Payment → Query Order`

Use this flow when you need the fulfillment path and your system can move to payment immediately.

This page defines the end-to-end sequence for this path.

Use [Booking step guides](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/7Hivwro5sZdOotzmaEIn) when you need endpoint-level detail for one step.

### When to use this flow

Use this flow when you need to:

* use `getOfferPrice.do` as the entry point
* access the fulfillment path with broader display rules
* add optional ancillaries before order when the product needs seat or baggage upsell
* create and pay the order without delay

### Full flow

{% stepper %}
{% step %}
### Get Offer Price

Call [Get Offer Price](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/e7tapaArEz0MBOv62dxZ).

Keep the returned `OfferId`.
{% endstep %}

{% step %}
### Optional ancillaries

This step is optional.

Use [Optional ancillaries](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Bbuhdlzobxaya4FUurUl) before order creation when seat or baggage upsell is part of your product.
{% endstep %}

{% step %}
### Create Order

Call [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE) with `OfferId` only when payment can start immediately.

Keep `orderNo`.
{% endstep %}

{% step %}
### Payment & Ticketing

Call [Payment & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB) without delay.

Treat the 5-minute payment and ticketing window as strict.
{% endstep %}

{% step %}
### Query Order

Use [Query Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n) as the standard follow-up step after payment.

Keep following the order until it is ticketed or cancelled.

Use [Post-payment polling](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2qOXdnt78bFPEFbkcemP) for polling timing and retry guidance.
{% endstep %}
{% endstepper %}

### Key rules

* Keep `OfferId` from `getOfferPrice.do` until `order.do`
* Start payment immediately after order creation
* Treat the 5-minute fulfillment window as strict
* Keep `orderNo` after `order.do`
* Follow the final state through order query or webhook
* Keep airline PNR and `ticketNos` after ticketing completes

### Decision support

Use [Get Offer vs Get Offer Price](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/hJ5KgpKJEmpzw2hRXmYp) when you are choosing between Get Offer and Get Offer Price.

Use [API Request Limits](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV) when you need request-limit guidance for pre-booking APIs.

Use [API Reference](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/LfT8Y3jMIGXTnxwihZhV) when you need exact request and response fields.
