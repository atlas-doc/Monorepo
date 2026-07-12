---
description: >-
  Atlas API getOffers.do reference for pricing a known itinerary and retrieving
  bookable flight offers.
---

# Get Offer

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this endpoint when the target itinerary is already known.

It returns the `OfferId` used by `order.do` and optional ancillary lookup.

{% hint style="info" %}
Use OpenAPI naming as the source of truth.

Use `getOffers.do` in implementation and documentation.
{% endhint %}

{% hint style="warning" %}
`getOffers.do` shares one `60 QPM` fulfillment pool with `verify.do`.

Over-limit requests return `HTTP 429 Too Many Requests`.

Wait for the returned `retryAfter` value before retrying.
{% endhint %}

Use [API Request Limits](../../product-guides/booking/booking-overview/api-request-limits.md) for shared rules and counting details.

{% openapi-operation spec="atlas-api" path="/getOffers.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T083621Z&X-Amz-Expires=172800&X-Amz-Signature=d96b093f0818d36d49f45a087a44719b31b391c1572dd5420d410d5ff0bfd5ee&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
