---
description: 确认 OTA 随单行李变价亏出，并在 30 分钟内继续履约出票。
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

# 确认行李损失

{% include "../../.gitbook/includes/eva-help-hint.md" %}

用于处理 OTA 随单行李加购中航司报价高于 OTA 售价的情况。

收到 `3011` 后，传入 `orderNo` 确认亏出，系统继续完成行李加购和出票。

请在 30 分钟内完成确认。超时未确认的订单会自动取消。

完整的接入规则、异常处理和结算方式，请参阅 [OTA 随单行李加购](../../product-guides/extensions-and-integrations/special-integrations/中国OTA随单行李加购.md)。

{% openapi-operation spec="atlas-api" path="/confirmBaggageLoss.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/e19fea306b1e50097f74f5576d380a3707ddaa114d2a41b1e4e4876229ee1f13.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260721%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260721T080301Z&X-Amz-Expires=172800&X-Amz-Signature=1ea5c17e49ff897b205504f8486b911c2c0cf7b4b037fe4cfa368aadd98aa352&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
