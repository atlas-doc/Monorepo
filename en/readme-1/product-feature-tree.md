---
description: Atlas API 产品功能全景图，展示所有核心接口能力与依赖关系
---

# Atlas API 产品功能树

Atlas API 全能力全景图，涵盖搜索、预订、支付、退票、改签等核心业务流程。

---

## 📊 产品场景总览

> Atlas API 以三大搜索入口为起点，串联五个核心业务阶段，共提供 **26 个 API 接口**

| 指标 | 数量 | 说明 |
|------|------|------|
| 🔍 搜索入口 | 3 | Search, GetOffer, SmartSearch |
| 🚀 核心阶段 | 5 | 搜索 → 验价 → 预订 → 支付 → 出票后 |
| 📡 API 接口 | 26 | 全量功能覆盖 |
| 🔗 调用链路 | 8 | 不同场景组合 |

---

### 三大搜索入口

| 编号 | API 名称 | 接口 | 核心能力 |
|------|---------|------|---------|
| 🔵 | **Search · 标准搜索** | `POST /search.do` | 通用场景，支持单程/往返、多航司过滤、航班号精确搜索、多运价舱位 |
| 🔷 | **GetOffer · 直接报价** | `POST /getOffers.do` | 指定航班直接获取报价，跳过 Search，提高 L2B 转化率 |
| 🟠 | **SmartSearch · 智能搜索** | `POST /smartSearch.do` | 仅限 TMC，覆盖 Search API 未覆盖的航线与时段 |

---

## 🅰️ 标准预订流程

> 完整 8 步标准预订流程

### 流程：搜索 → 验价 → 选座/行李 → 预订 → 支付 → 出票 → 订单查询

| 步骤 | API | 依赖 | 核心功能 |
|------|-----|------|---------|
| **A1** | **票价查询**<br>`POST /search.do` | 无（入口接口） | ✅ 行程类型（单程 / 往返）<br>✅ 乘客数（成人 / 儿童 / 婴儿）<br>✅ 出发 / 到达城市或机场 IATA 码<br>✅ 出发 / 返回日期 (yyyyMMdd)<br>✅ 指定航司 / 航班号（可选过滤）<br>✅ 多运价舱位、结算币种 |
| **A2** | **验价**<br>`POST /verify.do` | 需先调用票价查询 | ✅ 传入 Search 的 routingIdentifier<br>✅ 实时价格（原始价 vs 新价）<br>✅ 返回 sessionId（用于后续下单）<br>✅ 返回 bookingRequirement<br>✅ 退改签规则 / 行李额度 |
| **A3** | **预订**<br>`POST /createOrder.do` | 需先调用验价 | ✅ 传入 Verify 返回的 sessionId<br>✅ 乘客信息（姓名、生日证件）<br>✅ 联系人信息（邮箱、电话）<br>✅ 内部订单号（便于对账）<br>✅ 保险、附加服务预订 |
| **A4** | **支付**<br>`POST /pay.do` | 需先调用创建订单 | ✅ Deposit（预存款）支付<br>✅ VCC（虚拟信用卡）支付<br>✅ MoR（商户代收）模式<br>✅ 信用卡：Visa / MC / AE / Discover |
| **A5** | **订单查询**<br>`POST /retrieveOrder.do` | 支付成功后 | ✅ 查询订单状态、票号<br>✅ 支付状态、出票状态<br>✅ PNR 信息、乘客信息<br>✅ 附加服务信息 |

---

## 🅱️ GetOffer 直接报价

> 跳过搜索，直接报价 · 提高转化率

| 步骤 | API | 依赖 | 核心功能 |
|------|-----|------|---------|
| **B1** | **直接获取报价**<br>`POST /getOffers.do` | 无（第二入口） | ✅ 指定航司、航班号、舱位<br>✅ 出发日期、出发/到达机场<br>✅ 返回包含 sessionId<br>✅ 可直接用于后续 CreateOrder |
| **B2** | **GetOffer 价格查询**<br>`POST /getOfferPrice.do` | GetOffer | ✅ 传入 GetOffer 的 offerId<br>✅ 获取实时精确报价<br>✅ 用于价格展示与比价 |

---

## 🅲 SmartSearch 智能搜索

> TMC 增强版搜索能力

| 步骤 | API | 依赖 | 核心功能 |
|------|-----|------|---------|
| **C1** | **智能搜索**<br>`POST /smartSearch.do` | 需 TMC 权限 | ✅ 覆盖 Search API 未覆盖的航线与时段<br>✅ TMC 场景增强版搜索<br>✅ 返回 routingIdentifier |
| **C2** | **价格对比搜索**<br>`POST /priceCompareSearch.do` | 无（比价入口） | ✅ 多航班比价搜索<br>✅ 灵活日期比价<br>✅ 价格日历视图 |

---

## 🅳 退票 & 改签

> 出票后订单维护

