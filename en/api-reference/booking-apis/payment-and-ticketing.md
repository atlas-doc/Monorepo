# Payment & Ticketing

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this endpoint to pay an existing order.

Send `orderNo` and the selected `paymentMethod`.

Payment success does not always mean ticketing is already complete.

Use [Query Order](../../product-guides/booking/booking-step-guides/query-order/) to confirm the final ticketing state.

{% openapi-operation spec="atlas-api" path="/pay.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260709%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260709T031124Z&X-Amz-Expires=172800&X-Amz-Signature=1e9560eea36a0642d63d078b53660ca0003454e12d11250b98fbc3924e8ead9b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
