---
description: Atlas API 订单列表端点参考，用于查询订单集合，支持预订后运营、核对和订单跟进。
---

# 订单列表

{% include "../../.gitbook/includes/eva-help-hint.md" %}

使用 `orderList.do` 查询订单集合，支持预订后的运营核对和订单跟进。

它适用于列表级查询，而非单笔订单的出票状态确认。

### 常见问题

#### 何时应使用 `orderList.do`？

当需要查询多个订单并进行运营跟进时使用。

使用它支持订单核对和预订后处理。

#### 如何查询单笔订单的出票状态？

使用[查询订单](../booking-apis/query-order.md)获取单笔订单状态、出票进度和订单详情。

不要使用列表查询替代支付后的订单状态跟进。

#### 查询订单后应做什么？

根据订单状态选择适用的预订后操作。

退款、作废和订单维护流程请参阅[预订后操作](../../product-guides/post-booking/)。

### 相关指南

使用[订单维护](../../product-guides/post-booking/order-maintenance.md)了解运营查询与其他维护操作的边界。

{% openapi-operation spec="atlas-api" path="/orderList.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130708Z&X-Amz-Expires=172800&X-Amz-Signature=4374947ae0632333ad3b7840636e7638e090f48e9f0b320f1cb7ed976813a7a3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
