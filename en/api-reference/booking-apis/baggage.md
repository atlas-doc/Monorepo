# Baggage

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this endpoint for inflow baggage lookup.

{% hint style="warning" %}
`getLuggage.do` shares one `60 QPM` ancillary pool with `seatAvailability.do`.

Over-limit requests return `HTTP 429 Too Many Requests`.

Wait for the returned `retryAfter` value before retrying.
{% endhint %}

### GetLuggage call rules

Use `getLuggage.do` inside a valid booking chain.

Supported request context:

* `sessionId` returned by `verify.do`, sent as `offerId`
* `OfferId` returned by `getOffers.do`

### What to do with the response

`getLuggage.do` returns baggage products for the current itinerary.

Each product has a `productCode`.

Use that `productCode` in `order.do` when baggage is selected.

### Notes

* query baggage after the target itinerary is confirmed
* keep baggage mapping consistent for the current booking context
* for connecting flights, keep baggage selection consistent across connected segments in the same direction

Use [API Request Limits](../../product-guides/booking/booking-overview/api-request-limits.md) for shared rules and counting details.

{% openapi-operation spec="atlas-api" path="/getLuggage.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260709%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260709T032226Z&X-Amz-Expires=172800&X-Amz-Signature=f0f1c9dcc24cca3c9dd4e640a476f6d87540108e439f74665c68014015dac5a1&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
