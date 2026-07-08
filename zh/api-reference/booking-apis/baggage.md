# 行李

{% include "../../.gitbook/includes/eva-help-hint.md" %}

使用此端点进行流入行李查询。

{% hint style="warning" %}
`getLuggage.do` 与 `seatAvailability.do` 共享一个 `60 QPM` 的辅助服务池。

超出限制的请求返回 `HTTP 429 Too Many Requests`。

请等待返回的 `retryAfter` 值后再重试。
{% endhint %}

### GetLuggage 调用规则

在有效的预订链中使用 `getLuggage.do`。

支持的请求上下文：

* `verify.do` 返回的 `sessionId`，作为 `offerId` 发送
* `getOffers.do` 返回的 `OfferId`

### 如何处理响应

`getLuggage.do` 返回当前行程的行李产品。

每个产品都有一个 `productCode`。

在选择行李时，将该 `productCode` 用于 `order.do`。

### 注意事项

* 在目标行程确认后查询行李
* 保持当前预订上下文的行李映射一致
* 对于联程航班，保持同一方向连接航段的行李选择一致

有关共享规则和计数详情，请使用 [API 请求限制](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV)。

{% openapi-operation spec="atlas-api" path="/getLuggage.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/6d498c79f43546e63a2289f81c033345c8210830410d2835d33def093c5f3f29.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260708%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260708T131021Z&X-Amz-Expires=172800&X-Amz-Signature=a7df629c73fe758cf3eba4a8807d31e59e90f716b8c4749c291410c9e4c62e50&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
