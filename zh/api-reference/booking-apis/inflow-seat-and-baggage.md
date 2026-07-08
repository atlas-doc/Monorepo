# 座位

{% include "../../.gitbook/includes/eva-help-hint.md" %}

使用此端点进行流入座位查询。

{% hint style="warning" %}
`seatAvailability.do` 不再支持独立模式。

仅使用 `verify.do` 的有效 `sessionId` 或 `getOffers.do` 的 `OfferId` 进行调用。

不要仅使用航班数据调用它。
{% endhint %}

{% hint style="warning" %}
`seatAvailability.do` 与 `getLuggage.do` 共享一个 `60 QPM` 的辅助服务池。

超出限制的请求返回 `HTTP 429 Too Many Requests`。

请等待返回的 `retryAfter` 值后再重试。
{% endhint %}

### SeatAvailability 调用规则

仅在有效的预订链中使用 `seatAvailability.do`。

支持的请求上下文：

* `verify.do` 返回的 `sessionId`
* `getOffers.do` 返回的 `OfferId`

不支持的请求上下文：

* 仅航班信息

### 区域处理

#### 全球客户

保持当前流程。

像以前一样使用 `sessionId` 或 `OfferId`。

#### 中国 OTA 场景

某些上游座位请求仅包含航班信息。

对于这种情况，保留 `verify.do` 返回的 `sessionId`。

当座位请求到达时，将航班与缓存的 `sessionId` 进行匹配。

如果匹配成功，使用该 `sessionId` 调用 `seatAvailability.do`。

如果不存在匹配，则将其视为纯询价请求。

Atlas 不支持这种情况。

### 变更原因

此规则确保座位定价和履约与实际预订链保持一致。

同时也减少了无效的航司侧查询。

有关共享规则和计数详情，请使用 [API 请求限制](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV)。

{% openapi-operation spec="atlas-api" path="/seatAvailability.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/6d498c79f43546e63a2289f81c033345c8210830410d2835d33def093c5f3f29.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260708%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260708T131020Z&X-Amz-Expires=172800&X-Amz-Signature=27126ae21ba6c52dbf38f05311990817f1e9c7b7109d7807e10d2e1b9238185d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
