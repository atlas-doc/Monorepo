---
description: >-
  可选座位和行李指南，涵盖支持的预订流程、选择时机、新鲜度规则及回退处理。
---

# 可选附加服务

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

当您需要在预订中安全添加可选座位或行李时，请使用此部分。

这不是一个强制性的预订步骤。

仅在附加服务升级是您产品的一部分且预订流程支持时使用。

支持的预订上下文包括：

* `verify.do` 后的 `sessionId`
* `getOffers.do` 后的 `OfferId`
* `getOfferPrice.do` 后的 `OfferId`

此部分帮助您：

* 选择合适的附加服务查询步骤
* 在 `order.do` 之前保持座位和行李数据的新鲜度
* 明确处理座位回退行为
* 避免因过期的 `productCode` 导致的失败

### 简要说明

座位和行李是预订流程中的可选附加项。

仅在需要时添加。

在接近订单创建时使用座位和行李数据。

当预订上下文发生变化或预订被延迟时，刷新附加服务。

不要将座位或行李的 `productCode` 值视为可重用的目录 ID。

### 何时使用此部分

在以下情况下使用此部分：

* 您希望在预订前添加座位升级
* 您希望在预订前添加行李升级
* `order.do` 因附加服务数据可能过期而失败
* 您需要决定所选座位不可用时的处理方式

如果预订不包含座位或行李升级，请跳过此部分。

### 阅读顺序

#### 添加座位

从[座位](seats-and-baggage/)开始。

然后，当订单时的座位处理需要业务规则时，使用[座位回退模式](seats-and-baggage/seat-fallback-modes.md)。

#### 添加行李

从[行李](baggage.md)开始。

当行李报价和航段映射是预订流程的一部分时使用。

#### 预订前验证新鲜度

在会话、报价、行程或乘客组合发生变化时，在 `order.do` 之前使用[行李和座位 productCode 新鲜度](baggage-and-seat-productcode-freshness.md)。

### 本部分的页面

* [座位](seats-and-baggage/)
* [行李](baggage.md)
* [行李和座位 productCode 新鲜度](baggage-and-seat-productcode-freshness.md)

### 快速决策规则

#### 何时查询座位？

仅从有效的预订上下文中查询座位。

在 `verify.do` 后使用 `sessionId`，或在 `getOffers.do` 或 `getOfferPrice.do` 后使用 `OfferId`。

#### 何时查询行李？

在目标行程确认后查询行李。

保持航段映射精确。

#### 何时刷新附加服务？

在以下情况下刷新：

* `sessionId` 发生变化
* `OfferId` 发生变化
* 行程发生变化
* 乘客数量或乘客类型发生变化
* 预订延迟足够长，使旧上下文变得不可靠

### 常见风险

#### 使用过期的附加服务数据

旧的座位或行李选择可能不再匹配当前的预订上下文。

这可能导致 `order.do` 期间的附加服务不匹配失败。

#### 将 `productCode` 视为稳定的 SKU

不要这样做。

座位和行李的 `productCode` 值是与上下文绑定的。

#### 忽略座位回退行为

如果所选座位在出票前消失，订单结果取决于您发送的座位处理模式。

请明确该行为。

### 按任务推荐的下一个页面

#### 预订前添加座位

使用：

* [座位](seats-and-baggage/)
* [座位回退模式](seats-and-baggage/seat-fallback-modes.md)

#### 预订前添加行李

使用：

* [行李](baggage.md)
* [创建订单](../booking-step-guides/create-order.md)

#### 修复过期的附加服务失败

使用：

* [行李和座位 productCode 新鲜度](baggage-and-seat-productcode-freshness.md)
* [错误码](../../../support-and-reference/troubleshooting-and-support/errors-handing/)

### 相关页面

* [预订概述](../booking-overview/)
* [获取报价](../booking-step-guides/get-offer.md)
* [获取报价价格](../booking-step-guides/get-offer-price.md)
* [验证](../booking-step-guides/verify.md)
* [创建订单](../booking-step-guides/create-order.md)
