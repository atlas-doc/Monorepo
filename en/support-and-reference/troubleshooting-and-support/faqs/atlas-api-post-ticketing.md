---
description: >-
  Common post-booking questions about notifications, refunds, service requests,
  and urgent operations.
---

# Post-booking

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page for refund, schedule change, and operational follow-up questions.

{% hint style="info" %}
Submit Service Requests through Eva in ATRIP.
{% endhint %}

### Do we get notified about schedule changes?

Yes, but not always through a single channel.\
Airlines may notify the booking contact directly.\
Atlas webhook and incident flows should also be configured.

### Does Atlas guarantee webhook delivery?

No.\
Webhook delivery is best effort.

Use airline emails, incident flows, and order queries for final confirmation.

### How should post-booking operations be handled?

Use Atlas APIs and ATRIP based on the action:

* refunds and cancellations
* ancillary add-ons
* service requests for changes
* incident follow-up

### Do you provide urgent post-sale support?

For urgent cases within 24 hours of departure, use the airline’s **Manage My Booking** flow where possible.

### Where should we check refund and cancellation policy?

Always use the airline’s latest policy as the source of truth.

### How long do refunds take?

Atlas usually submits refund requests to the airline within 4 hours.\
Final confirmation and fund return still depend on the airline.

After Atlas receives the funds, reconciliation and balance credit follow.

### How does Atlas void handling work?

Use the dedicated void flow:

* `voidQuotation.do`
* `void.do`
* `queryVoidOrders.do`

Request quotation first.

Then submit the void with the latest `voidOfferId`.

Track status until the case is closed.

See [Void](../../../product-guides/post-booking/void.md).

### Does Atlas support partial void for some passengers?

No.\
Atlas accepts full-order void only.

Do not submit void for only some passengers.

### What happens if we submit void after the deadline?

Atlas rejects the request in real time.\
Typical message:

* `Void deadline exceeded. This ticket can no longer be voided`

If the void window has passed, re-check whether the case should move to refund.

### Is void quotation required when the void fee is fixed?

Yes.\
`voidQuotation.do` is still required before `void.do`.

### How fast can we get a void result?

In most cases, Atlas returns within about 5 minutes whether the void request was accepted for processing.\
Final completion or rejection can still take longer.

Use webhook for progress updates.\
Use void query for final reconciliation.

### How should booking changes be requested?

Submit a Service Request through Eva in ATRIP for name correction, flight change, or similar post-booking action.

### Are booking changes supported through API?

Not as a general self-service API flow.\
Use Eva in ATRIP to submit the Service Request.

### How are involuntary changes handled?

For airline schedule changes or similar involuntary cases, use the refund flow in ATRIP.\
This is handled free of charge.

### Can baggage or seat be added after ticketing?

Baggage may be added after ticketing when the airline and order support it.\
Seat selection after ticketing is not supported.

See [Seats](../../../product-guides/booking/optional-ancillaries/seats-and-baggage/) for the current seat-selection support scope.

### What happens in case of booking or service failure?

If Atlas causes incorrect booking or ticketing, Atlas will compensate with a replacement ticket when applicable.\
Refund delays remain dependent on airline processing.

### What support or training is provided for operations teams?

Atlas provides a go-live walkthrough after UAT completion.\
That includes ATRIP process guidance and follow-up Q\&A.

### How does refund handling differ by payment mode?

#### Deposit

* Atlas tracks refunds initiated through Atlas
* If the passenger or agency refunds directly with the airline, notify Atlas through ATRIP when required
* Atlas credits your Atlas balance after airline funds are received

#### VCC

Refunded funds usually go back to the original VCC account.\
Do not use the ATRIP **Agent and Passenger Initiated Refund** flow for VCC refunds.

### What refund initiation options are available in ATRIP?

#### Atlas-initiated refund

Use either:

* the **Refund** button
* a **Cancel & Refund** service request through Eva

#### Agency or passenger initiated refund

Use either:

* an **Agency & Passenger Initiated Refund** service request through Eva
* batch upload in the refund module

### How should refund follow-up be handled?

Wait at least 21 days after refund submission before follow-up.\
Then follow up in the existing service request through Eva, or create a new refund follow-up request in ATRIP.

### Related pages

* [Refunds](../../../product-guides/post-booking/refunds.md)
* [Post-booking](../../../product-guides/post-booking/)
* [Webhook Overview](../../../product-guides/extensions-and-integrations/webhook-overview/)
