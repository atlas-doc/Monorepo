---
description: >-
  Atlas API search flow overview for flight offers, Get Offer, smart search, and
  downstream identifier handling.
---

# Search

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page to start the booking flow.

{% hint style="warning" %}
`Smart Search` (`smartSearch.do`) will be deprecated soon.

Do not use it for new integrations. Prefer the standard `search.do` flow.
{% endhint %}

Start here when you need to:

* begin the standard booking flow
* choose between `search.do` and `getOffers.do`
* understand which identifier to keep for the next step

### FAQ

#### When should I use `search.do`?

Use `search.do` when Atlas is your main shopping entry point.

Keep the returned `routingIdentifier` for `verify.do`.

#### When should I use `getOffers.do` instead?

Use `getOffers.do` when you already know the target itinerary or need an independent price check.

Keep the returned `OfferId` for the order flow.

#### What request limit applies to `search.do`?

`search.do` uses `10 QPS` by default.

Over-limit requests return Atlas error code `429`.

Honor the returned `retryAfter` value before retrying.

### Search request limits

Atlas counts `search.do` in a rolling 1-second window.

Use `10 QPS` as the default limit unless Atlas configured a different tier for your account.

#### What counts

These requests count:

* successful searches
* no-result searches
* business failures, airline failures, and cache-hit responses

These requests do not count:

* requests rejected by request-limit governance
* authentication, permission, or validation failures

#### How to avoid `429`

Use local cache when possible.

Collapse duplicate searches.

Back off with the returned `retryAfter` value before retrying.

### What this page covers

* Standard offer search
* Independent Get Offer lookup
* Advanced or smart search flows
* Offer polling and request follow-up

### Main APIs

* `search.do`
* `getOffers.do`
* `smartSearch.do`

### Key outputs

* `routingIdentifier` for standard verify flow
* `OfferId` for Get Offer order flow
* `requestId` for smart search follow-up
* Offer data for downstream selection

### Which identifier should you keep?

Keep the identifier that matches the flow:

* `routingIdentifier` for the standard search → verify flow
* `OfferId` for the Get Offer → order flow
* `requestId` only for smart search follow-up

Do not mix identifiers across flows.

### Use this when you need

* A standard search-to-book flow
* An independent offer lookup without standard search
* Smart or asynchronous search behavior
* Offer refresh after smart search

### What comes next?

#### Standard flow

Call [Verify](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm) with `routingIdentifier`.

#### Get Offer flow

Continue with [Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FSGess6buGE1P02WnVNu) and then create the order with `OfferId`.

#### Smart search flow

Use the smart search follow-up only for existing implementations.

### Related pages

* [Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FSGess6buGE1P02WnVNu)
* [Verify](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm)
* [Sandbox Access](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/O9n7Z0tHowy0I3hOF44f)
* [Booking APIs](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/beDx3cjbYPiOQ1Pwk6bC)

### Full API reference

See endpoint-level details here:

* [Search](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/lqBleuC7HEsPku6mncSh)
* [Smart Search](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jU5sjhTD1WPTM2EU260v)
* [Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/rzWbUXxEiy9glqM2Zv3J)
