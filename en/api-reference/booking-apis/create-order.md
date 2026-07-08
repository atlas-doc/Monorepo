# Create Order

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this endpoint to create the booking after verification.

It uses the current `sessionId` and returns the `orderNo` used by `pay.do` and order follow-up.

### Baggage for connecting flights

Atlas may return baggage options per segment.

For connecting flights in the same direction, keep the baggage selection consistent across all connected segments.

If outbound connected segments use different baggage selections, or inbound connected segments use different baggage selections, order creation can fail with `307`.

Outbound and inbound can still use different baggage selections.

Use [Verify](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm) as the source of truth for `bookingRequirement` and the current `sessionId`.

{% openapi-operation spec="atlas-api" path="/order.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/6d498c79f43546e63a2289f81c033345c8210830410d2835d33def093c5f3f29.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260708%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260708T131020Z&X-Amz-Expires=172800&X-Amz-Signature=27126ae21ba6c52dbf38f05311990817f1e9c7b7109d7807e10d2e1b9238185d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
