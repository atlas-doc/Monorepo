---
description: Atlas API 支付与出票流程。
---

# 支付与出票

使用此页面处理 Atlas 支付和出票。

### 概述

支付与出票流程涵盖订单创建后的支付处理和出票跟进。

### 关键规则

* 支付成功并不总是意味着出票已完成
* 使用 `queryOrderDetails.do` 跟进直到出票达到终态
* 对于履约流程，应用 5 分钟出票窗口

### 相关页面

* [创建订单](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE)
* [支付后轮询](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2qOXdnt78bFPEFbkcemP)
* [查询订单](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n)
