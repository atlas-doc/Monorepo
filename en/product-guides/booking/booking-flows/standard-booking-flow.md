---
description: >-
  Standard Atlas booking path from search through order follow-up for partners
  who use Atlas as the main shopping and booking layer.
---

# Standard booking flow

Path: `Search → Verify → Order → Payment → Query Order`

Use this flow when Atlas is your main shopping and booking layer.

This page defines the end-to-end sequence for this path.

Use [Booking step guides](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/7Hivwro5sZdOotzmaEIn) when you need endpoint-level detail for one step.

### When to use this flow

Use this flow when you need to:

* start from Atlas search results
* recheck fare and booking requirements before order creation
* follow the standard booking sequence from search to ticketing

### Full flow

{% stepper %}
{% step %}
### Search

Call [Search](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/9K7uEnLGfEbpjGjni5gD).

Keep `routingIdentifier`.
{% endstep %}

{% step %}
### Verify

Call [Verify](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm) before order creation.

Keep `sessionId`.
{% endstep %}

{% step %}
### Optional ancillaries

This step is optional.

Use [Optional ancillaries](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Bbuhdlzobxaya4FUurUl) before order creation when seat or baggage upsell is part of your product.
{% endstep %}

{% step %}
### Create Order

Call [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE).

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

* Keep `routingIdentifier` after `search.do`
* Keep `sessionId` after `verify.do`
* Keep `orderNo` after `order.do`
* Keep airline PNR and `ticketNos` after ticketing completes

### Decision support

Use [Booking decisions](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ygfSw8OHHyKfi9HuC7VS) when you need to compare this path with Get Offer or Fulfillment.

Use [API Reference](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/LfT8Y3jMIGXTnxwihZhV) when you need exact request and response fields.
