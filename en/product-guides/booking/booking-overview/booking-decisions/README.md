---
description: Choose the right booking flow, restart point, or API step.
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

Start with [Search vs Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Pcq0icGceiiiaVBThnzx).

Use it when you need to decide whether Atlas is your shopping layer or your pricing and booking layer.

#### Choose the offer path

Then use [Get Offer vs Get Offer Price](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/hJ5KgpKJEmpzw2hRXmYp).

Use it when you already need an offer-based path and must choose between normal offer retrieval and fast fulfillment.

#### Decide where to restart

Use [Restart point](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ZxJaikDjWinutACjHNEw).

Use it when identifiers expired, pricing drifted, or booking was delayed.

#### Decide which API owns the problem

Use [Verify vs Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2hu9DU8aIIGLGqeathgL).

Use it when you need to separate validation from booking creation.

### Pages in this section

* [Search vs Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Pcq0icGceiiiaVBThnzx)
* [Restart point](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ZxJaikDjWinutACjHNEw)
* [Get Offer vs Get Offer Price](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/hJ5KgpKJEmpzw2hRXmYp)
* [Verify vs Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2hu9DU8aIIGLGqeathgL)

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

* [Search vs Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Pcq0icGceiiiaVBThnzx)
* [Get Offer vs Get Offer Price](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/hJ5KgpKJEmpzw2hRXmYp)
* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)

#### Decide what to retry

Use:

* [Restart point](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ZxJaikDjWinutACjHNEw)
* [Identifiers](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ns5eKoKIPFUTFhjJkPyC)
* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)

#### Decide whether the issue belongs to verify or order

Use:

* [Verify vs Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2hu9DU8aIIGLGqeathgL)
* [Verify](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm)
* [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE)

### Related pages

* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [Identifiers](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ns5eKoKIPFUTFhjJkPyC)
* [API Request Limits](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV)
* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)
