---
description: >-
  Common Fulfilment API questions about fit, coexistence with existing
  interfaces, pricing, payment paths, alerts, and airline coverage.
---

# Fulfilment API FAQ

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page for common Fulfilment API questions from commercial evaluation through integration planning.

Start here when you need to:

* decide whether Fulfilment API fits your booking model
* understand how it works with existing Atlas interfaces
* explain pricing, payment paths, and failure handling to internal teams

### Short answer

Fulfilment API does not replace the standard Atlas booking flow.

It adds an independent fulfilment path for partners who already hold an order or fare and want Atlas to complete verification and ticketing.

You can run it in parallel with existing Atlas interfaces.

### When to evaluate Fulfilment API

Evaluate Fulfilment API when any of these apply:

* you need last-minute ticketing without cache-expiry pressure
* you handle multi-passenger bookings and want better price accuracy before ticketing
* you already have your own fare source and only need Atlas fulfilment
* you need payment fallback between deposit and VCC pass-through
* you want a simpler ticketing integration than the full `search.do` → `verify.do` → `order.do` chain

### Fulfilment API vs. Existing Interfaces — One Table, Full Clarity

Fulfilment API does not replace existing Atlas interfaces.

It adds an independent fulfilment path on top of the standard booking flow.

| Dimension                        | Existing interfaces (`search.do` / `verify.do` / `order.do`)  | Fulfilment API                                                     |
| -------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------ |
| Prerequisite                     | Must first obtain fare through Atlas shopping flow            | You already hold the fare or order context and pass it in directly |
| Fare source                      | Must come from Atlas fare context                             | Can come from Atlas or your own fare source                        |
| Last-minute ticketing            | Limited by cache-expiry pressure                              | No advance-purchase restriction after request submission           |
| Multi-passenger pricing accuracy | Cache-dependent with higher price-change risk                 | Real-time verification improves accuracy before ticketing          |
| VCC rebate / airline commission  | Usually handled separately in commercial calculation          | Can be reflected directly in the quoted net price                  |
| Payment methods                  | Deposit                                                       | Deposit and VCC pass-through                                       |
| System failure after submission  | Your own booking orchestration can be interrupted             | Atlas continues fulfilment after the request is accepted           |
| Integration effort               | Full `search.do` → `verify.do` → `order.do` chain is required | Independent interface with roughly 1-hour integration scope        |
| Pricing model                    | Follows the standard commercial model                         | Usage-based transaction fee model                                  |
| Can run in parallel              | Yes                                                           | Yes                                                                |

#### What stays the same

Existing `search.do`, `verify.do`, `order.do`, and related flows continue to work normally.

Fulfilment API is an additional product path.

#### What changes

Fulfilment API starts from `getOfferPrice.do`.

It is designed for cases where you already know the target order context and need Atlas to complete fulfilment fast.

It also applies a strict 5-minute payment and ticketing window after order creation.

#### Why teams choose it

Teams usually choose Fulfilment API for one or more of these reasons:

* better support for near-departure ticketing
* real-time fare verification before ticketing
* bring-your-own-fare fulfilment with Atlas ticketing capability
* dual payment paths through deposit and VCC pass-through
* lower integration effort for ticketing-only scenarios

### FAQ

#### I already use Atlas existing interfaces. Do I also need Fulfilment API?

No.

It is optional.

Use it when your business has a gap that the standard flow does not solve well.

Typical triggers include last-minute ticketing, multi-passenger price drift, self-sourced fares, or stronger fault-tolerance needs.

#### Will Fulfilment API replace `search.do`, `verify.do`, and `order.do`?

No.

Fulfilment API is a separate fulfilment channel.

Use the standard flow when Atlas is your main shopping and booking layer.

Use Fulfilment API when you already hold the fare or order context and need Atlas to complete verification and ticketing.

#### Can I use existing interfaces and Fulfilment API in parallel?

Yes.

