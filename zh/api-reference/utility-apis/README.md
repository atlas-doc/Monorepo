---
description: Atlas API 工具端点参考，涵盖余额查询、航线导出、邮件查询和 ATRIP 令牌生成。
---

# 工具 API

{% include "../../.gitbook/includes/eva-help-hint.md" %}

{% include "../../.gitbook/includes/environment-endpoint-note.md" %}

使用工具 API 完成集成后的运营、财务和数据操作。

这些端点不属于核心预订交易流程。

### 常见问题

#### 如何查询账户余额？

使用[余额](balance.md)端点获取余额信息。

将结果用于财务核对和运营检查。

#### 如何获取航线或订单相关数据？

使用[航线导出](route-export.md)获取航线数据。

使用[邮件查询](email-query.md)检索关联邮件记录。

### 按任务选择端点

* [余额](balance.md) — 查询账户余额。
* [航线导出](route-export.md) — 导出航线数据。
* [邮件查询](email-query.md) — 查询订单关联邮件。
* [ATRIP 令牌](atrip-token.md) — 生成下游流程所需令牌。
