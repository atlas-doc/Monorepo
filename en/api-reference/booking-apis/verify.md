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

Use [API Request Limits](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV) for shared rules and counting details.

{% openapi-operation spec="atlas-api" path="/verify.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/6d498c79f43546e63a2289f81c033345c8210830410d2835d33def093c5f3f29.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260708%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260708T131020Z&X-Amz-Expires=172800&X-Amz-Signature=27126ae21ba6c52dbf38f05311990817f1e9c7b7109d7807e10d2e1b9238185d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
