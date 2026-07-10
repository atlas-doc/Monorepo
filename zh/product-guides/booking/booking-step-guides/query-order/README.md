---
description: >-
  Atlas API 订单查询流程，用于获取预订状态、出票进度、航司 PNR 及最终订单跟进。
---

# 查询订单

{% include "../../../../.gitbook/includes/eva-help-hint.md" %}

使用此页面检查最新的预订状态。

这是 `pay.do` 之后的标准跟进步骤。

如果您需要轮询规则和时机指导，请使用[支付后轮询](post-payment-polling.md)。

在以下情况下从此页面开始：

* 在 `pay.do` 后跟踪出票进度
* 确认订单是否已支付或已出票
* 出票后读取航司 PNR 和票号详情

### 常见问题

#### 何时应调用 `queryOrderDetails.do`？

在需要最新订单状态时，在 `order.do` 或 `pay.do` 之后调用。

在预订达到最终状态之前，将其作为主要的跟进 API 使用。

#### 在订单查询响应中应检查什么？

检查 `orderStatus`、`ticketStatus`、航司 PNR 详情和票号。

使用这些字段确认出票是否仍在进行中或已完成。

### 主要 API

* `queryOrderDetails.do`

### 适用场景

* 轮询出票进度
* 检索预订和乘客详情
* 确认航司 PNR 和最终状态

### 常见检查项

* `orderStatus`
* `ticketStatus`
* 航司 PNR 详情
* 附加服务和运价数据

### 订单查询帮助您做出哪些决策？

用于决策：

* 是否应重试支付
* 出票是否仍在处理中
* 航司 PNR 和票号是否已可用
* 是否可以开始预订后操作

### 最佳实践

使用 `queryOrderDetails.do` 作为支付后的主要状态来源。

Webhook 可以提供帮助，但不应该是您唯一的确认方式。

如果支付可能正在进行或已完成，请在任何重试前查询订单。

### 履约流程跟进

如果订单来自 `getOfferPrice.do`，请更积极地监控。

使用订单查询确认订单是否仍在出票中、已出票或已因超时被取消。

当订单已接近 5 分钟履约截止时间时，不要继续重试支付。

### 相关页面

* [支付与出票](../payment-and-ticketing/)
* [出票后附加服务](../../../post-booking/post-ticketing-ancillaries.md)
* [Webhook 概述](../../../extensions-and-integrations/webhook-overview/)
* [预订 API](../../../../api-reference/booking-apis/)

### 完整 API 参考

在此查看端点级别的详细信息：

* [查询订单](../../../../api-reference/booking-apis/query-order.md)
