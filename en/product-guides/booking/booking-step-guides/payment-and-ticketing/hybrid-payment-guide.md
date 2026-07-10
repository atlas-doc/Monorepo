---
description: >-
  Recover failed VCC pass-through payments by switching to deposit or another
  card.
icon: right-left
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Hybrid Payment Guide

{% include "../../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when VCC pass-through fails and you need a safe fallback path.

### What hybrid payment means

Hybrid payment is a retry strategy for one booking.

It switches the payment path after a failed payment attempt.

The most common pattern is:

* first try **VCC pass-through**
* if that fails, retry with **deposit**
* or retry with **another card**

{% hint style="info" %}
Hybrid payment is a fallback model.

It is not split payment.
{% endhint %}

### When to use it

Use hybrid payment in these cases:

* VCC pass-through payment fails
* `pay.do` succeeds, but the airline rejects the charge
* the original card is restricted or no longer usable
* you want deposit as a fallback path
* Search, Verify, or Order shows VCC support, but you still need a recovery path

### Fulfillment flow caution

For orders created from `getOfferPrice.do`, every fallback decision must fit inside the 5-minute ticketing window.

Do not wait for delayed manual approval.

Query the order before every retry.

If the original order is cancelled and regeneration is supported, keep the fulfillment-flow identity on the regenerated order.

### Before you start VCC pass-through

Check these points first:

* confirm the fare supports VCC in `VendorFare`
* set `paymentMethod: 3`
* send `supportCreditTransPayment: "1"`
* send complete `creditCard` data
* send full billing address data when the airline requires it
* if the fare or channel does not support VCC, use deposit directly

```json
{
  "orderNo": "XXX",
  "supportCreditTransPayment": "1",
  "paymentMethod": 3,
  "creditCard": {
    "cardNumber": "4111111111111111",
    "cardExpireMonth": "12",
    "cardExpireYear": "2028",
    "cardCVV": "***",
    "cardHolderLastName": "ZHANG",
    "cardHolderFirstName": "SAN",
    "cardHolderCountry": "CN",
    "cardHolderCity": "SHANGHAI",
    "cardHolderPostCode": "200000",
    "cardHolderAddress": "XXX Road"
  }
}
```

### How hybrid payment differs from other cases

#### Hybrid payment vs normal retry

Normal retry keeps the same payment method.

Examples:

* retry the same VCC after a timeout
* retry the same `pay.do` after a network issue

Hybrid payment changes the payment path.

Examples:

* switch from VCC to deposit
* switch from one failed card to another card

#### Hybrid payment vs card change

Changing to another card is a common hybrid case.

If the first VCC fails and the order is still payable, retrying with another VCC still counts as a fallback path.

#### Hybrid payment vs split payment

Hybrid payment does **not** mean:

* split one order amount into two payments
* pay part by card and part by balance
* submit two payment sources in one `pay.do`

If your business case needs amount splitting, handle it with a different solution.

### Decision guide

Follow this order every time:

{% stepper %}
{% step %}
### Check the payment result

Confirm whether `pay.do` failed, or succeeded but later failed at the airline side.
{% endstep %}

{% step %}
### Check whether the original order is still usable

Query the order before any retry.

Only continue on the same order when it is still unpaid and still payable.

In the fulfillment flow, make this decision immediately.
{% endstep %}

{% step %}
### Choose the next payment path

Use the usual priority:

1. retry the original payment path for temporary issues
2. switch to another card
3. switch to deposit
{% endstep %}

{% step %}
### Track the final result

After payment, keep querying the order until ticketing completes or the order reaches a final failure state.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
`pay.do` success does not mean the airline already accepted the payment.

Do not retry before you check the latest order status.
{% endhint %}

### Common payment paths

#### Scenario A: `pay.do` fails

This is the simpler case.

If the order is still unpaid, you can usually:

1. retry the same payment method
2. switch to another card
3. switch to deposit

Use deposit when VCC fails and the same order still supports payment.

```json
{
  "orderNo": "XXX",
  "paymentMethod": 1
}
```

#### Scenario B: `pay.do` succeeds, but airline payment fails

This case needs extra care.

Atlas may accept the request, but the airline can still decline the charge later.

The original order may then be cancelled automatically.

In that case:

1. confirm the final order status
2. wait for the cancellation event if applicable
3. regenerate the order
4. pay the new order with deposit or another supported card

For `getOfferPrice.do` orders, do this only when the recovery path still fits the active fulfillment window.

### Simplified example

This is the most common hybrid payment flow:

1. create the order
2. call `pay.do` with VCC
3. the airline declines the charge
4. the original order is cancelled
5. call `regenerateOrder.do`
6. call `pay.do` on the new order with deposit
7. query the order until ticketing completes

### Regenerate then pay

When the original order is cancelled or no longer payable, create a new order from the original order number.

```json
{
  "originalOrderNo": "{original order no}"
}
```

Then pay the new order:

```json
{
  "orderNo": "{new order no}",
  "paymentMethod": 1
}
```

### Webhook example

If the airline declines the payment and the order is auto-cancelled, use webhook data as an early signal.

```json
{
  "type": "order.cancelled",
  "data": {
    "orderNo": "{canceled order no}",
    "errorCode": "604",
    "errorMessage": "Payment declined by airline"
  }
}
```

### Main risks in VCC pass-through

These issues are common in hybrid payment cases:

* `pay.do` success is not the final business result
* the airline can reject payment after Atlas accepts the request
* card brand or card type mismatch can fail directly
* missing billing address can trigger airline declines
* refunds usually return to the original card, not to deposit
* retries without status checks can cause duplicate charge risk

### ATRIP flow

{% stepper %}
{% step %}
### Find the original order

Open **ATRIP Flight Deck** and go to **My Orders**.

Find the failed order first.
{% endstep %}

{% step %}
### Regenerate the order if needed

Use **Regenerate Order** when the original order was cancelled or can no longer be paid.
{% endstep %}

{% step %}
### Pay with the fallback method

Open the new order and choose **Deposit** or another supported card.
{% endstep %}
{% endstepper %}

If you hit an API integration issue, you can also log in to Eva for support.

### API flow

{% stepper %}
{% step %}
### Query before retry

Check the latest order state before every payment retry.
{% endstep %}

{% step %}
### Decide whether to reuse the order

Reuse the same order only when it is still unpaid and still payable.

If it is cancelled, regenerate first.

When the order came from `getOfferPrice.do`, preserve the fulfillment-flow identity on the regenerated order when the flow supports it.
{% endstep %}

{% step %}
### Retry with a supported method

Retry with the same method for temporary issues.

Switch to deposit or another card when the fallback path is supported.
{% endstep %}
{% endstepper %}

### Best practices

* check supported payment methods before every payment attempt
* confirm VCC support in `VendorFare` before the first VCC payment
* send full card data and billing address when required
* do not reuse a declined or single-use VCC
* do not keep paying the original order after airline decline
* listen for webhook events in auto-cancel cases
* record the original order number, new order number, error code, and switch reason
* reconcile VCC refunds separately from deposit refunds
* keep the original failure reason when you switch to deposit
* avoid fallback paths that depend on slow manual review in the fulfillment flow

### Related pages

* [Payment & Ticketing](./)
* [Fulfillment API](../get-offer-price.md)
* [Payments](../../../../support-and-reference/troubleshooting-and-support/faqs/atlas-api-payments.md)
* [Query Order](../query-order/)
* [Payment Errors](../../../../support-and-reference/troubleshooting-and-support/errors-handing/payment-errors.md)
* [Order Maintenance](../../../post-booking/order-maintenance.md)
* [Regenerate Order](../../../../api-reference/post-booking-apis/regenerate-order.md)
