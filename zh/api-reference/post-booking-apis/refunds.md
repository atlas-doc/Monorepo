---
description: Atlas API 退款端点参考，用于获取退款报价、提交退款请求并跟踪退款处理状态。
---

# 退款

{% include "../../.gitbook/includes/eva-help-hint.md" %}

退款标准流程为 `refundQuotation.do` → `refund.do` → `queryRefundOrders.do`。

先获取最新退款报价，再提交退款，并持续查询最终状态。

### 常见问题

#### 何时应使用退款而不是作废？

当作废窗口已过，或订单需要走退款流程时，使用退款。

订单仍符合航司作废条件时，应使用作废路径。

#### 提交退款前应确认什么？

确认原始 `orderNo` 正确、行程信息完整，并且最新退款报价仍然有效。

流程要求时，还应确认出票已完成。

#### 退款流程中应保留哪些标识符？

提交退款时保留最新的 `refundOfferId`。

提交后保留 `refundCode`，并使用 `queryRefundOrders.do` 跟进最终状态。

### 相关指南

使用[退款](../../product-guides/post-booking/refunds.md)了解完整退款流程和资格条件。

订单仍可能作废时，先使用[作废](void.md)确认正确路径。

{% openapi-operation spec="atlas-api" path="/refundQuotation.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130706Z&X-Amz-Expires=172800&X-Amz-Signature=ed831eb627658f05066487da35b6e7847bcd35599e3beb2c0f94e791fb76408c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="atlas-api" path="/refund.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130706Z&X-Amz-Expires=172800&X-Amz-Signature=ed831eb627658f05066487da35b6e7847bcd35599e3beb2c0f94e791fb76408c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="atlas-api" path="/queryRefundOrders.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130706Z&X-Amz-Expires=172800&X-Amz-Signature=ed831eb627658f05066487da35b6e7847bcd35599e3beb2c0f94e791fb76408c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
