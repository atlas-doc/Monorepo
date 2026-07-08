---
description: >-
  从获取报价价格到订单跟进的履约预订路径，具有严格的 5 分钟支付和出票窗口。
---

# 履约流程

路径：`Get Offer Price → Order → Payment → Query Order`

当您需要履约路径且您的系统可以立即进入支付时，使用此流程。

本页面定义了该路径的端到端序列。

当您需要某一端点的步骤级详情时，请使用[预订步骤指南](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/7Hivwro5sZdOotzmaEIn)。

### 何时使用此流程

当您需要以下内容时使用此流程：

* 使用 `getOfferPrice.do` 作为入口点
* 访问具有更广泛展示规则的履约路径
* 在产品需要座位或行李追加销售时，在订单前添加可选附加服务
* 立即创建并支付订单

### 完整流程

{% stepper %}
{% step %}
### 获取报价价格

调用[获取报价价格](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/e7tapaArEz0MBOv62dxZ)。

保留返回的 `OfferId`。
{% endstep %}

{% step %}
### 可选附加服务

此步骤为可选。

当座位或行李追加销售是您产品的一部分时，在订单创建前使用[可选附加服务](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Bbuhdlzobxaya4FUurUl)。
{% endstep %}

{% step %}
### 创建订单

仅在可以立即开始支付时，使用 `OfferId` 调用[创建订单](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE)。

保留 `orderNo`。
{% endstep %}

{% step %}
### 支付与出票

立即调用[支付与出票](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB)。

将 5 分钟支付和出票窗口视为严格的。
{% endstep %}

{% step %}
### 查询订单

使用[查询订单](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n)作为支付后的标准跟进步骤。

持续跟进订单，直到出票或取消。

使用[支付后轮询](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2qOXdnt78bFPEFbkcemP)了解轮询时机和重试指导。
{% endstep %}
{% endstepper %}

### 关键规则

* 从 `getOfferPrice.do` 保留 `OfferId` 直到 `order.do`
* 订单创建后立即开始支付
* 将 5 分钟履约窗口视为严格的
* 在 `order.do` 后保留 `orderNo`
* 通过订单查询或 webhook 跟进最终状态
* 出票完成后保留航司 PNR 和 `ticketNos`

### 决策支持

当您在获取报价和获取报价价格之间做选择时，使用[获取报价 vs 获取报价价格](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/hJ5KgpKJEmpzw2hRXmYp)。

当您需要预订前 API 的请求限制指导时，使用[API 请求限制](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV)。

当您需要精确的请求和响应字段时，使用[API 参考](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/LfT8Y3jMIGXTnxwihZhV)。