They are fully compatible.

Many partners keep the standard flow for Atlas-sourced shopping and use Fulfilment API for independent fulfilment scenarios.

#### When is Fulfilment API a better fit than the standard flow?

It is usually a better fit when you need:

* last-minute ticketing
* higher multi-passenger pricing accuracy before ticketing
* Atlas ticketing on top of your own fare source
* payment fallback between deposit and VCC pass-through
* fulfilment that keeps running after your request is submitted

#### Why is Fulfilment API better for last-minute ticketing?

The standard flow depends more on cached pricing context.

Fulfilment API performs real-time fare verification closer to fulfilment.

That removes the standard cache-expiry pressure after request submission.

It makes Fulfilment API better suited to near-departure booking scenarios without advance-purchase restriction after request submission.

#### Why is Fulfilment API better for multi-passenger bookings?

Multi-passenger bookings are more exposed to price drift.

Fulfilment API verifies the fare again before ticketing.

That reduces the risk of late price change compared with cache-dependent flows.

#### Can I bring my own fare source?

Yes.

Fulfilment API supports partners that already source fares outside Atlas.

Use it when you want Atlas fulfilment and ticketing capability without moving your shopping layer into Atlas.

#### What payment methods does Fulfilment API support?

{% include "../../../.gitbook/includes/fulfilment-api-dual-payment-paths.md" %}

#### What happens if my own system fails after I submit the request?

After the fulfilment request is accepted, Atlas continues the fulfilment process on the Atlas side.

Later partner-side instability does not stop the already submitted fulfilment task from progressing.

You should still monitor the final order state through order query or webhook.

#### Is the pricing model usage-based?

Yes.

Fulfilment API uses a per-booking transaction fee model.

Pricing is usage-based and can scale by usage tier.

You only pay for successful usage.

#### What does the 1-hour integration claim mean in practice?

It means the integration scope is much smaller than the standard full-chain flow.

You do not need to rebuild search, verify, and order orchestration from scratch.

At a high level, you:

1. send the existing fare or order context in the required request format
2. handle the fare verification result
3. handle the ticketing result or failure follow-up

{% include "../../../.gitbook/includes/fulfilment-api-integration-scope.md" %}

#### Why can Fulfilment API pricing be more competitive?

Fulfilment API pricing can include rebates directly in the net price.

That can reduce separate rebate calculation work for VCC rebate and airline commission scenarios.

The exact commercial result still depends on your contracted pricing model.

#### What happens if ticketing fails?

Fulfilment API supports failure alerting and fast diagnosis.

When ticketing fails, the failure message identifies the main cause category so your team can act faster.

Use order query as the source of truth for the final state.

#### How fast are failure alerts sent?

{% include "../../../.gitbook/includes/fulfilment-api-failure-alert-timing.md" %}

Use the SLA agreed for your account when you need a contractual commitment.

#### Which airlines does Fulfilment API support?

Fulfilment API is powered by Atlas's 100+ direct official airline connections and continues to expand.

Coverage is broadly aligned with existing Atlas airline fulfilment capability.

If airline scope is a launch blocker, confirm the exact airline list during solution review.

#### Is Fulfilment API useful for AI-agent workflows?

Yes.

It gives AI-agent systems one fulfilment-oriented interface instead of separate airline-specific ticketing rules.

That reduces orchestration complexity when your automation layer needs standard status handling and error management.

### Related pages

* [Fulfilment API](../../../product-guides/booking/booking-flows/fulfillment-flow.md)
* [Get Offer Price](../../../product-guides/booking/booking-step-guides/get-offer-price.md)
* [Get Offer vs Fulfilment API](../../../product-guides/booking/booking-overview/booking-decisions/get-offer-vs-get-offer-price.md)
* [Orders & Ticketing](atlas-api-order.md)
* [Payment & Ticketing](../../../product-guides/booking/booking-step-guides/payment-and-ticketing/)