| 步骤 | API | 依赖 | 核心功能 |
|------|-----|------|---------|
| **D1** | **退票**<br>`POST /refund.do` | 已出票订单 | ✅ 支持部分退票<br>✅ 支持自愿 / 非自愿退票<br>✅ 退票金额计算<br>✅ 退票状态查询 |
| **D2** | **RegenerateOrder**<br>`POST /regenerateOrder.do` | 已出票订单 | ✅ 订单重新生成<br>✅ 改签场景使用<br>✅ 保留原订单信息 |
| **D3** | **停止出票**<br>`POST /stopTicketIssuance.do` | 支付成功未出票 | ✅ 紧急停止出票流程<br>✅ 支付后快速响应前 |

---

## 🅴 附加服务

> 行李、选座等增值服务

| 步骤 | API | 依赖 | 核心功能 |
|------|-----|------|---------|
| **E1** | **行李服务**<br>`POST /getLuggage.do` | Verify 后 | ✅ 行李产品查询<br>✅ 多等级可选<br>✅ CreateOrder 时预订 |
| **E2** | **选座服务**<br>`POST /seatAvailability.do` | Verify 后 | ✅ 座位图展示<br>✅ 座位价格查询<br>✅ CreateOrder 时预订 |
| **E3** | **预订后附加服务**<br>`POST /bookAncillary.do` | 已出票 | ✅ 出票后追加行李<br>✅ 出票后选座<br>✅ 支付附加费单独支付 |

---

## 🅵 Webhook 通知管理

> 事件推送与回调

| 步骤 | API | 核心功能 |
|------|-----|---------|
| **F1** | **通知注册**<br>`POST /webhook/register.do` | ✅ 注册回调 URL<br>✅ 选择通知类型<br>✅ 验签密钥配置 |
| **F2** | **事件查询**<br>`POST /incident/query.do` | ✅ 航变事件查询<br>✅ 按时间范围<br>✅ 航班状态更新 |

### Webhook 事件类型

| 事件代码 | 说明 |
|---------|------|
| `TICKETING_COMPLETE` | ✅ 出票完成通知 |
| `VOID_NOTIFICATION` | ❌ 订单作废通知 |
| `SCHEDULE_CHANGE` | ⚠️ 航班时刻变更通知 |
| `AIRLINE_STATUS_UPDATE` | 📢 航司状态更新通知 |
| `EMAIL_NOTIFICATION` | 📧 邮件通知 |
| `INCIDENT_NOTIFICATION` | 🔔 事件通知 |

---

## 🅶 订单列表 & PNR 管理

> 订单查询与 PNR 操作

| 步骤 | API | 核心功能 |
|------|-----|---------|
| **G1** | **订单列表**<br>`POST /orderList.do` | ✅ 按创建时间范围<br>✅ 按订单状态过滤<br>✅ 分页查询支持 |
| **G2** | **PNR 提取**<br>`POST /extractPnr.do` | ✅ 提取 PNR 原文<br>✅ E-ticket 电子客票 |
| **G3** | **PNR Claim**<br>`POST /pnrClaim.do` | ✅ 认领 PNR 归属<br>✅ 订单绑定 |

---

## 🅷 工具类接口

> 辅助功能接口

| 步骤 | API | 核心功能 |
|------|-----|---------|
| **H1** | **账户余额**<br>`POST /balance.do` | ✅ 查询账户余额<br>✅ 多币种支持 |
| **H2** | **航班数据导出**<br>`POST /flightDataFeed.do` | ✅ 全量航线数据<br>✅ 增量数据同步 |
| **H3** | **邮件查询**<br>`POST /emailQuery.do` | ✅ 邮件内容查询<br>✅ 邮件附件下载 |
| **H4** | **aTrip Token**<br>`POST /atripToken.do` | ✅ 获取访问令牌<br>✅ Token 刷新机制 |

---

## 🔗 API 依赖关系总表

| API 接口 | 依赖接口 | 关键传递参数 |
|---------|---------|-------------|
| `search.do` | - | `routingIdentifier` → Verify |
| `verify.do` | `search.do` | `sessionId` → CreateOrder / 退改签规则 / 行李额度 |
| `createOrder.do` | `verify.do` / `getOffers.do` | `sessionId`, `bookingRequirement` |
| `getOffers.do` | - | `offerId`, `sessionId` |
| `pay.do` | `createOrder.do` | `orderNumber` |
| `refund.do` | `retrieveOrder.do` | `orderNumber`, `ticketNumber` |
| `getLuggage.do` | `verify.do` | `sessionId` |
| `seatAvailability.do` | `verify.do` | `sessionId` |
| `bookAncillary.do` | `retrieveOrder.do` | `orderNumber` |
| `regenerateOrder.do` | `retrieveOrder.do` | `orderNumber` |

---

### 📝 说明

- **入口接口**：`search.do`, `getOffers.do`, `smartSearch.do`
- **必走流程**：Search/GetOffer → Verify → CreateOrder → Pay → RetrieveOrder
- **可选附加**：Luggage / Seat / Ancillary
- **出票后操作**：Refund / Regenerate / BookAncillary / OrderList
- **回调通知**：Webhook 注册 + 事件接收
