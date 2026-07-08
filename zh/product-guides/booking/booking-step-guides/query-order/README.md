---
description: Atlas API 订单查询流程。
---

# 查询订单

使用此页面查询订单详情。

### 概述

查询订单用于在支付后跟进订单状态，直到出票完成或达到终态。

### 关键规则

* 支付后持续轮询直到出票或取消
* 使用 `queryOrderDetails.do` 获取最新订单状态
* Webhook 可以作为补充，但不应该是唯一的确认方式

### 相关页面

* [支付后轮询](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2qOXdnt78bFPEFbkcemP)
* [支付与出票](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB)
