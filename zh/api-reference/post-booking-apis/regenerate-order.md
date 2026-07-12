---
description: Atlas API 重新生成订单端点参考，用于恢复订单数据并继续适用的预订后运营流程。
---

# 重新生成订单

{% include "../../.gitbook/includes/eva-help-hint.md" %}

当符合恢复条件的订单已过期或失败时，使用 `regenerateOrder.do` 重建订单。

它用于预订后的运营恢复，不属于标准搜索到出票流程。

### 常见问题

#### 何时应使用 `regenerateOrder.do`？

仅在恢复路径支持当前订单状态时使用。

确认原始订单已不可用后，再尝试重建。

#### `regenerateOrder.do` 可以延长履约流程的出票期限吗？

不可以。不要使用订单重建延长履约路径的 5 分钟支付和出票窗口。

重建前，确认原始履约订单已达到最终取消或不可支付状态。

#### 重建订单后应做什么？

根据返回的订单状态继续适用的后续流程。

需要订单状态确认时，使用[查询订单](../booking-apis/query-order.md)。

### 相关指南

使用[订单维护](../../product-guides/post-booking/order-maintenance.md)了解订单重建、停止出票和运营查询的适用边界。

{% openapi-operation spec="atlas-api" path="/regenerateOrder.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130708Z&X-Amz-Expires=172800&X-Amz-Signature=4374947ae0632333ad3b7840636e7638e090f48e9f0b320f1cb7ed976813a7a3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
