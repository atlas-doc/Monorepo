---
description: >-
  Atlas API 预订流程概述，涵盖搜索、获取报价、验证、订单创建、支付、出票、标识符和订单跟进。
---

# 预订概述

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

使用此部分选择正确的 Atlas API 预订流程，并在每个步骤保留正确的标识符。

<figure><img src="../../../.gitbook/assets/FlowChart_2_IssueTicket.png" alt=""><figcaption><p>从搜索到支付和跟进的预订流程</p></figcaption></figure>

当您需要以下内容时从这里开始：

* 了解标准的 Atlas API 预订流程
* 在 `search.do` 和 `getOffers.do` 之间做选择
* 查看每个步骤应保留哪个标识符
* 在售前评估航线覆盖和原始价格

### 常见问题

#### 每个步骤后应保留哪个标识符？

在 `search.do` 后保留 `routingIdentifier`。

在 `verify.do` 后保留 `sessionId`。

在 `order.do` 后保留 `orderNo`。

出票后保留航司 PNR 和 `ticketNos`。

对于获取报价流程，从 `getOffers.do` 保留 `OfferId`。

#### `routingIdentifier` 和 `sessionId` 的有效期是多久？

`routingIdentifier` 在 `search.do` 后最长有效 6 小时。

`sessionId` 在 `verify.do` 后最长有效 2 小时。

两种情况下，较短时间更安全，因为运价和库存可能更早变化。

#### 标准的 Atlas API 预订流程是什么？

标准流程是 `search.do` → `verify.do` → `order.do` → `pay.do` → `queryOrderDetails.do`。

`支付后轮询` 不是独立的 API 步骤。

它解释了如何持续使用 `queryOrderDetails.do` 直到出票达到终态。

如果航司是 FR，在支付前添加 `orderCommit.do`。

#### 何时应使用 `getOffers.do` 而不是 `search.do`？

当 Atlas 是您的主要购物入口点时，使用 `search.do`。

当您已知道目标行程或需要独立价格检查时，使用 `getOffers.do`。

当您需要履约路径（具有更广泛的展示规则和严格的 5 分钟出票窗口）时，使用 `getOfferPrice.do`。

#### 何时应使用 `priceCompareSearch.do`？

在售前进行航线覆盖检查和原始价格发现时，使用 `priceCompareSearch.do`。

它不是标准预订流程的一部分。

不要将其视为生产环境的预订价格源。

#### 应首先选择哪个流程？

当 Atlas 是您的主要搜索和预订层时，使用 `search.do`。

当目标行程已知或需要独立价格检查时，使用 `getOffers.do`。

仅在售前进行航线覆盖检查和原始价格发现时，使用 `priceCompareSearch.do`。

### API 请求限制

Atlas 对选定的预订前 API 应用请求限制治理。

超限请求返回 Atlas 错误代码 `429`。

#### 默认限制

* `search.do` 使用 `10 QPS`
* `verify.do` 和 `getOffers.do` 共享 `60 QPM`
* `getOfferPrice.do` 使用自己的履约 QPM 策略
* `seatAvailability.do` 和 `getLuggage.do` 共享 `60 QPM`

#### 不受此策略约束的 API

`order.do` 和 `pay.do` 不属于此 QPS 和 QPM 策略的一部分。

#### 什么计入限制

以下请求会计入：

* 成功的请求
* 无结果的请求
* 业务失败和航司失败
* 缓存命中的响应

以下请求不计入：

* 已被 QPS 或 QPM 拒绝的请求
* 认证、权限或验证失败
* 幂等性阻止的重复请求（从未进入业务处理）

#### 遇到 `429` 时怎么办

降低请求频率。

等待返回的 `retryAfter` 值后再重试。

避免立即重试循环。

有关完整策略，请使用[API 请求限制](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV)。

### 关键预订页面

* [标识符](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ns5eKoKIPFUTFhjJkPyC)
* [搜索](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/9K7uEnLGfEbpjGjni5gD)
* [价格比较搜索](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/xXO9qKGJUXpfkxLDdpiB)
* [获取报价](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FSGess6buGE1P02WnVNu)
* [获取报价价格](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/e7tapaArEz0MBOv62dxZ)
* [验证](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm)
* [创建订单](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE)
* [确认订单](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/cyd69uDJk3ulct18V6QB)
* [支付与出票](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB)
* [查询订单](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n)
* [可选附加服务](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Bbuhdlzobxaya4FUurUl)
* [预订决策](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ygfSw8OHHyKfi9HuC7VS)

### 预订流程中的关键标识符

在每个阶段保留并重用正确的标识符：

* 从 `search.do` 获取 `routingIdentifier`
* 从 `verify.do` 获取 `sessionId`
* 从 `order.do` 获取 `orderNo`
* 出票后从 `queryOrderDetails.do` 获取航司 PNR 和 `ticketNos`

对于获取报价路径，从 `getOffers.do` 保留 `OfferId`。

对于座位和行李查询，从 `verify.do` 保留 `sessionId`，或从 `getOffers.do` / `getOfferPrice.do` 保留 `OfferId`。

### 此部分涵盖的内容

* 搜索航班报价
* 通过独立的获取报价流程检索报价
* 验证运价和航线
* 创建订单
* 在需要时确认 FR 订单
* 支付和出票
* 检索预订详情
* 运行高级搜索流程
* 查询座位
* 查询行李

### 应选择哪个流程？

#### 标准搜索流程

当 Atlas 是您的主要搜索和预订层时使用此流程。

此路径首先使用 `search.do`，然后在预订前使用 `verify.do`。

#### 获取报价流程

