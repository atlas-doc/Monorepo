---
description: Atlas API getOfferPrice.do 端点参考，用于履约路径的报价定价，并启动限时支付与出票流程。
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

# Get Offer Price

{% include "../../.gitbook/includes/eva-help-hint.md" %}

使用 `核价出票` 作为 `getOfferPrice.do` 的文档名称。

此端点启动履约流程。

当你需要履约特定的定价，并可以在 `order.do` 后立即进行支付时使用它。

将返回的上下文视为履约专用。

有关请求限制详情，请使用 [API 请求限制](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV)。

{% openapi-operation spec="atlas-api" path="/getOfferPrice.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130709Z&X-Amz-Expires=172800&X-Amz-Signature=c45e97e7189fcd169671b3760c4336c0cd2eb7d48d677787ddce88113a0cc4a3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
