---
description: >-
  End-to-end booking paths for standard shopping, known-itinerary offer lookup,
  and fast fulfillment.
---

# Booking flows

Use this section for end-to-end Atlas API booking flows.

Start here when you need to:

* compare the three booking paths
* decide whether to start with `search.do`, `getOffers.do`, or `getOfferPrice.do`
* match the journey to your payment and ticketing constraints

### Choose the right flow

Use [Standard booking flow](standard-booking-flow.md) when Atlas is your main shopping layer.

Start with `search.do`.

Then continue with `verify.do` before `order.do`.

Use [Get Offer flow](get-offer-flow.md) when the itinerary is already known or when you need an independent price check.

Start with `getOffers.do`.

Then continue with `order.do` using `OfferId`.

Use [Fulfillment flow](fulfillment-flow.md) when you need broader offer visibility and can start payment immediately after order creation.

Start with `getOfferPrice.do`.

Follow the stricter fulfillment timing rules.

Need help choosing between entry paths?

Use [Search vs Offer](../booking-overview/booking-decisions/search-vs-offer.md) and [Offer vs Fulfillment](../booking-overview/booking-decisions/get-offer-vs-get-offer-price.md).

### Available flows

* [Standard booking flow](standard-booking-flow.md)
* [Get Offer flow](get-offer-flow.md)
* [Fulfillment flow](fulfillment-flow.md)

Each flow page contains the full end-to-end step sequence for that path.

### Need a deeper decision guide?

Use [Booking decisions](../booking-overview/booking-decisions/) for restart choices, API boundaries, and edge cases.

### Need shared rules across flows?

Use [Booking Overview](../booking-overview/).

### Need one booking step in detail?

Use [Booking step guides](../booking-step-guides/).

### Need optional seat or baggage handling?

Use [Optional ancillaries](../optional-ancillaries/).