当行程已知或需要在订单创建前进行独立价格检查时使用此流程。

此路径以 `getOffers.do` 开始，并使用 `OfferId`。

#### 履约流程

当您需要更广泛的报价可见性且您的系统可以立即执行支付时使用此流程。

此路径以 `getOfferPrice.do` 开始，并在订单创建后应用 5 分钟支付和出票窗口。

#### 价格比较搜索

当您需要售前覆盖可见性和原始价格信号时使用此流程。

此路径使用 `priceCompareSearch.do`。

它不替代标准预订流程。

### 流程摘要

#### 标准预订流程

使用 `search.do` → `verify.do` → `order.do` → `pay.do` → `queryOrderDetails.do`。

仅在需要时在订单前插入附加服务。

仅在 FR 航司时在支付前插入 `orderCommit.do`。

有关完整的分步顺序，请使用[标准预订流程](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/o5Zn1hYIBI5mVZ83ihHN)。

#### 如何包含座位和行李

将座位和行李视为预订流程中的可选附加项。

仅当附加销售是产品的一部分且流程支持时，才使用 `getLuggage.do` 和 `seatAvailability.do`。

在支付前使用它们以提高旅客清晰度和订单转化率。

仅使用有效的 `sessionId` 或 `OfferId` 调用 `seatAvailability.do`。

不要仅根据航班数据调用它。

#### 获取报价流程

使用 `getOffers.do` → `order.do` → `pay.do` → `queryOrderDetails.do`。

仅在需要时在订单前插入附加服务。

仅在 FR 航司时在支付前插入 `orderCommit.do`。

有关完整的分步顺序，请使用[获取报价流程](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/NS7gkZIr0mFD8f0vV1sj)。

#### 履约流程

使用 `getOfferPrice.do` → `order.do` → `pay.do` → `queryOrderDetails.do`。

仅在需要时在订单前插入附加服务。

将 5 分钟支付和出票窗口视为严格的。

有关完整的分步顺序，请使用[履约流程](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/0JojHpwRpiZgp5WlLy01)。

#### `pay.do` 之后会发生什么？

不要假设支付和最终出票在同一时刻发生。

使用 `queryOrderDetails.do` 直到订单达到最终出票状态。

Webhook 可以提供帮助，但不应该是您唯一的确认路径。

### 主要 API

* `search.do`
* `priceCompareSearch.do`
* `getOffers.do`
* `getOfferPrice.do`
* `verify.do`
* `order.do`
* `orderCommit.do`
* `pay.do`
* `queryOrderDetails.do`
* `smartSearch.do`
* `seatAvailability.do`
* `getLuggage.do`

### 按任务推荐的下一个页面

#### 选择正确的预订路径

使用：

* [预订决策](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ygfSw8OHHyKfi9HuC7VS)
* [搜索 vs 报价](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Pcq0icGceiiiaVBThnzx)
* [获取报价 vs 获取报价价格](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/hJ5KgpKJEmpzw2hRXmYp)

#### 构建标准流程

使用：

* [标识符](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ns5eKoKIPFUTFhjJkPyC)
* [标准预订流程](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/o5Zn1hYIBI5mVZ83ihHN)
* [搜索](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/9K7uEnLGfEbpjGjni5gD)
* [验证](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm)
* [创建订单](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE)

#### 构建支付和跟进

使用：

* [支付与出票](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB)
* [支付后轮询](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2qOXdnt78bFPEFbkcemP)
* [查询订单](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n)

#### 添加座位和行李

使用：

* [可选附加服务](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Bbuhdlzobxaya4FUurUl)
* [座位](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/3ujCySdZ8OYYLfGI3iF3)
* [行李](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ftzqh42LAaE6QYzklv67)
* [行李和座位 productCode 新鲜度](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Cxdx0FWp0CbRm6vH8YZg)

将这里的附加服务视为可选的添加项，而不是强制性的预订步骤。

#### 构建备选报价路径

使用：

* [预订决策](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ygfSw8OHHyKfi9HuC7VS)
* [获取报价流程](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/NS7gkZIr0mFD8f0vV1sj)
* [获取报价](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FSGess6buGE1P02WnVNu)
* [可选附加服务](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Bbuhdlzobxaya4FUurUl)

#### 构建履约路径

使用：

* [履约流程](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/0JojHpwRpiZgp5WlLy01)
* [获取报价价格](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/e7tapaArEz0MBOv62dxZ)
* [获取报价 vs 获取报价价格](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/hJ5KgpKJEmpzw2hRXmYp)
* [可选附加服务](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Bbuhdlzobxaya4FUurUl)
* [支付与出票](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB)
* [API 请求限制](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV)

#### 评估售前航线覆盖

使用：

* [价格比较搜索](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/xXO9qKGJUXpfkxLDdpiB)
* [搜索](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/9K7uEnLGfEbpjGjni5gD)

### 在以下情况下使用此部分

* 标准的搜索到出票流程
* 独立的报价查询和价格检查流程
* 售前航线覆盖和原始价格检查
* 适用时的 FR 订单确认支持
* 座位和行李追加销售
* 实时或智能搜索选项

### 完整 API 参考

在此查看端点级详情：

[预订 API](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/beDx3cjbYPiOQ1Pwk6bC)

### 相关页面

* [快速入门](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/MkEt9qjU24ig50fQ8be2)
* [获取沙箱凭据](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/O9n7Z0tHowy0I3hOF44f)
* [标识符](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ns5eKoKIPFUTFhjJkPyC)
* [可选附加服务](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Bbuhdlzobxaya4FUurUl)
* [预订决策](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ygfSw8OHHyKfi9HuC7VS)
* [错误代码](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)
