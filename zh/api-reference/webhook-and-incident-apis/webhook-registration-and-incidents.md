---
description: >-
  Atlas API webhook 注册和事件查询参考，用于端点设置、更新和事件对账。
---

# Webhook 注册与事件

{% include "../../.gitbook/includes/eva-help-hint.md" %}

使用此页面从 API 参考层注册你的 webhook 端点和查询事件记录。

在需要以下内容时从此处开始：

* 在上线前注册或更新 webhook URL
* 在错过或未解决的事件后查询事件记录
* 将 webhook 投递与事件记录进行对账

### 常见问题

#### 何时应注册 webhook URL？

在上线前注册 webhook URL。

然后在接收端点发生变更时更新它。

同一 URL 接收所有支持的事件，包括 `order.void`。

#### 何时应查询事件？

当 webhook 投递、航班时刻变更处理或运营跟进需要更深层次对账时，查询事件。

当事件轨迹不完整或在 webhook 处理后仍不清楚时，使用事件查询。

#### 履约流程订单应如何使用 webhook 和事件查询？

将 webhook 用作早期信号。

当事件轨迹不完整时，使用事件查询。

在 5 分钟履约窗口期间保持主动订单轮询。

### 本页面涵盖内容

* `updateWebhookURL.do` 用于 webhook 注册
* `event/getPageList.do` 用于事件查询

### 后续步骤

使用 [Webhook 概述](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/1kDgZtL5TYuOLUmAxRd6)了解运营模式和事件覆盖范围。

当需要更深入的事件跟进时，使用[事件查询](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/70gk6tmdLYkYGQSscSKw)和[事件通知](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/IrfigjkYxz2qfdAQwbuX)。

### 典型流程

{% stepper %}
{% step %}
### 注册你的 webhook URL

保存 Atlas 应调用的端点以进行 webhook 投递。
{% endstep %}

{% step %}
### 接收 webhook 事件

处理出票、作废、航班时刻变更、航司状态、邮件和事件通知。

对于履约流程订单，使用这些事件减少响应时间，而非替代订单查询。
{% endstep %}

{% step %}
### 在需要时查询事件

使用事件查询来对账错过或未解决的事件。
{% endstep %}
{% endstepper %}

### 在需要时使用此功能

* 初始 webhook 设置
* webhook 端点更新
* 事件对账
* 航班时刻变更或取消后的运营跟进

### 注册范围

使用 `updateWebhookURL.do` 注册一个 webhook URL。

Atlas 将该 URL 用于所有支持的 webhook 事件类型。

包括 `order.void`。

在开始使用 `getOfferPrice.do` 进行履约流量之前，应已完成同一注册。

### 相关页面

* [Webhooks](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/1kDgZtL5TYuOLUmAxRd6)
* [履约 API](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/e7tapaArEz0MBOv62dxZ)
* [事件查询](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/70gk6tmdLYkYGQSscSKw)
* [事件通知](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/IrfigjkYxz2qfdAQwbuX)

{% openapi-operation spec="atlas-api" path="/updateWebhookURL.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/6d498c79f43546e63a2289f81c033345c8210830410d2835d33def093c5f3f29.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260708%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260708T131020Z&X-Amz-Expires=172800&X-Amz-Signature=27126ae21ba6c52dbf38f05311990817f1e9c7b7109d7807e10d2e1b9238185d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="atlas-api" path="/event/getPageList.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/6d498c79f43546e63a2289f81c033345c8210830410d2835d33def093c5f3f29.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260708%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260708T131020Z&X-Amz-Expires=172800&X-Amz-Signature=27126ae21ba6c52dbf38f05311990817f1e9c7b7109d7807e10d2e1b9238185d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
