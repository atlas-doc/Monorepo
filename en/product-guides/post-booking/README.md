---
description: >-
  Atlas API post-booking overview for refunds, voids, ancillaries, order
  maintenance, and PNR claim workflows after booking.
---

# Post-booking

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this section after the booking flow is complete.

Start here when you need to:

* choose the right post-booking workflow
* decide whether the case is a refund, void, ancillary, maintenance, or PNR issue
* route operational follow-up after ticketing

### FAQ

#### What should I use after the booking flow is complete?

Use this section for refunds, voids, post-ticketing ancillaries, order maintenance, and PNR claim workflows.

Start by checking the current order state before taking post-booking action.

#### Which post-booking path should I choose?

Use **Refunds** for refund quotation, submission, and status tracking.

Use [**Void**](void.md) when the order is still inside the airline void window and should follow the dedicated void flow.

Use **Post-ticketing Ancillaries** for baggage actions after ticketing.

Use **Order Maintenance** and **PNR Claim & Extraction** when the booking needs operational follow-up or intervention.

### Pages in this section

* [Order Maintenance](order-maintenance.md)
* [Refunds](refunds.md)
* [Void](void.md)
* [Post-ticketing Ancillaries](post-ticketing-ancillaries.md)
* [PNR Claim & Extraction](pnr-claim-and-extraction.md)

### Recommended order of checks

1. Confirm the latest booking state.
2. Decide whether the case is refund, void, ancillary, maintenance, or PNR related.
3. Use the matching workflow page.
4. Reconcile with webhook, order query, or operations follow-up when needed.

### What this section covers

* Post-ticketing ancillaries
* Refund requests and tracking
* Void requests and tracking
* Order maintenance and follow-up operations
* PNR extraction and claim workflows

### Typical flow

{% stepper %}
{% step %}
### Check the order state

Track ticketing progress and order changes.
{% endstep %}

{% step %}
### Handle post-booking actions

Add ancillaries or process refunds.
{% endstep %}

{% step %}
### Resolve operational follow-ups

Use order maintenance and PNR tools when bookings need intervention.
{% endstep %}
{% endstepper %}

### Start here by task

#### Refund handling

Use [Refunds](refunds.md).

#### Void handling

Use [Void](void.md).

#### Post-ticketing baggage

Use [Post-ticketing Ancillaries](post-ticketing-ancillaries.md).

#### Operational intervention

Use [Order Maintenance](order-maintenance.md).

#### PNR claim or extraction

Use [PNR Claim & Extraction](pnr-claim-and-extraction.md).

### Related pages

* [Post-ticketing Ancillaries](post-ticketing-ancillaries.md)
* [Refunds](refunds.md)
* [Void](void.md)
* [Order Maintenance](order-maintenance.md)
* [PNR Claim & Extraction](pnr-claim-and-extraction.md)
* [Webhook Overview](../extensions-and-integrations/webhook-overview/)

### Full API reference

Use endpoint-level details here:

[Post-booking APIs](../../api-reference/post-booking-apis/)
