---
description: APIs for post-booking ancillaries and related post-ticketing actions.
---

# Post-ticketing Ancillaries

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this section for actions after the original ticket is already issued.

{% hint style="info" %}
Post-ticketing ancillary support here is for baggage.

Post-ticketing seat selection is not supported.
{% endhint %}

### What this section covers

* Search post-booking ancillary options
* Create ancillary orders for issued tickets
* Handle baggage-related post-ticketing flows

### Typical flow

{% stepper %}
{% step %}
### Search Ancillary

Query available post-ticketing ancillary products for the ticketed order.
{% endstep %}

{% step %}
### Order Ancillary

Create the ancillary order with the selected product codes.
{% endstep %}
{% endstepper %}

### Main APIs

* `postBookingAncillarySearch.do`
* `postBookingAncillaryOrder.do`

### Use this when you need

* Add baggage after ticketing
* Handle post-booking ancillary purchases
* Support post-ticketing service operations

### Full API reference

Use the complete endpoint schemas and samples here:

[Post-ticketing Ancillaries](../../api-reference/post-booking-apis/post-ticketing-ancillaries.md)

### Related pages

* [Webhook Overview](../extensions-and-integrations/webhook-overview/)
* [Post-booking](./)
* [Refunds](refunds.md)
