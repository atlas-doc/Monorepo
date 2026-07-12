---
description: Atlas API 预订后端点参考，涵盖退款、作废、订单维护、出票后附加服务和 PNR 操作。
---

# 预订后 API

{% include "../../.gitbook/includes/eva-help-hint.md" %}

{% include "../../.gitbook/includes/environment-endpoint-note.md" %}

使用本部分获取端点级别的预订后参考。

在需要以下内容时从此处开始：

* 退款端点详情
* 作废端点详情
* 辅助服务、维护或 PNR 预订后 API

### 主要 API 分组

* [退款](refunds.md)
* [作废](void.md)
* [出票后辅助服务](post-ticketing-ancillaries.md)
* [重新生成订单](regenerate-order.md)
* [停止出票](stop-ticket-issuance.md)
* [订单列表](order-list.md)
* [PNR 认领](pnr-claim.md)
* [提取 PNR](extract-pnr.md)

### 常见问题

#### 已出票订单应使用哪个 API？

根据任务选择端点。退款使用退款 API。作废使用作废 API。

需要恢复订单数据时，使用重新生成订单或 PNR 相关 API。

#### 作废和退款有什么区别？

作废适用于仍符合航司作废条件的订单。

不符合条件时，应使用退款流程。先检查订单状态和业务规则。

### 后续步骤

先阅读[预订后操作](../../product-guides/post-booking/)以选择正确流程。

随后打开与任务匹配的端点页，确认请求字段和响应处理方式。
