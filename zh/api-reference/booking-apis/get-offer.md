---
description: Atlas API getOffers.do 端点参考，用于为已知行程获取独立报价、实时价格和后续预订标识符。
---

# 获取报价

{% include "../../.gitbook/includes/eva-help-hint.md" %}

当目标行程已知时使用此端点。

它返回 `order.do` 和可选的辅助服务查询使用的 `OfferId`。

{% hint style="info" %}
使用 OpenAPI 命名作为权威来源。

在实现和文档中使用 `getOffers.do`。
{% endhint %}

{% hint style="warning" %}
`getOffers.do` 与 `verify.do` 共享一个 `60 QPM` 的履约池。

超出限制的请求返回 `HTTP 429 Too Many Requests`。

请等待返回的 `retryAfter` 值后再重试。
{% endhint %}

有关共享规则和计数详情，请使用 [API 请求限制](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV)。

{% openapi-operation spec="atlas-api" path="/getOffers.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130708Z&X-Amz-Expires=172800&X-Amz-Signature=4374947ae0632333ad3b7840636e7638e090f48e9f0b320f1cb7ed976813a7a3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
