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

Use [Standard booking flow](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/o5Zn1hYIBI5mVZ83ihHN) when Atlas is your main shopping layer.

Start with `search.do`.

Then continue with `verify.do` before `order.do`.

Use [Get Offer flow](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/NS7gkZIr0mFD8f0vV1sj) when the itinerary is already known or when you need an independent price check.

Start with `getOffers.do`.

Then continue with `order.do` using `OfferId`.

Use [Fulfillment flow](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/0JojHpwRpiZgp5WlLy01) when you need broader offer visibility and can start payment immediately after order creation.

Start with `getOfferPrice.do`.

Follow the stricter fulfillment timing rules.

Need help choosing between entry paths?

Use [Search vs Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Pcq0icGceiiiaVBThnzx) and [Offer vs Fulfillment](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/hJ5KgpKJEmpzw2hRXmYp).

### Available flows

* [Standard booking flow](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/o5Zn1hYIBI5mVZ83ihHN)
* [Get Offer flow](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/NS7gkZIr0mFD8f0vV1sj)
* [Fulfillment flow](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/0JojHpwRpiZgp5WlLy01)

Each flow page contains the full end-to-end step sequence for that path.

### Need a deeper decision guide?

Use [Booking decisions](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ygfSw8OHHyKfi9HuC7VS) for restart choices, API boundaries, and edge cases.

### Need shared rules across flows?

Use [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3).

### Need one booking step in detail?

Use [Booking step guides](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/7Hivwro5sZdOotzmaEIn).

### Need optional seat or baggage handling?

Use [Optional ancillaries](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Bbuhdlzobxaya4FUurUl).
