---
description: Atlas API 提取 PNR 端点参考，用于获取 PNR 数据，支持订单恢复、服务和预订后处理。
---

# 提取 PNR

{% include "../../.gitbook/includes/eva-help-hint.md" %}

使用 `extractPnr.do` 从现有 Atlas 订单中获取 PNR 数据。

该端点支持订单恢复、服务处理，以及 Atlas 与航司之间的 PNR 数据同步。

### 常见问题

#### 何时应使用 `extractPnr.do`？

当需要从已有 Atlas 订单检索 PNR 详细信息时使用。

它适用于订单恢复、服务和预订后处理。

#### PNR 提取与认领有什么区别？

PNR 提取用于读取 Atlas 订单关联的 PNR 数据。

PNR 认领用于将外部创建的航司 PNR 关联到 Atlas。

#### 提取 PNR 后应做什么？

根据订单服务或同步流程处理返回的 PNR 数据。

使用[PNR 认领与提取](../../product-guides/post-booking/pnr-claim-and-extraction.md)了解常见用例。

{% openapi-operation spec="atlas-api" path="/extractPnr.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130709Z&X-Amz-Expires=172800&X-Amz-Signature=c45e97e7189fcd169671b3760c4336c0cd2eb7d48d677787ddce88113a0cc4a3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
