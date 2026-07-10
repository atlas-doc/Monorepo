---
description: Atlas API 入门引导、沙箱设置、实施生命周期、UAT 验证和生产环境上线。
---

# 集成指南

{% include "../.gitbook/includes/eva-help-hint.md" %}

使用本部分进行 Atlas API 入门引导以及从沙箱到上线的完整实施生命周期。

当您需要以下内容时，从这里开始：

* 获取访问权限和凭证
* 按正确顺序构建集成
* 准备 UAT 验证材料
* 安全完成生产环境切换

### 集成指南包含什么

使用此部分进行：

* 入门引导和访问设置
* 沙箱实施
* 验证和上线准备
* 集成阶段设置任务

当您需要选择合适的预订流程或产品能力时，请使用[产品指南](../product-guides/)。

当您需要精确的端点字段和架构时，请使用[API 参考](../api-reference/)。

### 推荐阅读顺序

1. [快速入门](quick-start.md)
2. [沙箱访问](making-requests.md)
3. [沙箱开发](sandbox-development/)
4. [UAT 验证](uat-submission-guide.md)
5. [生产环境上线](production-go-live.md)

当您需要可选的实施加速工具时，请使用[集成工具](integration-tools/)，例如 [Atlas AI 助手技能](integration-tools/atlas-ai-assistant-skill.md)或 [MCP 辅助开发](integration-tools/mcp-assisted-development.md)。

### 常见起点

#### 新的 Atlas API 集成

从[快速入门](quick-start.md)开始。

然后前往[沙箱访问](making-requests.md)和[沙箱开发](sandbox-development/)。

#### UAT 和上线准备

使用[UAT 验证](uat-submission-guide.md)和[生产环境上线](production-go-live.md)。

#### 集成期间的通知设置

使用[Webhook 概述](../product-guides/extensions-and-integrations/webhook-overview/)了解 webhook 事件覆盖范围和处理指导。

使用[多渠道通知](../product-guides/extensions-and-integrations/multi-channel-notifications.md)进行 webhook、邮件、钉钉、企业微信、Slack 和 Teams 的渠道设置。

#### 需要选择预订流程？

使用[产品指南](../product-guides/)。

当您在三种主要预订路径之间做决策时，从[预订概述](../product-guides/booking/booking-overview/)开始。

### 典型实施生命周期

{% stepper %}
{% step %}
### 访问与启动

收集沙箱凭证并确认所需的请求头。
{% endstep %}

{% step %}
### 沙箱开发

在沙箱中构建集成并验证主要实施路径。
{% endstep %}

{% step %}
### UAT 验证

运行所需的 UAT 测试并提交验证材料。
{% endstep %}

{% step %}
### 生产环境上线

在 UAT 审批和账户激活后，切换到生产凭证和端点。
{% endstep %}
{% endstepper %}

### 相关部分

* [产品指南](../product-guides/)
* [API 参考](../api-reference/)
* [支持与参考](../support-and-reference/)
