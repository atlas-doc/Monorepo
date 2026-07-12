---
description: Atlas API verify.do 验价端点参考，用于确认实时价格、预订要求和订单创建前的会话状态。
---

# 验价

{% include "../../.gitbook/includes/eva-help-hint.md" %}

在 `search.do` 之后使用此端点刷新运价、航线和预订要求。

它返回 `order.do` 使用的 `sessionId`。

{% hint style="info" %}
使用不超过 6 小时的 `routingIdentifier`。

在 2 小时内使用返回的 `sessionId` 进行 `order.do`。
{% endhint %}

{% hint style="warning" %}
`verify.do` 与 `getOffers.do` 共享一个 `60 QPM` 的履约池。

超出限制的请求返回 `HTTP 429 Too Many Requests`。

请等待返回的 `retryAfter` 值后再重试。
{% endhint %}

有关共享规则和计数详情，请使用 [API 请求限制](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV)。

{% openapi-operation spec="atlas-api" path="/verify.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130709Z&X-Amz-Expires=172800&X-Amz-Signature=c45e97e7189fcd169671b3760c4336c0cd2eb7d48d677787ddce88113a0cc4a3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
