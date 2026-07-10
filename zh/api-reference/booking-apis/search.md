# 搜索

{% include "../../.gitbook/includes/eva-help-hint.md" %}

{% include "../../.gitbook/includes/environment-endpoint-note.md" %}

当 Atlas 是您的主要搜索入口点时使用此端点。

它返回 `verify.do` 使用的 `routingIdentifier`。

{% hint style="info" %}
`智能搜索` (`smartSearch.do`) 即将弃用。

新集成请使用 `search.do`。
{% endhint %}

{% hint style="warning" %}
`search.do` 默认使用 `10 QPS`。

超出限制的请求返回 `HTTP 429 Too Many Requests`。

请等待返回的 `retryAfter` 值后再重试。
{% endhint %}

有关共享规则和计数详情，请使用 [API 请求限制](../../product-guides/booking/booking-overview/api-request-limits.md)。

{% openapi-operation spec="atlas-api" path="/search.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260710%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260710T150255Z&X-Amz-Expires=172800&X-Amz-Signature=0388a193e40550981d2a95589da0c83cd718526413c3398fb2da98c370cda0a1&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
