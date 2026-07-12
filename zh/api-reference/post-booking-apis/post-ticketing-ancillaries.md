---
description: Atlas API 出票后附加服务端点参考，用于管理已出票订单的可用附加服务和相关操作。
---

# 出票后附加服务

{% include "../../.gitbook/includes/eva-help-hint.md" %}

使用出票后附加服务 API 为已出票订单查询和购买行李。

先使用 `postBookingAncillarySearch.do` 查询可用产品，再使用 `postBookingAncillaryOrder.do` 创建订单。

### 常见问题

#### 出票后可以添加哪些附加服务？

当前仅支持出票后添加行李。

不支持出票后的座位选择。

#### 出票后行李的标准流程是什么？

先搜索已出票订单可用的附加服务。

然后使用选定的产品代码创建附加服务订单。

#### 联程航班如何选择行李？

同一方向的所有联程航段必须使用一致的行李选择。

去程和回程可以使用不同的行李选择。

### 相关指南

使用[出票后附加服务指南](../../product-guides/post-booking/post-ticketing-ancillaries.md)了解适用范围和完整流程。

### 联程航班的行李选择

辅助服务搜索可能按航段返回行李选项。

对于同一方向的联程航班，请在所有连接的航段上保持行李选择一致。

去程和回程仍可使用不同的行李选择。

如果在一个连接方向内行李选择不同，辅助服务订单验证可能会拒绝该请求。

{% openapi-operation spec="atlas-api" path="/postBookingAncillarySearch.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130706Z&X-Amz-Expires=172800&X-Amz-Signature=ed831eb627658f05066487da35b6e7847bcd35599e3beb2c0f94e791fb76408c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="atlas-api" path="/postBookingAncillaryOrder.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T130706Z&X-Amz-Expires=172800&X-Amz-Signature=ed831eb627658f05066487da35b6e7847bcd35599e3beb2c0f94e791fb76408c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
