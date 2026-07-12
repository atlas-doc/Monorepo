---
description: Atlas API 比价搜索端点参考，用于检索和比较可用航班报价，支持后续报价或预订决策。
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# 比价搜索

{% include "../../.gitbook/includes/eva-help-hint.md" %}

使用此 API 进行售前航线覆盖和原始价格发现。

这不是标准的预订步骤。

{% hint style="warning" %}
`priceCompareSearch.do` 仅对售前客户可用。

默认使用配额为每天 1,000 次调用。

不要将返回的价格视为生产预订价格。
{% endhint %}

### 此 API 的功能

* 以最大航线覆盖范围返回原始价格
* 跳过预订规则过滤
* 忽略供应商运营开关
* 先检查 Atlas 缓存，然后回退到航司实时定价

### 请求兼容性

请求体与 `search.do` 完全兼容。

无需额外请求字段。

使用相同的核心字段：

* `tripType`、`adultNum`、`childNum`、`infantNum`
* `fromCity`、`toCity`、`fromDate`、`retDate`
* `airlines`、`currency`、`includeMultipleFareFamily`

### 如何读取响应

#### 当存在结果时

API 返回 `status: 0`、`msg: "success"` 和非空的 `routings` 数组。

`routings` 结构匹配 `search.do`。

#### 当不存在结果时

没有结果仍然返回 `status: 0`。

这是正常的业务结果。

检查以下两者：

* `routings.length`
* `noResultReason.code`

不要仅依赖 `status`。

### `noResultReason`

当 `routings` 为空时，响应可能包含 `noResultReason`。

它包含：

* `code` — 机器可读的原因
* `message` — 人类可读的详情
* `recentFlightDates` — 可选的实际航班计划附近日期

#### 原因代码

**`ROUTE_NOT_SUPPORTED`**

该航线不在 Atlas 覆盖范围内。

不要重试同一航线。

**`AIRLINE_NO_FLIGHT`**

航司未返回该航线和日期的航班信息。

检查 `recentFlightDates` 并使用其他支持的日期重试。

**`FLIGHT_SOLD_OUT`**

航班存在，但无可用座位。

检查 `recentFlightDates` 并使用其他日期重试。

**`PRICE_FETCH_FAILED`**

Atlas 无法从航司获取价格。

将此视为临时技术故障。

稍后重试。

### `recentFlightDates` 如何工作

`recentFlightDates` 返回搜索日期前后最多 7 个实际计划日期。

窗口目标为前后 3 天。

如果较早日期不可用，较晚日期将填补空缺。

列表仅包含有实际航班计划的日期。

### API 级别错误

`status != 0` 表示请求在 API 级别失败。

常见值包括：

* `100`、`101`、`102` — 请求数据缺失或无效
* `109` — 超出搜索限制
* `110` — 超出 QPS 限制
* `112` — 请求超时
* `900` — 未授权
* `9999` — 内部错误

### 集成指导

当你想在生产集成前评估 Atlas 航线覆盖范围时使用此 API。

当需要可预订的路径时，使用标准预订流程。

有关从搜索到出票的正常流程，请参见[预订概述](../../product-guides/booking/booking-overview/)。

{% openapi-operation spec="atlas-api" path="/priceCompareSearch.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130707Z&X-Amz-Expires=172800&X-Amz-Signature=299ebce0e5dadff16e59880204101597efad717e17104e120e224687194db559&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
