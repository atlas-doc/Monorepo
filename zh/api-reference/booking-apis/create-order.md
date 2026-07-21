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

### OTA 随单行李加购

OTA 可在创建机票订单时传入已售行李。

在请求体根级增加可选的 `passengerBaggages` 数组。

不传该字段时，订单按标准流程处理。

Atlas 使用 OTA 传入的规格和售价创建订单。

Atlas 不会用内部行李报价替换这些值。

#### 字段结构

`passengerBaggages` 按乘机人、航段和行李规格嵌套：

* `passengerName`：订单中的乘机人姓名。
* `baggages[].flight`：航班号。Atlas 仅使用此字段匹配航段。
* `baggages[].baggagePrices`：该航段的行李规格与 OTA 售价。

| 字段                 | 类型      | 必填 | 说明                         |
| ------------------ | ------- | -- | -------------------------- |
| `bookSalePrice`    | Decimal | 是  | OTA 向旅客收取的当前航段行李价格。        |
| `bookSaleCurrency` | String  | 是  | 售价币种，例如 `USD`。             |
| `pkgNumber`        | Integer | 是  | 计重制传 `-1`。计件制传正整数。不要传 `0`。 |
| `weight`           | Integer | 是  | 收费行李总重量，单位为 kg。            |
| `baggageType`      | Integer | 否  | `0` 为托运行李，也是默认值。`1` 为手提行李。 |

`cabin`、`depTime`、`fromAirport` 和 `toAirport` 为兼容字段。

它们不参与航段匹配或校验。

{% hint style="warning" %}
同一订单存在相同航班号的多个航段时，不要传入随单行李。

该场景无法可靠区分行李所属航段。
{% endhint %}

#### 请求示例

```json
{
  "sessionId": "6822e239-0cc7-4134-8956-b1a618fd0dcd",
  "passengers": [
    {
      "name": "ZHANG/SAN",
      "passengerType": 0,
      "gender": "M"
    }
  ],
  "passengerBaggages": [
    {
      "passengerName": "ZHANG/SAN",
      "baggages": [
        {
          "flight": "JT786",
          "baggagePrices": [
            {
              "bookSalePrice": 50.00,
              "bookSaleCurrency": "USD",
              "pkgNumber": -1,
              "weight": 20,
              "baggageType": 0
            }
          ]
        }
      ]
    }
  ],
  "contact": {
    "name": "ZHANG/SAN"
  }
}
```

#### 航司校验与确认

航司在履约时校验实际可购买的行李规格与价格。

航司实际价格不高于 OTA 售价时，Atlas 自动加购并出票。

`309` 表示该 OTA 随单行李规格不符合航司要求。

`3011` 表示航司实际价格高于 OTA 售价。

收到 `3011` 后，请在 30 分钟内取消订单或确认亏出。

可调用 `POST /confirmBaggageLoss.do`，并传入 `orderNo` 完成确认。

超时未确认的订单会自动取消。

请参阅 [OTA 随单行李加购](../../product-guides/extensions-and-integrations/special-integrations/中国OTA随单行李加购.md)，了解通知、结算和完整确认流程。

{% openapi-operation spec="atlas-api" path="/order.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260721%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260721T032533Z&X-Amz-Expires=172800&X-Amz-Signature=52680d754ae4e6ac3f75e968b910582a63084a5114ab8d19d3f620d78264d113&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
