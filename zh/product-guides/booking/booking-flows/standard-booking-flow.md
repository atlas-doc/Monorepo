---
description: >-
  从搜索到订单跟进的标准 Atlas 预订路径，适用于使用 Atlas 作为主要搜索和预订层的合作伙伴。
---

# 标准预订流程

路径：`Search → Verify → Order → Payment → Query Order`

当 Atlas 是您主要的搜索和预订层时，使用此流程。

本页面定义了该路径的端到端序列。

当您需要某一端点的步骤级详情时，请使用[预订步骤指南](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/7Hivwro5sZdOotzmaEIn)。

### 何时使用此流程

当您需要以下内容时使用此流程：

* 从 Atlas 搜索结果开始
* 在订单创建前重新检查运价和预订要求
* 遵循从搜索到出票的标准预订顺序

### 完整流程

{% stepper %}
{% step %}
### 搜索

调用[搜索](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/9K7uEnLGfEbpjGjni5gD)。

保留 `routingIdentifier`。
{% endstep %}

{% step %}
### 验证

在订单创建前调用[验证](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm)。

保留 `sessionId`。
{% endstep %}

{% step %}
### 可选附加服务

此步骤为可选。

当座位或行李追加销售是您产品的一部分时，在订单创建前使用[可选附加服务](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Bbuhdlzobxaya4FUurUl)。
{% endstep %}

{% step %}
### 创建订单

调用[创建订单](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE)。

保留 `orderNo`。
{% endstep %}

{% step %}
### 可选的 FR 确认

此步骤特定于航司。

当航司要求时，在支付前使用[确认订单（仅 FR）](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/cyd69uDJk3ulct18V6QB)。
{% endstep %}

{% step %}
### 支付与出票

调用[支付与出票](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB)。

支付成功并不总是意味着最终出票已完成。
{% endstep %}

{% step %}
### 查询订单

使用[查询订单](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n)作为支付后的标准跟进步骤。

持续跟进订单，直到出票或达到其他终态。

使用[支付后轮询](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2qOXdnt78bFPEFbkcemP)了解轮询时机和重试指导。
{% endstep %}
{% endstepper %}

### 关键标识符

* 在 `search.do` 后保留 `routingIdentifier`
* 在 `verify.do` 后保留 `sessionId`
* 在 `order.do` 后保留 `orderNo`
* 出票完成后保留航司 PNR 和 `ticketNos`

### 决策支持

当您需要将此路径与获取报价或履约流程进行比较时，使用[预订决策](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ygfSw8OHHyKfi9HuC7VS)。

当您需要精确的请求和响应字段时，使用[API 参考](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/LfT8Y3jMIGXTnxwihZhV)。
