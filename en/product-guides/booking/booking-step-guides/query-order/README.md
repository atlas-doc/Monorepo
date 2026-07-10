---
description: >-
  Atlas API order query flow for booking status, ticketing progress, airline
  PNR, and final order follow-up.
---

# Query Order

{% include "../../../../.gitbook/includes/eva-help-hint.md" %}

Use this page to check the latest booking state.

This is the standard follow-up step after `pay.do`.

If you need polling rules and timing guidance, use [Post-payment polling](post-payment-polling.md).

Start here when you need to:

* track ticketing after `pay.do`
* confirm whether an order is already paid or ticketed
* read airline PNR and ticket details after fulfilment

### FAQ

#### When should I call `queryOrderDetails.do`?

Call it after `order.do` or `pay.do` when you need the latest order state.

Use it as the main follow-up API until the booking reaches the final state.

#### What should I check in the order query response?

Check `orderStatus`, `ticketStatus`, airline PNR details, and ticket numbers.

Use these fields to confirm whether ticketing is still in progress or already complete.

### Main API

* `queryOrderDetails.do`

### Use this when you need

* Poll ticketing progress
* Retrieve booking and passenger details
* Confirm airline PNR and final status

### Common checks

* `orderStatus`
* `ticketStatus`
* Airline PNR details
* Ancillary and fare data

### What does order query help you decide?

Use it to decide:

* whether payment should be retried or not
* whether ticketing is still processing
* whether airline PNR and ticket numbers are already available
* whether post-booking actions can start

### Best practice

Use `queryOrderDetails.do` as the main status source after payment.

Webhook can help, but it should not be your only confirmation path.

If payment may already be in progress or completed, query the order before any retry.

### Fulfilment-flow follow-up

If the order came from `getOfferPrice.do`, monitor it more aggressively.

Use order query to confirm whether the order is still ticketing, already ticketed, or already cancelled by timeout.

Do not keep retrying payment when the order is already close to the 5-minute fulfilment deadline.

### Related pages

* [Payment & Ticketing](../payment-and-ticketing/)
* [Post-ticketing Ancillaries](../../../post-booking/post-ticketing-ancillaries.md)
* [Webhook Overview](../../../extensions-and-integrations/webhook-overview/)
* [Booking APIs](../../../../api-reference/booking-apis/)

### Full API reference

See endpoint-level details here:

* [Query Order](../../../../api-reference/booking-apis/query-order.md)
