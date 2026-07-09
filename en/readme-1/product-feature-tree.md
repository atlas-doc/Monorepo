---
description: Atlas API 产品功能全景图，展示所有核心接口能力与依赖关系
---

# Atlas API 产品功能树

Atlas API 全能力全景图，涵盖搜索、预订、支付、退票、改签等核心业务流程。

---


## 产品场景总览

---

Atlas API 以三大搜索入口为起点，串联五个核心业务阶段，共提供 26 个 API 接口

<div style="display: flex; gap: 16px; margin-bottom: 24px; flex-wrap: wrap;">
  <div style="flex: 1; min-width: 140px; background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; padding: 20px; text-align: center;">
    <div style="font-size: 32px; font-weight: 800; color: #1E3A8A; line-height: 1.1;">3</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">搜索入口</div>
  </div>
  <div style="flex: 1; min-width: 140px; background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; padding: 20px; text-align: center;">
    <div style="font-size: 32px; font-weight: 800; color: #1E3A8A; line-height: 1.1;">5</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">核心阶段</div>
  </div>
  <div style="flex: 1; min-width: 140px; background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; padding: 20px; text-align: center;">
    <div style="font-size: 32px; font-weight: 800; color: #1E3A8A; line-height: 1.1;">26</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">API 接口</div>
  </div>
  <div style="flex: 1; min-width: 140px; background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; padding: 20px; text-align: center;">
    <div style="font-size: 32px; font-weight: 800; color: #1E3A8A; line-height: 1.1;">8</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">调用链路</div>
  </div>
</div>


<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 16px; margin-bottom: 32px;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #1E3A8A;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">Search · 标准搜索</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /search.do</div>
      <div style="font-size: 13px; color: #0F172A; line-height: 1.5;">通用场景，支持单程/往返、多航司过滤、航班号精确搜索、多运价舱位</div>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #3B82F6;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">GetOffer · 直接报价</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /getOffers.do</div>
      <div style="font-size: 13px; color: #0F172A; line-height: 1.5;">指定航班直接获取报价，跳过 Search，提高 L2B 转化率</div>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #F97316;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">SmartSearch · 智能搜索</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /smartSearch.do</div>
      <div style="font-size: 13px; color: #0F172A; line-height: 1.5;">仅限 TMC，覆盖 Search API 未覆盖的航线与时段</div>
    </div>
  </div>
</div>

## A. 标准预订流程

---

<div style="font-size: 18px; font-weight: 700; color: #3B82F6; margin: 24px 0 12px;">标准预订 · 8 步流程</div>

<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 16px; margin-bottom: 24px;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #1E3A8A;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">A1. 票价查询</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /search.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：无（入口接口）</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">行程类型（单程 / 往返）</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">乘客数（成人 / 儿童 / 婴儿）</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">出发 / 到达城市或机场 IATA 码</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">出发 / 返回日期 (yyyyMMdd)</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">指定航司 / 航班号（可选过滤）</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">多运价舱位、结算币种</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #3B82F6;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">A2. 验价</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /verify.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：需先调用票价查询</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">传入 Search 的 routingIdentifier</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">实时价格（原始价 vs 新价）</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">返回 sessionId（用于后续下单）</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">返回 bookingRequirement</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">退改签规则 / 行李额度</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #3B82F6;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">A3. 预订</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /createOrder.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：需先调用验价</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">传入 Verify 返回的 sessionId</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">乘客信息（姓名、生日证件）</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">联系人信息（邮箱、电话）</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">内部订单号（便于对账）</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">保险、附加服务预订</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #10B981;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">A4. 支付</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /pay.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：需先调用创建订单</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Deposit（预存款）支付</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">VCC（虚拟信用卡）支付</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">MoR（商户代收）模式</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">信用卡：Visa / MC / AE / Discover</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #10B981;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">A5. 订单查询</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /retrieveOrder.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：支付成功后</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">查询订单状态、票号</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">支付状态、出票状态</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">PNR 信息、乘客信息</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">附加服务信息</li>
      </ul>
    </div>
  </div>
</div>

## B. GetOffer 直接报价

---

<div style="font-size: 18px; font-weight: 700; color: #3B82F6; margin: 24px 0 12px;">跳过搜索，直接报价 · 提高转化率</div>

<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 16px; margin-bottom: 24px;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #3B82F6;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">B1. 直接获取报价</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /getOffers.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：无（第二入口）</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">指定航司、航班号、舱位</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">出发日期、出发/到达机场</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">返回包含 sessionId</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">可直接用于后续 CreateOrder</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #3B82F6;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">B2. GetOffer 价格查询</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /getOfferPrice.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：GetOffer</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">传入 GetOffer 的 offerId</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">获取实时精确报价</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">用于价格展示与比价</li>
      </ul>
    </div>
  </div>
</div>

## C. SmartSearch 智能搜索

---

<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 16px; margin-bottom: 24px;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #F97316;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">C1. 智能搜索</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /smartSearch.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：需 TMC 权限</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">覆盖 Search API 未覆盖的航线与时段</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">TMC 场景增强版搜索</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">返回 routingIdentifier</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #3B82F6;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">C2. 价格对比搜索</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /priceCompareSearch.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：无（比价入口）</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">多航班比价搜索</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">灵活日期比价</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">价格日历视图</li>
      </ul>
    </div>
  </div>
</div>

## D. 退票 & 改签

---

<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 16px; margin-bottom: 24px;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #EF4444;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">D1. 退票</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /refund.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：已出票订单</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">支持部分退票</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">支持自愿 / 非自愿退票</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">退票金额计算</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">退票状态查询</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #EF4444;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">D2. RegenerateOrder</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /regenerateOrder.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：已出票订单</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">订单重新生成</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">改签场景使用</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">保留原订单信息</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #EF4444;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">D3. 停止出票</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /stopTicketIssuance.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：支付成功未出票</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">紧急停止出票流程</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">支付后快速响应前</li>
      </ul>
    </div>
  </div>
