---
description: >-
  Booking path for known itineraries and independent offer pricing from Get
  Offer through order follow-up.
---

# Get Offer flow

Path: `Get Offer → Order → Payment → Query Order`

Use this flow when the itinerary is already known or when you need an independent price check.

This page defines the end-to-end sequence for this path.

Use [Booking step guides](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/7Hivwro5sZdOotzmaEIn) when you need endpoint-level detail for one step.

### When to use this flow

Use this flow when you need to:

* skip Atlas search as the main shopping entry point
* price or validate a known itinerary
* create the order directly from `OfferId`

### Full flow

{% stepper %}
{% step %}
### Get Offer

Call [Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FSGess6buGE1P02WnVNu).

Keep `OfferId`.
{% endstep %}

{% step %}
### Optional ancillaries

This step is optional.

Use [Optional ancillaries](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Bbuhdlzobxaya4FUurUl) before order creation when seat or baggage upsell is part of your product.
{% endstep %}

{% step %}
### Create Order

Call [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE) with `OfferId`.

Keep `orderNo`.
{% endstep %}

{% step %}
### Optional FR confirmation

This step is airline-specific.

Use [Confirm Order (FR only)](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/cyd69uDJk3ulct18V6QB) before payment when the airline requires it.
{% endstep %}

{% step %}
### Payment & Ticketing

Call [Payment & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB).

Payment success does not always mean final ticketing is already complete.
{% endstep %}

{% step %}
### Query Order

Use [Query Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n) as the standard follow-up step after payment.

Keep following the order until it is ticketed or reaches another terminal state.

Use [Post-payment polling](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2qOXdnt78bFPEFbkcemP) for polling timing and retry guidance.
{% endstep %}
{% endstepper %}

### Key identifiers

* Keep `OfferId` after `getOffers.do`
* Keep `orderNo` after `order.do`
* Keep airline PNR and `ticketNos` after ticketing completes

### Decision support

Use [Search vs Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Pcq0icGceiiiaVBThnzx) when you are choosing between the standard search path and Get Offer.

Use [API Reference](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/LfT8Y3jMIGXTnxwihZhV) when you need exact request and response fields.
