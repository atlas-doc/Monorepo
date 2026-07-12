---
description: Atlas API 停止出票端点参考，用于在适用条件下中止订单出票，并安全管理后续操作。
---

# 停止出票

{% include "../../.gitbook/includes/eva-help-hint.md" %}

当订单流程支持停止出票时，使用 `stopTicket.do` 中止出票操作。

它用于预订后的运营处理，不属于标准预订步骤。

### 常见问题

#### 何时应使用 `stopTicket.do`？

仅当当前订单和流程支持停止出票时使用。

在调用前，先确认订单状态和业务处理目标。

#### 停止出票后应做什么？

查询订单以确认当前状态和可用的后续操作。

使用[查询订单](../booking-apis/query-order.md)获取订单与出票进度。

#### 停止出票与作废是否相同？

不是。停止出票用于中止适用流程中的出票操作。

作废适用于符合航司作废条件的订单。使用[作废](void.md)处理作废流程。

### 相关指南

使用[订单维护](../../product-guides/post-booking/order-maintenance.md)确认停止出票的适用边界。

{% openapi-operation spec="atlas-api" path="/stopTicket.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130708Z&X-Amz-Expires=172800&X-Amz-Signature=4374947ae0632333ad3b7840636e7638e090f48e9f0b320f1cb7ed976813a7a3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
