---
description: >-
  Atlas API QPS and QPM request-limit rules for selected pre-booking APIs,
  including shared pools, 429 handling, and retry guidance.
---

# API Request Limits

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when you need the request-limit rules in one place.

Atlas applies request-limit governance to selected pre-booking APIs.

Over-limit requests return Atlas error code `429`.

### Affected APIs

These APIs are covered by this policy:

* `search.do`
* `verify.do`
* `getOffers.do`
* `seatAvailability.do`
* `getLuggage.do`

These APIs are not covered by this policy:

* `order.do`
* `pay.do`

### Default limits

#### Search resource

* `search.do` — `10 QPS`

Atlas counts Search in a rolling 1-second window.

#### Fulfilment resource

* `verify.do` + `getOffers.do` — shared `60 QPM`

Atlas counts Fulfilment in a rolling 60-second window.

#### Ancillary resource

* `seatAvailability.do` + `getLuggage.do` — shared `60 QPM`

Atlas counts Ancillary in a rolling 60-second window.

### Shared-pool rules

`verify.do` and `getOffers.do` share one fulfilment pool.

Heavy traffic on one API can consume the pool for the other.

`seatAvailability.do` and `getLuggage.do` share one ancillary pool.

Heavy traffic on one API can consume the pool for the other.

### What counts toward the limit

These requests count:

* successful requests
* no-result requests
* business failures and airline failures
* cache-hit responses

These requests do not count:

* requests already rejected by request-limit governance
* authentication failures
* parameter validation failures
* permission or security-policy rejections
* idempotency-blocked duplicates that never enter business processing

### `429` response

When a request exceeds the active limit, Atlas returns error code `429`.

#### Response sample

```json
{
  "code": 429,
  "message": "Rate limit exceeded. Please retry after the current window resets",
  "limitType": "SEARCH_QPS",
  "limit": 1,
  "retryAfter": 1
}
```

#### Field meanings

* `code` — error code
* `message` — error summary
* `limitType` — active limit bucket
* `limit` — current configured limit
* `retryAfter` — wait time in seconds before retry

### How to handle 429

Reduce request frequency.

Wait for `retryAfter` before retrying.

Do not retry immediately in parallel.

Use cache where possible.

Collapse duplicate requests before they reach Atlas.

### Practical guidance by API

#### Search

Use local cache for repeated route and date lookups.

Smooth burst traffic across each second.

#### Verify and Get Offer

Do not recheck the same itinerary in tight loops.

Reuse fresh verification or offer context when booking conditions did not change.

#### Seats and Baggage

Do not requery ancillaries unless the booking context changed.

Reuse the current `sessionId` or `OfferId` while it is still valid.

### FAQ

#### Does `429` mean the account is banned?

No.

It only means the current request frequency exceeded the configured limit.

#### Do cache-hit requests count?

Yes.

If the request enters Atlas business processing and returns a result, it counts.

#### Can higher limits be requested?

Yes.

If your business needs higher throughput, contact your Atlas account manager or business team.

### Related pages

* [Booking Overview](./)
* [Error Codes](../../../support-and-reference/troubleshooting-and-support/errors-handing/)
* [Search](../booking-step-guides/search.md)
* [Get Offer](../booking-step-guides/get-offer.md)
* [Verify](../booking-step-guides/verify.md)
* [Seats](../optional-ancillaries/seats-and-baggage/)
* [Baggage](../optional-ancillaries/baggage.md)
