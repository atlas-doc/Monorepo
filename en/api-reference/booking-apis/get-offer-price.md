---
description: >-
  Atlas API getOfferPrice.do reference for pricing offers in the Fulfilment API
  booking workflow.
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

Use [API Request Limits](../../product-guides/booking/booking-overview/api-request-limits.md) for request-limit details.

{% openapi-operation spec="atlas-api" path="/getOfferPrice.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T083622Z&X-Amz-Expires=172800&X-Amz-Signature=8ecfe8fda6f5a32473da008d6ddf175f45c50f70ab0fd5ec308bd5af9cad3aaa&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
