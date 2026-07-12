---
description: >-
  Atlas API queryOrderDetails.do reference for checking booking status,
  ticketing progress, and order details.
---

# Query Order

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this endpoint to read the latest order state after `order.do` or `pay.do`.

Check `orderStatus`, `ticketStatus`, airline PNR details, and ticket numbers here.

{% openapi-operation spec="atlas-api" path="/queryOrderDetails.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T083621Z&X-Amz-Expires=172800&X-Amz-Signature=d96b093f0818d36d49f45a087a44719b31b391c1572dd5420d410d5ff0bfd5ee&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
