---
description: 标准搜索、已知行程报价查询和快速履约的端到端预订路径。
---

# 预订路径

使用此部分了解端到端的 Atlas API 预订流程。

当您需要以下内容时从这里开始：

* 比较三种预订路径
* 决定从 `search.do`、`getOffers.do` 还是 `getOfferPrice.do` 开始
* 根据您的支付和出票约束匹配预订路径

### 选择正确的流程

当 Atlas 是您主要的搜索层时，使用[标准预订](standard-booking-flow.md)。

从 `search.do` 开始。

然后在 `order.do` 之前继续调用 `verify.do`。

当行程已知或需要独立价格检查时，使用[获取报价接口](get-offer-flow.md)。

从 `getOffers.do` 开始。

然后使用 `OfferId` 继续调用 `order.do`。

当您需要更广泛的报价可见性且可以在创建订单后立即开始支付时，使用[核价出票接口](fulfillment-flow.md)。

从 `getOfferPrice.do` 开始。

遵守更严格的履约时间规则。

需要帮助选择入口路径？

请使用[搜索 vs 报价](../booking-overview/booking-decisions/search-vs-offer.md)和[获取报价 vs 获取报价价格](../booking-overview/booking-decisions/get-offer-vs-get-offer-price.md)。

### 可用流程

* [标准预订](standard-booking-flow.md)
* [获取报价接口](get-offer-flow.md)
* [核价出票接口](fulfillment-flow.md)

每个流程页面包含该路径的完整端到端步骤序列。

### 需要更深入的决定指南？

使用[预订决策](../booking-overview/booking-decisions/)了解重新开始选择、API 边界和边缘情况。

### 需要跨流程的共享规则？

使用[预订概述](../booking-overview/)。

### 需要详细了解某个预订步骤？

使用[预订步骤指南](../booking-step-guides/)。

### 需要可选座位或行李处理？

使用[可选附加服务](../optional-ancillaries/)。
