---
description: Atlas API Webhook 与事件端点参考，用于注册通知、接收订单事件并查询事件处理结果。
---

# Webhook 与事件 API

{% include "../../.gitbook/includes/eva-help-hint.md" %}

{% include "../../.gitbook/includes/environment-endpoint-note.md" %}

使用本部分配置 Atlas 事件通知，并查询已发生的事件。

Webhook 支持订单和航空公司相关的异步状态跟进。

### 常见问题

#### 如何接收 Atlas 订单事件？

使用[Webhook 注册与事件](webhook-registration-and-incidents.md)配置通知端点。

保存投递结果，并按业务流程处理每个事件。

#### Webhook 未收到事件时应怎么办？

先确认注册配置和接收端可用性。

然后使用事件查询核对预期事件与已处理记录。

### 相关指南

* [Webhook 概述](../../product-guides/extensions-and-integrations/webhook-overview/) — 了解事件覆盖范围和投递预期。
* [多渠道通知](../../product-guides/extensions-and-integrations/multi-channel-notifications.md) — 配置 webhook、邮件和协作工具通知。

### 后续步骤

在生产环境启用前，使用沙箱验证事件接收、去重和异常处理。
