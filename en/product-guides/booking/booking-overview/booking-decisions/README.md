---
description: >-
  Atlas API booking decision guides for choosing a flow, restart point, and the
  correct next API step.
---

# Booking decisions

{% include "../../../../.gitbook/includes/eva-help-hint.md" %}

Use this section when you need to choose the right booking path or decide which step to repeat.

This section helps you:

* choose between search, offer, and fulfillment paths
* decide which API owns a booking action
* restart from the safest point after delay or failure
* avoid mixing identifiers across flows

### Short answer

Use these pages when the question is not how to call an API, but which path to use.

If the problem is flow choice, restart scope, or API boundary, start here.

### When to use this section

Use this section when:

* you are deciding between `search.do` and `getOffers.do`
* you are deciding between `getOffers.do` and `getOfferPrice.do`
* you are unsure whether to restart from search, verify, or offer retrieval
* you are unsure whether a problem belongs to `verify.do` or `order.do`

### Reading order

#### Choose the booking entry path

Start with [Search vs Offer](search-vs-offer.md).

Use it when you need to decide whether Atlas is your shopping layer or your pricing and booking layer.

#### Choose the offer path

Then use [Get Offer vs Get Offer Price](get-offer-vs-get-offer-price.md).

Use it when you already need an offer-based path and must choose between normal offer retrieval and fast fulfillment.

#### Decide where to restart

Use [Restart point](restart-point.md).

Use it when identifiers expired, pricing drifted, or booking was delayed.

#### Decide which API owns the problem

Use [Verify vs Order](verify-vs-order.md).

Use it when you need to separate validation from booking creation.

### Pages in this section

* [Search vs Offer](search-vs-offer.md)
* [Restart point](restart-point.md)
* [Get Offer vs Get Offer Price](get-offer-vs-get-offer-price.md)
* [Verify vs Order](verify-vs-order.md)

### Quick decision rules

#### When should you use `search.do`?

Use it when Atlas is the main shopping entry point.

The standard next step is `verify.do`.

#### When should you use `getOffers.do`?

Use it when the target itinerary is already known or when you need an independent price check.

The standard next step is `order.do` with `OfferId`.

Optional ancillaries can be added before `order.do`.

#### When should you use `getOfferPrice.do`?

Use it when you need the fulfillment path with broader display rules and immediate payment readiness.

Do not use it when normal booking timing is enough.

Optional ancillaries can also be added before `order.do`, but they must fit the stricter fulfillment window.

#### When should you restart from an earlier step?

Restart when the identifier is stale, the itinerary changed, the fare drifted, or booking was delayed long enough to make the old context unreliable.

### Common risks

#### Mixing identifiers across flows

Do not use `routingIdentifier`, `sessionId`, and `OfferId` interchangeably.

Each one belongs to a specific booking path and step.

#### Restarting from the wrong step

Retrying too late in the flow can cause stale price, stale ancillary, or expired-session failures.

Restart from the earliest step that restores a safe booking context.

#### Using fulfillment rules in the normal offer flow

Do not assume `getOffers.do` and `getOfferPrice.do` have the same timing and recovery model.

They are separate product paths.

Do not assume ancillary support is the difference.

The real difference is timing, display scope, and operational recovery.

### Recommended next pages by task

#### Choose the right booking path

Use:

* [Search vs Offer](search-vs-offer.md)
* [Get Offer vs Get Offer Price](get-offer-vs-get-offer-price.md)
* [Booking Overview](../)

#### Decide what to retry

Use:

* [Restart point](restart-point.md)
* [Identifiers](../identifiers.md)
* [Error Codes](../../../../support-and-reference/troubleshooting-and-support/errors-handing/)

#### Decide whether the issue belongs to verify or order

Use:

* [Verify vs Order](verify-vs-order.md)
* [Verify](../../booking-step-guides/verify.md)
* [Create Order](../../booking-step-guides/create-order.md)

### Related pages

* [Booking Overview](../)
* [Identifiers](../identifiers.md)
* [API Request Limits](../api-request-limits.md)
* [Error Codes](../../../../support-and-reference/troubleshooting-and-support/errors-handing/)
