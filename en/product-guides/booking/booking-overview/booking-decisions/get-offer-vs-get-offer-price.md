---
description: Choose between the standard Get Offer path and Fulfilment API.
---

# Get Offer vs Fulfilment API

{% include "../../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when you need to choose between `getOffers.do` and `getOfferPrice.do`.

### Short answer

Use `getOffers.do` for the standard independent pricing path.

Use `getOfferPrice.do` for Fulfilment API with broader visibility and a strict 5-minute ticketing window.

Use [Fulfilment API FAQ](../../../../support-and-reference/troubleshooting-and-support/faqs/fulfilment-api-faq.md) when the main question is business fit, coexistence, pricing model, or payment fallback.

### Core difference

#### `getOffers.do`

This is the standard Atlas Get Offer path.

It is best when you need an independent price check before a normal booking flow.

#### `getOfferPrice.do`

This is the entry API for Fulfilment API.

It is best when you need Atlas to accept harder fulfilment scenarios and complete booking under tighter operational timing.

### Ancillary support

Both paths can support optional ancillaries before `order.do`.

Use the returned `OfferId` as the ancillary context in both paths.

The difference is operational timing, not ancillary availability.

### What changes in Fulfilment API

`getOfferPrice.do` can return offers that the standard Get Offer path may not show.

Examples include:

* near-departure flights
* sold-out-risk scenarios
* round-trip prices above `OW + OW`

For near-departure cases, this path is not constrained by the same cache-expiry pressure after request submission.

### Timing difference

#### Standard Get Offer path

The standard booking flow follows normal order timing.

It does not apply the fulfilment-specific 5-minute ticketing rule.

It can still add optional seats or baggage before `order.do`.

#### Fulfilment API

Fulfilment API applies a 5-minute payment and ticketing window.

If ticketing does not finish in time, the order is cancelled automatically.

It can also add optional seats or baggage before `order.do`, but the ancillary step must stay inside the stricter Fulfilment API timing.

### Request-limit difference

#### Standard Get Offer path

`getOffers.do` shares the standard fulfilment limit pool with `verify.do`.

#### Get Offer Price path

`getOfferPrice.do` uses its own request-limit policy.

Do not assume the limit is shared with `verify.do` or `getOffers.do`.

### Recovery difference

#### Standard Get Offer path

Retry decisions usually focus on fresh offer retrieval, stale booking context, or payment-state checks.

#### Fulfilment API

Retry decisions must also respect the remaining Fulfilment API window.

Before every retry, confirm the order is still inside the safe operating window.

### Decision guide

Use `getOffers.do` when:

* Atlas is your price check and booking layer
* you want the standard independent offer flow
* you may want ancillary upsell without fulfilment timing pressure
* normal order timing is acceptable

Use `getOfferPrice.do` when:

* you need optional ancillaries in Fulfilment API
* you need broader display rules
* you need Fulfilment API
* your system can pay immediately and monitor actively

### Business fit

Fulfilment API is often the better choice when you need:

* near-departure ticketing without advance-purchase restriction after request submission
* better multi-passenger price accuracy before ticketing
* Atlas fulfilment on top of your own fare source
* payment fallback between deposit and VCC pass-through

It also works well when you want one fulfilment-oriented interface for automation or AI-agent workflows.

It can also be a good fit when you already have the required order context and want a lighter integration scope than the full standard chain.

{% include "../../../../.gitbook/includes/fulfilment-api-integration-scope.md" %}

### Best practice

Do not switch traffic between these APIs without a business rule.

Treat them as separate product options with different operational behavior.

### Related pages

* [Get Offer](../../booking-step-guides/get-offer.md)
* [Fulfilment API](../../booking-flows/fulfillment-flow.md)
* [Get Offer Price](../../booking-step-guides/get-offer-price.md)
* [Fulfilment API FAQ](../../../../support-and-reference/troubleshooting-and-support/faqs/fulfilment-api-faq.md)
* [Optional ancillaries](../../optional-ancillaries/)
* [Booking Overview](../)
* [API Request Limits](../api-request-limits.md)
