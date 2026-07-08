---
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Price Compare Search

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this API for pre-sale route coverage and raw price discovery.

It is not a standard booking step.

{% hint style="warning" %}
`priceCompareSearch.do` is only available to pre-sale customers.

The default usage quota is 1,000 calls per day.

Do not treat the returned price as a production booking price.
{% endhint %}

### What this API does

* returns raw prices with maximum route coverage
* skips booking-rule filtering
* ignores supplier operational switches
* checks Atlas cache first, then falls back to live airline pricing

### Request compatibility

The request body is fully compatible with `search.do`.

No extra request fields are required.

Use the same core fields:

* `tripType`, `adultNum`, `childNum`, `infantNum`
* `fromCity`, `toCity`, `fromDate`, `retDate`
* `airlines`, `currency`, `includeMultipleFareFamily`

### How to read the response

#### When results exist

The API returns `status: 0`, `msg: "success"`, and a non-empty `routings` array.

The `routings` structure matches `search.do`.

#### When no results exist

No results still return `status: 0`.

This is a normal business outcome.

Check both:

* `routings.length`
* `noResultReason.code`

Do not rely on `status` alone.

### `noResultReason`

When `routings` is empty, the response may include `noResultReason`.

It contains:

* `code` — machine-readable reason
* `message` — human-readable detail
* `recentFlightDates` — optional nearby dates with actual flight schedules

#### Reason codes

**`ROUTE_NOT_SUPPORTED`**

The route is outside Atlas coverage.

Do not retry the same route.

**`AIRLINE_NO_FLIGHT`**

The airline returned no flight info for that route and date.

Check `recentFlightDates` and retry with another supported date.

**`FLIGHT_SOLD_OUT`**

The flight exists, but no seats are available.

Check `recentFlightDates` and retry with another date.

**`PRICE_FETCH_FAILED`**

Atlas could not fetch a price from the airline.

Treat this as a temporary technical failure.

Retry later.

### How `recentFlightDates` works

`recentFlightDates` returns up to 7 actual scheduled dates around the searched date.

The window targets 3 days before and 3 days after.

If earlier dates are unavailable, later dates fill the gap.

The list only includes dates with real flight schedules.

### API-level errors

`status != 0` means the request failed at API level.

Common values include:

* `100`, `101`, `102` — missing or invalid request data
* `109` — search limit exceeded
* `110` — QPS limit exceeded
* `112` — request timeout
* `900` — unauthorized
* `9999` — internal error

### Integration guidance

Use this API when you want to evaluate Atlas route coverage before production integration.

Use the standard booking flow when you need a bookable path.

See [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3) for the normal search-to-ticket flow.

{% openapi-operation spec="atlas-api" path="/priceCompareSearch.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/6d498c79f43546e63a2289f81c033345c8210830410d2835d33def093c5f3f29.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260708%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260708T131020Z&X-Amz-Expires=172800&X-Amz-Signature=27126ae21ba6c52dbf38f05311990817f1e9c7b7109d7807e10d2e1b9238185d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
