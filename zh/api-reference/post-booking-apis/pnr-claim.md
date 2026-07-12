---
description: Atlas API PNR 认领端点参考，用于认领符合条件的航司 PNR，并将其纳入后续订单处理。
---

# PNR 认领

{% include "../../.gitbook/includes/eva-help-hint.md" %}

使用 `pnr/claim.do` 将符合条件的现有航司 PNR 关联到 Atlas。

该操作适用于外部创建的 PNR，不用于从现有 Atlas 订单读取 PNR 数据。

### 常见问题

#### 何时应使用 PNR 认领？

当需要将现有航司 PNR 纳入 Atlas 后续订单处理时使用。

认领前，确认该 PNR 符合当前业务流程的处理条件。

#### PNR 认领与提取有什么区别？

PNR 认领用于关联外部创建的航司 PNR。

PNR 提取用于从现有 Atlas 订单获取 PNR 数据。

#### 认领 PNR 后应做什么？

根据业务流程处理关联后的订单数据。

使用[PNR 认领与提取](../../product-guides/post-booking/pnr-claim-and-extraction.md)了解完整流程和常见用例。

{% openapi-operation spec="atlas-api" path="/pnr/claim.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130709Z&X-Amz-Expires=172800&X-Amz-Signature=c45e97e7189fcd169671b3760c4336c0cd2eb7d48d677787ddce88113a0cc4a3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
