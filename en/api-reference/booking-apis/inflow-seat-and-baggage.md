# Seat

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this endpoint for inflow seat lookup.

{% hint style="warning" %}
`seatAvailability.do` no longer supports independent mode.

Call it only with a valid `sessionId` from `verify.do` or `OfferId` from `getOffers.do`.

Do not call it with flight data alone.
{% endhint %}

{% hint style="warning" %}
`seatAvailability.do` shares one `60 QPM` ancillary pool with `getLuggage.do`.

Over-limit requests return `HTTP 429 Too Many Requests`.

Wait for the returned `retryAfter` value before retrying.
{% endhint %}

### SeatAvailability call rules

Use `seatAvailability.do` only inside a valid booking chain.

Supported request context:

* `sessionId` returned by `verify.do`
* `OfferId` returned by `getOffers.do`

Unsupported request context:

* flight information alone

### Regional handling

#### Global customers

Keep the current flow.

Use `sessionId` or `OfferId` as before.

#### China OTA scenarios

Some upstream seat requests contain only flight information.

For this case, keep the `sessionId` returned by `verify.do`.

When the seat request arrives, match the flight to the cached `sessionId`.

If the match succeeds, call `seatAvailability.do` with that `sessionId`.

If no match exists, treat it as a pure quote request.

Atlas does not support that case.

### Why this changed

This rule keeps seat pricing and fulfillment aligned with the real booking chain.

It also reduces invalid airline-side queries.

Use [API Request Limits](../../product-guides/booking/booking-overview/api-request-limits.md) for shared rules and counting details.

{% openapi-operation spec="atlas-api" path="/seatAvailability.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260709%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260709T032226Z&X-Amz-Expires=172800&X-Amz-Signature=f0f1c9dcc24cca3c9dd4e640a476f6d87540108e439f74665c68014015dac5a1&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
