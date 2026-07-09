---
description: >-
  Atlas API order maintenance for order regeneration, ticket stop, and
  operational order lookup after booking.
---

# Order Maintenance

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this page for follow-up order actions outside the standard booking flow.

Start here when you need to:

* regenerate an expired or failed order
* stop ticketing when the flow supports it
* look up orders for operational follow-up

### FAQ

#### When should I use Order Maintenance?

Use this page for operational order actions that happen outside the standard search-to-ticket flow.

#### Which maintenance API should I use first?

Use `regenerateOrder.do` for eligible order regeneration, `stopTicket.do` when ticketing must be stopped, and `orderList.do` when you need operational order lookup.

#### Can fulfillment-flow orders be regenerated?

Yes, when the recovery path supports regeneration for that order state.

Confirm the original order is already unusable first.

Keep the fulfillment-flow identity on the regenerated order when the downstream flow expects it.

### Main APIs

* `regenerateOrder.do`
* `stopTicket.do`
* `orderList.do`

### Use this when you need

* Regenerate expired or failed orders
* Stop ticketing operations when supported
* Search operational order lists
* Recover eligible `getOfferPrice.do` orders after cancellation or airline-side payment failure

### Fulfillment flow maintenance

Use maintenance actions carefully for `getOfferPrice.do` orders.

Confirm the original order reached a final cancelled or unpayable state before regeneration.

Do not use maintenance actions to stretch the 5-minute ticketing deadline.

### What comes next?

Open the exact endpoint page below for request and response details, then reconcile the result with the current order state if needed.

### Full API reference

See endpoint-level details here:

* [Regenerate Order](../../api-reference/post-booking-apis/regenerate-order.md)
* [Stop Ticket Issuance](../../api-reference/post-booking-apis/stop-ticket-issuance.md)
* [Order List](../../api-reference/post-booking-apis/order-list.md)

### Related pages

* [Post-booking](./)
* [Post-booking APIs](../../api-reference/post-booking-apis/)
* [Hybrid Payment Guide](../booking/booking-step-guides/payment-and-ticketing/hybrid-payment-guide.md)
* [Error Codes](../../support-and-reference/troubleshooting-and-support/errors-handing/)
