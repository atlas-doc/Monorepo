---
description: 用于出票后附加服务及相关出票后操作的 API。
---

# 出票后附加服务

{% include "../../.gitbook/includes/eva-help-hint.md" %}

在原始机票已出票后使用此部分。

{% hint style="info" %}
此处的出票后附加服务支持仅针对行李。

不支持出票后的座位选择。
{% endhint %}

### 此部分涵盖的内容

* 搜索预订后附加服务选项
* 为已出票的机票创建附加服务订单
* 处理与行李相关的出票后流程

### 典型流程

{% stepper %}
{% step %}
### 搜索附加服务

查询已出票订单的可用的出票后附加服务产品。
{% endstep %}

{% step %}
### 订购附加服务

使用选定的产品代码创建附加服务订单。
{% endstep %}
{% endstepper %}

### 主要 API

* `postBookingAncillarySearch.do`
* `postBookingAncillaryOrder.do`

### 在以下情况使用此页面

* 出票后添加行李
* 处理预订后附加服务购买
* 支持出票后服务操作

### 完整 API 参考

使用完整的端点模式和示例：

[出票后附加服务](../../api-reference/post-booking-apis/post-ticketing-ancillaries.md)

### 相关页面

* [Webhook 概览](../extensions-and-integrations/webhook-overview/)
* [预订后操作](./)
* [退款](refunds.md)
