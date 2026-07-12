---
description: >-
  Atlas API verify.do reference for validating an offer before order creation
  and reviewing booking requirements.
---

# Verify

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this endpoint after `search.do` to refresh fare, routing, and booking requirements.

It returns the `sessionId` used by `order.do`.

{% hint style="info" %}
Use a `routingIdentifier` that is no more than 6 hours old.

Use the returned `sessionId` within 2 hours for `order.do`.
{% endhint %}

{% hint style="warning" %}
`verify.do` shares one `60 QPM` fulfillment pool with `getOffers.do`.

Over-limit requests return `HTTP 429 Too Many Requests`.

Wait for the returned `retryAfter` value before retrying.
{% endhint %}

Use [API Request Limits](../../product-guides/booking/booking-overview/api-request-limits.md) for shared rules and counting details.

{% openapi-operation spec="atlas-api" path="/verify.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T083621Z&X-Amz-Expires=172800&X-Amz-Signature=d96b093f0818d36d49f45a087a44719b31b391c1572dd5420d410d5ff0bfd5ee&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
