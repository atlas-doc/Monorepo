---
description: Choose between the standard Get Offer path and the Get Offer Price path.
---

# Get Offer vs Get Offer Price

{% include "../../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when you need to choose between `getOffers.do` and `getOfferPrice.do`.

### Short answer

Use `getOffers.do` for the standard independent pricing path.

Use `getOfferPrice.do` for the Get Offer Price path with broader visibility and a strict 5-minute ticketing window.

### Core difference

#### `getOffers.do`

This is the standard Atlas Get Offer path.

It is best when you need an independent price check before a normal booking flow.

#### `getOfferPrice.do`

This is the Get Offer Price path.

It is best when you need Atlas to accept harder fulfillment scenarios and complete booking under tighter operational timing.

### Ancillary support

Both paths can support optional ancillaries before `order.do`.

Use the returned `OfferId` as the ancillary context in both paths.

The difference is operational timing, not ancillary availability.

### What changes in the Get Offer Price path

`getOfferPrice.do` can return offers that the standard Get Offer path may not show.

Examples include:

* near-departure flights
* sold-out-risk scenarios
* round-trip prices above `OW + OW`

### Timing difference

#### Standard Get Offer path

The standard booking flow follows normal order timing.

It does not apply the fulfillment-specific 5-minute ticketing rule.

It can still add optional seats or baggage before `order.do`.

#### Get Offer Price path

The Get Offer Price path applies a 5-minute payment and ticketing window.

If ticketing does not finish in time, the order is cancelled automatically.

It can also add optional seats or baggage before `order.do`, but the ancillary step must stay inside the stricter fulfillment timing.

### Request-limit difference

#### Standard Get Offer path

`getOffers.do` shares the standard fulfillment limit pool with `verify.do`.

#### Get Offer Price path

`getOfferPrice.do` uses its own request-limit policy.

Do not assume the limit is shared with `verify.do` or `getOffers.do`.

### Recovery difference

#### Standard Get Offer path

Retry decisions usually focus on fresh offer retrieval, stale booking context, or payment-state checks.

#### Get Offer Price path

Retry decisions must also respect the remaining Get Offer Price window.

Before every retry, confirm the order is still inside the safe operating window.

### Decision guide

Use `getOffers.do` when:

* Atlas is your price check and booking layer
* you want the standard independent offer flow
* you may want ancillary upsell without fulfillment timing pressure
* normal order timing is acceptable

Use `getOfferPrice.do` when:

* you need optional ancillaries with the fulfillment path
* you need broader display rules
* you need a fast fulfillment path
* your system can pay immediately and monitor actively

### Best practice

Do not switch traffic between these APIs without a business rule.

Treat them as separate product paths with different operational behavior.

### Related pages

* [Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FSGess6buGE1P02WnVNu)
* [Get Offer Price](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/e7tapaArEz0MBOv62dxZ)
* [Optional ancillaries](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Bbuhdlzobxaya4FUurUl)
* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [API Request Limits](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV)
