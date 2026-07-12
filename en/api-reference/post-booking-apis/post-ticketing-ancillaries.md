---
description: >-
  Atlas API reference for post-ticketing ancillary search, ordering, and related
  servicing workflows.
---

# Post-ticketing Ancillaries

{% include "../../.gitbook/includes/eva-help-hint.md" %}

### Baggage selection for connecting flights

Ancillary search may return baggage options per segment.

For connecting flights in the same direction, keep the baggage selection consistent across all connected segments.

Outbound and inbound can still use different baggage selections.

If baggage selections differ within one connected direction, ancillary order validation can reject the request.

{% openapi-operation spec="atlas-api" path="/postBookingAncillarySearch.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T083621Z&X-Amz-Expires=172800&X-Amz-Signature=d96b093f0818d36d49f45a087a44719b31b391c1572dd5420d410d5ff0bfd5ee&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="atlas-api" path="/postBookingAncillaryOrder.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T083621Z&X-Amz-Expires=172800&X-Amz-Signature=d96b093f0818d36d49f45a087a44719b31b391c1572dd5420d410d5ff0bfd5ee&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
