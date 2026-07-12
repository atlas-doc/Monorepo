---
description: Atlas API 预订端点参考，涵盖航班搜索、报价、验价、附加服务、订单创建、支付和出票。
---

# 预订 API

{% include "../../.gitbook/includes/eva-help-hint.md" %}

{% include "../../.gitbook/includes/environment-endpoint-note.md" %}

使用本部分获取预订流程的端点级参考。

在需要请求字段、响应字段或端点示例时，从此处开始。

### 常见问题

#### 预订 Atlas 航班应使用哪些 API？

标准流程通常为搜索、验价、创建订单、支付与出票。

根据工作流，你还可以使用获取报价、座位或行李 API。

#### 应先阅读产品指南还是 API 参考？

需要选择流程或理解顺序时，先阅读[预订概述](../../product-guides/booking/booking-overview/)。

需要精确的字段、模式和示例时，使用本部分的端点页。

### 按任务选择端点

* [搜索](search.md) — 搜索航班报价。
* [验价](verify.md) — 确认实时价格和预订条件。
* [创建订单](create-order.md) — 建立待支付订单。
* [支付与出票](payment-and-ticketing.md) — 支付订单并跟进出票。
* [获取报价](get-offer.md) — 为已知行程获取独立报价。
* [Get Offer Price](get-offer-price.md) — 在履约路径中为报价定价。
* [座位](inflow-seat-and-baggage.md) — 查询和选择座位。
* [行李](baggage.md) — 查询和添加行李服务。

### 后续步骤

完成端点实现后，使用[API 请求限制](../../product-guides/booking/booking-overview/api-request-limits.md)确认速率限制和重试行为。
