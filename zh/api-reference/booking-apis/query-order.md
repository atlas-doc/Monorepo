---
description: Atlas API 查询订单端点参考，用于获取订单状态、出票进度、航司 PNR 和最终订单详情。
---

# 查询订单

{% include "../../.gitbook/includes/eva-help-hint.md" %}

使用此端点在 `order.do` 或 `pay.do` 后读取最新订单状态。

在此处检查 `orderStatus`、`ticketStatus`、航司 PNR 详情和票号。

{% openapi-operation spec="atlas-api" path="/queryOrderDetails.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130707Z&X-Amz-Expires=172800&X-Amz-Signature=299ebce0e5dadff16e59880204101597efad717e17104e120e224687194db559&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
