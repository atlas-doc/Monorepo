---
description: >-
  Atlas API payment and ticketing flow for pay.do, payment methods, retry
  safety, and final ticketing follow-up.
---

# Payment & Ticketing

{% include "../../../../.gitbook/includes/eva-help-hint.md" %}

Use this page to complete payment and wait for ticket issuance.

Start here when you need to:

* pay an existing order
* choose the correct payment method
* track final ticketing after `pay.do`

### FAQ

#### What do I need before `pay.do`?

You need a valid `orderNo`, a supported payment method, and card data when the method is card-based.

The order must still be unpaid and still support the selected payment path.

#### Does payment success mean ticketing is already complete?

No.

Payment success does not always mean the airline PNR and ticket numbers are already final.

Use order follow-up until the final ticketing state is confirmed.

#### Is the deadline different for fulfillment-flow orders?

Yes.

Orders created from `getOfferPrice.do` use a 5-minute payment and ticketing window.

If ticketing does not complete in time, Atlas cancels the order automatically.

### Main API

* `pay.do`

### Use this when you need

* Deposit payment
* VCC pass-through payment
* BYOA payment
* MoR payment
* Ticket issuance tracking after payment

### Before you call

Confirm these points first:

* the order already exists
* the order is still unpaid
* the order supports the selected payment method
* card data is ready if you use card-based payment

For standard flows, call `order.do` before `pay.do`.

### What should you keep in mind after payment?

Keep using `orderNo` for order follow-up.

Read the final ticketing state from order query.

Do not send duplicate payment requests when payment may already be in progress or completed.

### Payment methods

* `1`: Deposit
* `3`: VCC passthrough
* `4`: BYOA
* `5`: MoR

### Key inputs

Always send:

* `orderNo`
* `paymentMethod`

Send `creditCard` when using:

* VCC passthrough
* MoR

`threeDS.ip` is only relevant for MoR.

### What comes next?

After `pay.do`, use [Query Order](../query-order/) until the final ticketed state is confirmed.

Use webhook as a supplement, not as the only confirmation path.

### What to watch

* supported payment methods vary by airline and fare
* card brand must match the order requirements
* payment can fail if the booking is past deadline
* payment success does not always mean ticketing is already finished
* you still need order follow-up until the final ticketing state is confirmed

### Best practice

* read supported payment methods from the booking flow before payment
* use deposit when you need fare guarantee after payment
* use VCC only when the fare supports it
* poll order status after payment until ticketing completes
* handle payment retries carefully to avoid duplicate charges

### Fulfillment flow deadline

Apply these extra rules when the order comes from `getOfferPrice.do`:

* start payment immediately after order creation
* check the remaining time before every retry
* only retry when the order is still inside the safe operating window
* stop retrying when the order is already near timeout

{% hint style="warning" %}
Do not apply the standard 30-minute order-hold expectation to fulfillment-flow orders.

This flow is designed around a 5-minute ticketing deadline.
{% endhint %}

### Safe retry rule

If payment may already have started, query the order first.

Do not retry payment blindly after `402`, `404`, `406`, or similar order-state errors.

### Common failure cases

Common payment response failures include:

* invalid request data
* payment after deadline
* unsupported payment method
* order already paid
* payment already in progress
* missing passenger data
* card not supported
* card mismatch
* order not confirmed in FR flow

Use the API response `status` as the source of truth.

### Related pages

* [Create Order](../create-order.md)
* [Confirm Order](../confirm-order.md)
* [Query Order](../query-order/)
* [Hybrid Payment Guide](hybrid-payment-guide.md)
* [Error Codes](../../../../support-and-reference/troubleshooting-and-support/errors-handing/)
* [Booking APIs](../../../../api-reference/booking-apis/)

### Full API reference

See endpoint-level details here:

* [Payment & Ticketing](../../../../api-reference/booking-apis/payment-and-ticketing.md)
