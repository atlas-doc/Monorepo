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

# Get Offer Price

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use `Get Offer Price` as the documentation name for `getOfferPrice.do`.

This endpoint starts the fulfillment flow.

Use it when you need fulfillment-specific pricing and can move to payment immediately after `order.do`.

Treat the returned context as fulfillment-specific.

Use [API Request Limits](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV) for request-limit details.

{% openapi-operation spec="atlas-api" path="/getOfferPrice.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/6d498c79f43546e63a2289f81c033345c8210830410d2835d33def093c5f3f29.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260708%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260708T131022Z&X-Amz-Expires=172800&X-Amz-Signature=b6079393979857c3a7b391b6d634998344fa7d201f2e66a8ca8bf6bfa021c674&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
