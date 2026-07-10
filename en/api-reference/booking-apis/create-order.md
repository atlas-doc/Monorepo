# Create Order

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this endpoint to create the booking after verification.

It uses the current `sessionId` and returns the `orderNo` used by `pay.do` and order follow-up.

### Baggage for connecting flights

Atlas may return baggage options per segment.

For connecting flights in the same direction, keep the baggage selection consistent across all connected segments.

If outbound connected segments use different baggage selections, or inbound connected segments use different baggage selections, order creation can fail with `307`.

Outbound and inbound can still use different baggage selections.

Use [Verify](../../product-guides/booking/booking-step-guides/verify.md) as the source of truth for `bookingRequirement` and the current `sessionId`.

{% openapi-operation spec="atlas-api" path="/order.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260710%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260710T101130Z&X-Amz-Expires=172800&X-Amz-Signature=b2ace22ab171cc0dd008352f0264395b9e5c587c72b2e0850bffd935060deef6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
