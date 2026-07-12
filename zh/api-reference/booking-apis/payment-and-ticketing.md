---
description: Atlas API 支付与出票端点参考，用于支付订单、处理重试安全，并跟进最终出票状态。
---

# 支付与出票

{% include "../../.gitbook/includes/eva-help-hint.md" %}

使用此端点支付已有订单。

发送 `orderNo` 和选定的 `paymentMethod`。

支付成功并不总是意味着出票已经完成。

使用[查询订单](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n)确认最终出票状态。

{% openapi-operation spec="atlas-api" path="/pay.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130708Z&X-Amz-Expires=172800&X-Amz-Signature=4374947ae0632333ad3b7840636e7638e090f48e9f0b320f1cb7ed976813a7a3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
