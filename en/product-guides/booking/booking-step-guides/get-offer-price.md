---
description: >-
  Step guide for `getOfferPrice.do` in the Fulfilment API path, including
  broader offer scope, 5-minute ticketing impact, and handoff to order creation.
---

# Get Offer Price

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when you need `getOfferPrice.do` behavior, timing, and recovery rules in Fulfilment API.

Start with [Fulfilment API](../booking-flows/fulfillment-flow.md) when you need the full end-to-end booking sequence.

This page covers the Fulfilment API entry step only.

It does not replace the full Fulfilment API path.

Use [Fulfilment API FAQ](../../../support-and-reference/troubleshooting-and-support/faqs/fulfilment-api-faq.md) when the main question is product fit, coexistence with existing interfaces, pricing model, or airline coverage.

Use this step when you already know the target order context and need Atlas to start a fast fulfilment chain under a strict ticketing window.

### FAQ

#### When should I use `getOfferPrice.do`?

Use `getOfferPrice.do` when you need broader display rules and a fast ticketing deadline.

This step is a fit for urgent ticketing, risky inventory cases, and scenarios that are intentionally excluded from the standard Get Offer display policy.

#### How is `getOfferPrice.do` different from `getOffers.do`?

`getOfferPrice.do` is the core entry API for Fulfilment API.

It allows broader offer visibility, uses its own request-limit policy, and applies a 5-minute fulfilment window after order creation.

#### Can I use `getOfferPrice.do` alongside existing Atlas interfaces?

Yes.

Fulfilment API is an additional fulfilment channel.

Use it in parallel with the standard flow when different business scenarios need different booking paths.

#### What restrictions are relaxed in this step?

This step can return offers that are normally filtered in the standard Get Offer path.

Relaxed rules include:

* near-departure flights
* sold-out-risk scenarios
* round-trip prices that are higher than `OW + OW`

For near-departure cases, this path is not constrained by the same cache-expiry pressure after request submission.

#### What downstream deadline does this step trigger?

Orders created through Fulfilment API have a 5-minute payment and ticketing window.

If ticketing is not completed in time, Atlas cancels the order automatically.

### Main API

* `getOfferPrice.do`

### Downstream APIs in this path

After `getOfferPrice.do`, the usual Fulfilment API chain continues with:

* `getLuggage.do`
* `seatAvailability.do`
* `order.do`
* `pay.do`
* `queryOrderDetails.do`

### What `getOfferPrice.do` changes

#### Broader offer visibility

`getOfferPrice.do` can surface inventory that standard `getOffers.do` may hide.

That makes it useful for urgent or harder-to-fulfil scenarios.

#### Separate request governance

`getOfferPrice.do` uses its own QPM policy.

Do not assume it shares the same pool as `verify.do` or `getOffers.do`.

#### Faster operational deadline

This step leads into an operating window that is much shorter than the standard booking hold.

Plan the full chain for immediate payment and active follow-up.

#### Different integration scope

This is one entry interface within Fulfilment API, not the full standard shopping chain.

{% include "../../../.gitbook/includes/fulfilment-api-integration-scope.md" %}

### 5-minute Fulfilment API rule

Atlas expects the whole Fulfilment API chain to complete quickly.

Use these rules:

* create the order only when you are ready to pay
* complete payment without delay
* keep polling until final ticketing or final failure
* stop retrying when the order is already outside the allowed window

{% hint style="warning" %}
Do not treat Fulfilment API like the standard order hold flow.

The operational window is 5 minutes, not 30 minutes.
{% endhint %}

### Retry and timeout handling

Check the remaining time before every retry.

As a working rule, only retry when the order is still within the safe 4-minute operating window.

If the order is already close to timeout, avoid another payment retry and query the latest order state first.

If ticketing still does not complete within 5 minutes, Atlas cancels the order automatically.

### Order identity and recovery

Orders created through Fulfilment API should keep their Fulfilment API identity.

If you need to regenerate the order after a supported cancellation path, keep the same Fulfilment API marker on the regenerated order.

Use `regenerateOrder.do` only when the original order is no longer payable and the recovery path supports regeneration.

### Airline scope

The default scope is all airlines.

U2 and 9C are currently excluded from Fulfilment API.

They do not reliably meet the 5-minute ticketing requirement.

For U2 and 9C, use the standard booking path instead.

Outside those exclusions, Fulfilment API is powered by Atlas's 100+ direct official airline connections and continues to expand.

### Where this step sits in the full path

{% stepper %}
{% step %}
### Get the offer

Call `getOfferPrice.do` and keep the returned `OfferId`.
{% endstep %}

{% step %}
### Add ancillaries when needed

Query `getLuggage.do` or `seatAvailability.do` before order creation when seat or baggage upsell is part of your product.

Use the returned `OfferId` as the ancillary context in Fulfilment API.
{% endstep %}

{% step %}
### Create the order

Call `order.do` with `OfferId` only when payment can start immediately.

Treat order creation as the start of the strict Fulfilment API window.
{% endstep %}

{% step %}
### Pay the order

Call `pay.do` as soon as the order is ready.

Do not delay payment in Fulfilment API.
{% endstep %}

{% step %}
### Follow ticketing to final state

Use `queryOrderDetails.do` until the order is ticketed or cancelled.

Webhook can help, but it should not be your only confirmation path.
{% endstep %}
{% endstepper %}

### Best practice

* connect Fulfilment API only to fast payment UX
* keep retry logic conservative
* log the Fulfilment API marker with `orderNo`
* separate monitoring for timeout cancellation and payment failure
* use airline allowlists or blocklists that match the 5-minute SLA

### Failure alert timing

{% include "../../../.gitbook/includes/fulfilment-api-failure-alert-timing.md" %}

### Related pages

* [Fulfilment API](../booking-flows/fulfillment-flow.md)
* [Fulfilment API FAQ](../../../support-and-reference/troubleshooting-and-support/faqs/fulfilment-api-faq.md)
* [Booking Overview](../booking-overview/)
* [Get Offer](get-offer.md)
* [Create Order](create-order.md)
* [Payment & Ticketing](payment-and-ticketing/)
* [Query Order](query-order/)
* [API Request Limits](../booking-overview/api-request-limits.md)
* [Get Offer Price](../../../api-reference/booking-apis/get-offer-price.md)
