# 支付与出票

{% include "../../.gitbook/includes/eva-help-hint.md" %}

使用此端点支付已有订单。

发送 `orderNo` 和选定的 `paymentMethod`。

支付成功并不总是意味着出票已经完成。

使用[查询订单](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n)确认最终出票状态。

{% openapi-operation spec="atlas-api" path="/pay.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/6d498c79f43546e63a2289f81c033345c8210830410d2835d33def093c5f3f29.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260708%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260708T131020Z&X-Amz-Expires=172800&X-Amz-Signature=27126ae21ba6c52dbf38f05311990817f1e9c7b7109d7807e10d2e1b9238185d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
