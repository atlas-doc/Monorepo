---
description: Atlas API 创建订单端点参考，用于提交旅客、联系人和附加服务数据以建立待支付订单。
---

# 创建订单

{% include "../../.gitbook/includes/eva-help-hint.md" %}

使用此端点在验证后创建预订。

它使用当前的 `sessionId`，并返回 `pay.do` 和订单后续操作使用的 `orderNo`。

### 联程航班的行李

Atlas 可能按航段返回行李选项。

对于同一方向的联程航班，请在所有连接的航段上保持行李选择一致。

如果去程连接航段使用不同的行李选择，或回程连接航段使用不同的行李选择，订单创建可能失败并返回 `307`。

去程和回程仍可使用不同的行李选择。

使用[验证](../../product-guides/booking/booking-step-guides/verify.md)作为 `bookingRequirement` 和当前 `sessionId` 的权威来源。

### 中国 OTA 随单行李加购

对于中国 OTA 随单行李加购场景，您可以在请求体中传入 `passengerBaggages` 数组，携带 OTA 自有行李规格与价格。Atlas 会直接使用您传入的价格创建订单，并使用航司实际价格进行校验。

完整集成文档请参考：[中国 OTA 随单行李加购](../../../product-guides/extensions-and-integrations/special-integrations/中国OTA随单行李加购.md)

{% openapi-operation spec="atlas-api" path="/order.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130707Z&X-Amz-Expires=172800&X-Amz-Signature=299ebce0e5dadff16e59880204101597efad717e17104e120e224687194db559&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
