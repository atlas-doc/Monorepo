---
description: >-
  Step-level guide for the `getOfferPrice.do` fulfillment path, 5-minute
  ticketing, timeout handling, and recovery rules.
---

# Get Offer Price

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when you need the `getOfferPrice.do` fulfillment flow.

This flow is designed for cases where you already know the target order context and need Atlas to complete fast fulfillment under a strict ticketing window.

### FAQ

#### When should I use `getOfferPrice.do`?

Use `getOfferPrice.do` when you need the fulfillment flow with broader display rules and a fast ticketing deadline.

This flow is a fit for urgent ticketing, risky inventory cases, and scenarios that are intentionally excluded from the standard Get Offer display policy.

#### How is this flow different from `getOffers.do`?

`getOfferPrice.do` is a fulfillment-oriented path.

It allows broader offer visibility, uses its own request-limit policy, and applies a 5-minute fulfillment window after order creation.

#### What restrictions are relaxed in this flow?

This flow can return offers that are normally filtered in the standard Get Offer path.

Relaxed rules include:

* near-departure flights
* sold-out-risk scenarios
* round-trip prices that are higher than `OW + OW`

#### What is the payment and ticketing deadline?

Orders created from this flow have a 5-minute payment and ticketing window.

If ticketing is not completed in time, Atlas cancels the order automatically.

### Main API

* `getOfferPrice.do`
* `getLuggage.do`
* `seatAvailability.do`
* `order.do`
* `pay.do`
* `queryOrderDetails.do`

### What is different in this flow

#### Broader offer visibility

This flow can surface inventory that standard `getOffers.do` may hide.

That makes it useful for urgent or harder-to-fulfill scenarios.

#### Separate request governance

`getOfferPrice.do` uses its own QPM policy.

Do not assume it shares the same pool as `verify.do` or `getOffers.do`.

#### Faster operational deadline

The fulfillment window is much shorter than the standard booking hold.

Plan the full chain for immediate payment and active follow-up.

### 5-minute fulfillment rule

Atlas expects the whole fulfillment chain to complete quickly in this flow.

Use these rules:

* create the order only when you are ready to pay
* complete payment without delay
* keep polling until final ticketing or final failure
* stop retrying when the order is already outside the allowed window

{% hint style="warning" %}
Do not treat this flow like the standard order hold flow.

The operational window is 5 minutes, not 30 minutes.
{% endhint %}

### Retry and timeout handling

Check the remaining time before every retry.

As a working rule, only retry when the order is still within the safe 4-minute operating window.

If the order is already close to timeout, avoid another payment retry and query the latest order state first.

If ticketing still does not complete within 5 minutes, Atlas cancels the order automatically.

### Order identity and recovery

Orders created from this flow should keep their fulfillment identity.

If you need to regenerate the order after a supported cancellation path, keep the same fulfillment flow marker on the regenerated order.

Use `regenerateOrder.do` only when the original order is no longer payable and the recovery path supports regeneration.

### Airline scope

The default scope is all airlines.

U2 and 9C are currently excluded from this flow.

They do not reliably meet the 5-minute ticketing requirement.

For U2 and 9C, use the standard booking path instead.

### Typical flow

{% stepper %}
{% step %}
### Get fulfillment offer

Call `getOfferPrice.do` and keep the returned `OfferId`.
{% endstep %}

{% step %}
### Add ancillaries when needed

Query `getLuggage.do` or `seatAvailability.do` before order creation when seat or baggage upsell is part of your product.

Use the returned `OfferId` as the ancillary context in this flow.
{% endstep %}

{% step %}
### Create the order

Call `order.do` with `OfferId` only when payment can start immediately.

Treat order creation as the start of the strict fulfillment window.
{% endstep %}

{% step %}
### Pay the order

Call `pay.do` as soon as the order is ready.

Do not delay payment in this flow.
{% endstep %}

{% step %}
### Follow ticketing to final state

Use `queryOrderDetails.do` until the order is ticketed or cancelled.

Webhook can help, but it should not be your only confirmation path.
{% endstep %}
{% endstepper %}

### Best practice

* connect this flow only to fast payment UX
* keep retry logic conservative
* log the fulfillment flow marker with `orderNo`
* separate monitoring for timeout cancellation and payment failure
* use airline allowlists or blocklists that match the 5-minute SLA

### Related pages

* [Booking Overview](../booking-overview/)
* [Get Offer](get-offer.md)
* [Create Order](create-order.md)
* [Payment & Ticketing](payment-and-ticketing/)
* [Query Order](query-order/)
* [API Request Limits](../booking-overview/api-request-limits.md)
* [Get Offer Price](../../../api-reference/booking-apis/get-offer-price.md)
