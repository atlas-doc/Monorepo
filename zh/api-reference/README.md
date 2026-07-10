---
description: Atlas API 端点参考文档，包含按工作流和能力组织的请求模式、响应字段和示例。
---

# API 参考

{% include "../.gitbook/includes/eva-help-hint.md" %}

{% include "../.gitbook/includes/environment-endpoint-note.md" %}

使用本部分获取精确的端点模式、字段和示例。

在以下情况下从此处开始：

* 确认精确的请求和响应字段
* 查找工作流的端点参考
* 在阅读指南后验证字段级别的实现细节

### 常见问题

#### 何时应使用 API 参考？

当你需要精确的端点级详细信息（如请求字段、响应字段、模式和示例）时，请使用 API 参考。

当需要流程选择、顺序指导或业务决策时，请首先使用[产品指南](../product-guides/)。

当需要入门、沙箱、UAT 或上线步骤时，请使用[集成指南](../readme-1/)。

#### 在 API 参考中应首先打开哪个页面？

从与任务匹配的工作流分组开始。

然后打开你要实现的 API 的精确端点页面。

### 按工作流浏览

* [预订 API](booking-apis/)
* [预订后 API](post-booking-apis/)
* [Webhook 与事件 API](webhook-and-incident-apis/)
* [工具 API](utility-apis/)

### 常见起点

* [搜索](booking-apis/search.md)
* [验价](booking-apis/verify.md)
* [创建订单](booking-apis/create-order.md)
* [支付与出票](booking-apis/payment-and-ticketing.md)
* [退款](post-booking-apis/refunds.md)
* [Webhook 注册与事件](webhook-and-incident-apis/webhook-registration-and-incidents.md)
* [余额](utility-apis/balance.md)
* [ATRIP 令牌](utility-apis/atrip-token.md)

### 推荐用法

1. 从[产品指南](../product-guides/)开始选择工作流。
2. 使用[集成指南](../readme-1/)进行沙箱、UAT 和生产部署。
3. 使用本部分获取请求和响应详细信息。
4. 使用[支持与参考](../support-and-reference/)进行故障排除、共享参考数据和更新。

### 通过 MCP 更快实现

在需要帮助寻找正确工作流、比较相关 API 或缩小下一步集成范围时，使用[MCP 辅助开发](../readme-1/integration-tools/mcp-assisted-development.md)。

在工作流明确后，使用本部分作为字段级别的权威来源。

### 后续步骤

确认端点模式后，返回匹配的工作流或集成页面继续实施。
