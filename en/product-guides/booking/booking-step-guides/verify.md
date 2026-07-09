---
description: >-
  Atlas API verify flow for fare recheck, booking requirements, ancillary
  options, and session handling before order creation.
---

# Verify

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page after offer selection.

{% hint style="info" %}
Use `bookingRequirement` from the verify response as the source of truth for booking input.

It tells you which passenger and document fields are required for `order.do`.
{% endhint %}

Start here when you need to:

* recheck fare and routing before booking
* get the required passenger and document fields
* create a fresh `sessionId` for `order.do`
* keep a valid `sessionId` for `seatAvailability.do`

### FAQ

#### When should I call `verify.do`?

Call `verify.do` after `search.do` and before `order.do`.

Use it to refresh fare, routing, and booking requirements close to booking time.

Use a `routingIdentifier` that is no more than 6 hours old.

#### What should I read from the verify response?

Read `sessionId`, latest fare details, ancillary options, and `bookingRequirement`.

Treat `bookingRequirement` as the source of truth for the order request.

#### What request limit applies to `verify.do`?

`verify.do` shares one `60 QPM` fulfillment pool with `getOffers.do`.

Over-limit requests return `HTTP 429 Too Many Requests`.

Honor the returned `retryAfter` value before retrying.

### Fulfillment request limits

Atlas counts `verify.do` and `getOffers.do` together in a rolling 60-second window.

The default shared limit is `60 QPM`.

One busy API can consume the shared pool for the other.

#### What counts

These requests count:

* successful responses
* no-result responses
* business failures, airline failures, and cache-hit responses

#### How to reduce limit pressure

Do not re-verify unchanged itineraries in tight loops.

Reuse the current `sessionId` while it is still valid.

Honor `retryAfter` when `429` is returned.

### Main API

* `verify.do`

### Inputs

* `routingIdentifier` from search, valid for up to 6 hours

### Key outputs

* `sessionId` for order creation and seat lookup, valid for up to 2 hours
* Latest fare and routing details
* `bookingRequirement` for required passenger and document fields
* Ancillary options

### What should you keep from verify?

Keep:

* `sessionId` for `order.do`
* `sessionId` for `seatAvailability.do` when seat selection is needed before booking
* `bookingRequirement` for required input fields
* current ancillary options when baggage or seats matter before booking

Use `sessionId` within 2 hours.

Do not reuse an expired `sessionId`.

If your seat request arrives later from an upstream system, keep enough itinerary linkage to match that request back to the current `sessionId`.

### Use this when you need

* Fare recheck before booking
* Final validation of routing details
* Required passenger and document rules for `order.do`

### What comes next?

Use [Create Order](create-order.md) with the returned `sessionId`.

If price, inventory, or ancillaries changed, use the verify result as the current source of truth.

### Related pages

* [Search](search.md)
* [Create Order](create-order.md)
* [Booking APIs](../../../api-reference/booking-apis/)

### Full API reference

See endpoint-level details here:

* [Verify](../../../api-reference/booking-apis/verify.md)
