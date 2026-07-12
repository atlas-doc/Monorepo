---
description: Atlas API 作废端点参考，用于检查作废条件、提交作废请求，并确定退款或后续处理路径。
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# 作废

{% include "../../.gitbook/includes/eva-help-hint.md" %}

使用本部分了解专用的作废生命周期。

在需要以下内容时从此处开始：

* 检查订单是否仍可作废
* 使用最新的 `voidOfferId` 提交作废请求
* 跟踪作废处理和结果

需要先了解工作流指南？

使用[作废工作流](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/B8hsI0GKlmcexaJt4Npx)。

### 常见问题

#### 标准的 Atlas API 作废流程是什么？

标准流程是 `voidQuotation.do` → `void.do` → `queryVoidOrders.do`。

首先请求报价。

然后使用最新的 `voidOfferId` 提交作废。

提交后，查询状态直到案件完成或被拒绝。

#### Atlas 会在截止日期后拒绝作废请求吗？

会。

如果返回的当日作废截止日期已过，`void.do` 会实时失败。

典型错误信息：

* `Void deadline exceeded. This ticket can no longer be voided`（超过作废截止日期。此票证无法再作废）

#### Atlas 支持部分乘客作废吗？

不支持。

Atlas 仅接受整单作废。

不要仅针对部分乘客提交作废。

#### 服务费固定时，是否仍需调用 `voidQuotation.do`？

需要。

每次 `void.do` 请求前都需要调用 `voidQuotation.do`。

#### 何时应使用作废而非退款？

当订单仍在航司作废窗口内时使用作废。

当作废窗口已过或案件需要走退款流程时使用退款。

### 当前作废覆盖范围

Atlas 作废目前支持四个地区的 23 家航司。

#### 美洲

* `AS`
* `DM`
* `F9`
* `G4`
* `PB`
* `SY`
* `TS`
* `Y4`

#### 欧洲

* `A3`
* `D8`
* `EI`
* `DY`
* `N0`
* `OA`
* `VF`
* `Z0`

#### 日本

* `ZG` — 仅限美国航线

#### 韩国

* `7C`
* `BX`
* `LJ`
* `RS`
* `TW`
* `ZE`

近期新增：

* `TS`
* `Y4`
* `EI`
* `VF`

覆盖范围因航司和航线而异。

如果预订超出此范围，Atlas 可能返回 `843`。

### 本部分涵盖内容

* 请求作废报价
* 提交作废请求
* 查询作废状态和结果

### 典型流程

{% stepper %}
{% step %}
### 作废报价

检查订单是否可作废。

获取最新金额、方式和 `voidOfferId`。
{% endstep %}

{% step %}
### 提交作废

使用最新的报价结果提交作废请求。

保留返回的 `voidCode` 用于后续跟进。
{% endstep %}

{% step %}
### 查询作废状态

跟踪进度，直到作废完成、被拒绝或以其他方式关闭。
{% endstep %}
{% endstepper %}

### 提交作废前应确认什么？

确认：

* 原始 `orderNo` 正确
* 订单仍在航司作废窗口内
* 返回的当日截止日期尚未过
* 使用的是最新的 `voidOfferId`
* 该案件应走作废流程，而非退款流程

作废处理通常比退款处理更严格。

窗口过期可能使订单不可作废，即使退款仍有可能。

如果截止日期已过，Atlas 会立即拒绝作废请求。

### 关键行为

* 作废使用专用端点
* 提交前应先进行报价
* `voidOfferId` 用于提交
* `voidCode` 用于状态跟进

### 主要 API

* `voidQuotation.do`
* `void.do`
* `queryVoidOrders.do`

### 请求模型

使用专用的作废流程，输入如下：

* `voidQuotation.do`：`orderNo`
* `void.do`：`orderNo` + `voidOfferId`
* `queryVoidOrders.do`：`voidCode`

{% hint style="warning" %}
作废应在订单级别处理。

不要将作废视为部分退款流程。

Atlas 仅接受整单作废。
{% endhint %}

### 端点说明

#### `voidQuotation.do`

使用报价获取最新的作废资格和金额。

预期响应回答：

* 订单是否可作废
* 适用的 `voidMethod`
* 下一步使用的 `voidOfferId`

首先读取的重要字段：

* `isVoidable`
* `voidOfferId`
* `expectedConfirmationDate`
* `expectedRefundDate`
* `voidWindow.sameDayDeadlineTime`
* `voidWindow.sameDayTimezone`

#### `void.do`

使用最新的 `voidOfferId` 提交作废。

保留返回的 `voidCode`。

使用该代码进行所有后续状态跟进。

即使服务费固定，也不要跳过报价。

如果返回的当日截止日期已过，Atlas 会实时拒绝请求。

#### `queryVoidOrders.do`

使用查询在提交后跟踪作废状态。

在大多数情况下，Atlas 会在约 5 分钟内返回作废请求是否已被接受处理。

最终完成或拒绝仍可能需要更长时间。

首先读取的重要字段：

* `voidCode`
* `voidStatus`
* `cancelReason`
* `actualRefundAmount`（可用时）

### 状态处理

需要关注的主要结果状态：

* 处理中
* 已退款或履约完成
* 已拒绝

如果作废被拒绝，首先检查 `cancelReason`。

如果作废窗口已过期，在适用时将案件移至退款流程。

### 集成说明

提交前使用最新的报价结果。

不要重复使用旧的 `voidOfferId`。

将作废窗口视为严格限制。

如果订单不再可作废，不要继续重试作废路径。

### Webhook 选项

Atlas 也可以将 `order.void` 发送到你注册的 webhook URL。

在 `void.do` 之后使用它获取近乎实时的状态更新。

Webhook 是提交后跟进进度的推荐方式。

首先读取这些字段：

* `data.orderNo`
* `data.voidCode`
* `data.voidStatus`
* `data.message`

无需额外注册 webhook。

使用通过 `updateWebhookURL.do` 注册的同一 URL。

当需要最终对账时，使用 `queryVoidOrders.do`。

阅读[作废通知](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/4aywYMVHUfvNZttgiHPn)。

### 相关页面

* [退款](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/4SLUBW4WrcN15Hl7KYDP)
* [作废通知](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/4aywYMVHUfvNZttgiHPn)
* [错误代码](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)
* [预订后 API](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/8P9YQq692vHSOmVjquJF)

{% openapi-operation spec="atlas-api" path="/voidQuotation.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130708Z&X-Amz-Expires=172800&X-Amz-Signature=4374947ae0632333ad3b7840636e7638e090f48e9f0b320f1cb7ed976813a7a3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="atlas-api" path="/void.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130708Z&X-Amz-Expires=172800&X-Amz-Signature=4374947ae0632333ad3b7840636e7638e090f48e9f0b320f1cb7ed976813a7a3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="atlas-api" path="/queryVoidOrders.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130708Z&X-Amz-Expires=172800&X-Amz-Signature=4374947ae0632333ad3b7840636e7638e090f48e9f0b320f1cb7ed976813a7a3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