</div>

## E. 附加服务

---

<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 16px; margin-bottom: 24px;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #10B981;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">E1. 行李服务</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /getLuggage.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：Verify 后</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">行李产品查询</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">多等级可选</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">CreateOrder 时预订</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #10B981;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">E2. 选座服务</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /seatAvailability.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：Verify 后</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">座位图展示</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">座位价格查询</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">CreateOrder 时预订</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #10B981;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">E3. 预订后附加服务</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /bookAncillary.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：已出票</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">出票后追加行李</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">出票后选座</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">支付附加费单独支付</li>
      </ul>
    </div>
  </div>
</div>

## F. Webhook 通知管理

---

<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 16px; margin-bottom: 24px;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #8B5CF6;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">F1. 通知注册</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /webhook/register.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">注册回调 URL</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">选择通知类型</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">验签密钥配置</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #8B5CF6;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">F2. 事件查询</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /incident/query.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">航变事件查询</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">按时间范围</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">航班状态更新</li>
      </ul>
    </div>
  </div>
</div>

### Webhook 事件类型

<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 12px; margin-bottom: 20px;">
  <div style="background: #FFFFFF; border-radius: 8px; border: 1px solid #CBD5E1; padding: 14px; border-left: 3px solid #3B82F6;">
    <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 12px; font-weight: 600; color: #3B82F6;">TICKETING_COMPLETE</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">出票完成通知</div>
  </div>
  <div style="background: #FFFFFF; border-radius: 8px; border: 1px solid #CBD5E1; padding: 14px; border-left: 3px solid #EF4444;">
    <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 12px; font-weight: 600; color: #EF4444;">VOID_NOTIFICATION</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">订单作废通知</div>
  </div>
  <div style="background: #FFFFFF; border-radius: 8px; border: 1px solid #CBD5E1; padding: 14px; border-left: 3px solid #F97316;">
    <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 12px; font-weight: 600; color: #F97316;">SCHEDULE_CHANGE</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">航班时刻变更通知</div>
  </div>
  <div style="background: #FFFFFF; border-radius: 8px; border: 1px solid #CBD5E1; padding: 14px; border-left: 3px solid #10B981;">
    <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 12px; font-weight: 600; color: #10B981;">AIRLINE_STATUS_UPDATE</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">航司状态更新通知</div>
  </div>
</div>

## G. 订单列表 & PNR 管理

---

<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 16px; margin-bottom: 24px;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #0EA5E9;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">G1. 订单列表</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /orderList.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">按创建时间范围</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">按订单状态过滤</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">分页查询支持</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #0EA5E9;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">G2. PNR 提取</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /extractPnr.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">提取 PNR 原文</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">E-ticket 电子客票</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #0EA5E9;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">G3. PNR Claim</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /pnrClaim.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">认领 PNR 归属</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">订单绑定</li>
      </ul>
    </div>
  </div>
</div>

## H. 工具类接口

---

<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 16px; margin-bottom: 24px;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #0891B2;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">H1. 账户余额</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /balance.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">查询账户余额</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">多币种支持</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #0891B2;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">H2. 航班数据导出</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /flightDataFeed.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">全量航线数据</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">增量数据同步</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #0891B2;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">H3. 邮件查询</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /emailQuery.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">邮件内容查询</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">邮件附件下载</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #0891B2;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">H4. aTrip Token</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /atripToken.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">获取访问令牌</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Token 刷新机制</li>
      </ul>
    </div>
  </div>
</div>

## 依赖关系总表

---

<div style="overflow-x: auto; margin-bottom: 24px;">
  <table style="width: 100%; border-collapse: collapse; font-size: 13px;">
    <thead>
      <tr>
        <th style="background: #1E3A8A; color: #FFFFFF; padding: 10px 12px; text-align: left; font-weight: 600;">API 接口</th>
        <th style="background: #1E3A8A; color: #FFFFFF; padding: 10px 12px; text-align: left; font-weight: 600;">依赖接口</th>
        <th style="background: #1E3A8A; color: #FFFFFF; padding: 10px 12px; text-align: left; font-weight: 600;">关键传递参数</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1; background: #F8FAFC;">search.do</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1; background: #F8FAFC;">-</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1; background: #F8FAFC;">routingIdentifier → Verify</td>
      </tr>
      <tr>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1;">verify.do</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1;">search.do</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1;">sessionId → CreateOrder / 退改签规则 / 行李额度</td>
      </tr>
      <tr>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1; background: #F8FAFC;">createOrder.do</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1; background: #F8FAFC;">verify.do / getOffers.do</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1; background: #F8FAFC;">sessionId, bookingRequirement</td>
      </tr>
      <tr>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1;">getOffers.do</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1;">-</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1;">offerId, sessionId</td>
      </tr>
      <tr>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1; background: #F8FAFC;">pay.do</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1; background: #F8FAFC;">createOrder.do</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1; background: #F8FAFC;">orderNumber</td>
      </tr>
      <tr>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1;">refund.do</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1;">retrieveOrder.do</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1;">orderNumber, ticketNumber</td>
      </tr>
      <tr>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1; background: #F8FAFC;">getLuggage.do</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1; background: #F8FAFC;">verify.do</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1; background: #F8FAFC;">sessionId</td>
      </tr>
      <tr>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1;">seatAvailability.do</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1;">verify.do</td>
        <td style="padding: 8px 12px; border-bottom: 1px solid #CBD5E1;">sessionId</td>
      </tr>
    </tbody>
  </table>
</div>
