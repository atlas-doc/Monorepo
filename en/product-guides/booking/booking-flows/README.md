---
description: >-
  End-to-end booking paths for standard shopping, known-itinerary offer lookup,
  and Fulfilment API.
---

# Booking paths

Use this section for end-to-end Atlas API booking paths.

{% hint style="warning" %}
**🆕 Featured new path:** Use [🆕 Fulfilment API](fulfillment-flow.md) when you start with `getOfferPrice.do` and can begin payment immediately after order creation.
{% endhint %}

Start here when you need to:

* compare the three booking paths
* decide whether to start with `search.do`, `getOffers.do`, or `getOfferPrice.do`
* match the journey to your payment and ticketing constraints

### Choose the right path

Use [🆕 Fulfilment API](fulfillment-flow.md) when you need broader offer visibility and can start payment immediately after order creation.

Start with `getOfferPrice.do`.

Follow the stricter Fulfilment API timing rules.

Use [Standard booking](standard-booking-flow.md) when Atlas is your main shopping layer.

Start with `search.do`.

Then continue with `verify.do` before `order.do`.

Use [Get Offer](get-offer-flow.md) when the itinerary is already known or when you need an independent price check.

Start with `getOffers.do`.

Then continue with `order.do` using `OfferId`.

Need help choosing between entry paths?

Use [Search vs Offer](../booking-overview/booking-decisions/search-vs-offer.md) and [Get Offer vs Fulfilment API](../booking-overview/booking-decisions/get-offer-vs-get-offer-price.md).

### Available paths

* [🆕 Fulfilment API](fulfillment-flow.md)
* [Standard booking](standard-booking-flow.md)
* [Get Offer](get-offer-flow.md)

Each path page contains the full end-to-end step sequence for that path.

### Need a deeper decision guide?

Use [Booking decisions](../booking-overview/booking-decisions/) for restart choices, API boundaries, and edge cases.

### Need shared rules across paths?

Use [Booking Overview](../booking-overview/).

### Need one booking step in detail?

Use [Booking steps](../booking-step-guides/).

### Need optional seat or baggage handling?

Use [Optional ancillaries](../optional-ancillaries/).
