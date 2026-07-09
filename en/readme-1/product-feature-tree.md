---
description: Atlas API 产品功能全景图，展示所有核心接口能力与依赖关系
---

# Atlas API 产品功能树

Atlas API 全能力全景图，涵盖搜索、预订、支付、退票、改签等核心业务流程。

---

<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 16px; margin-bottom: 24px;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden; transition: all 0.2s;">
    <div style="height: 4px; background: #1E3A8A;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">A1. 票价查询</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /search.do</div>
      <div style="font-size: 12px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：无（入口接口）</div>
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
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden; transition: all 0.2s;">
    <div style="height: 4px; background: #3B82F6;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">A2. 验价</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /verify.do</div>
      <div style="font-size: 12px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：需先调用票价查询</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">传入 Search 的 routingIdentifier</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">实时价格（原始价 vs 新价）</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">返回 sessionId（用于后续下单）</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">返回 bookingRequirement</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">退改签规则 / 行李额度</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden; transition: all 0.2s;">
    <div style="height: 4px; background: #1E3A8A;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E3A8A; margin-bottom: 4px;">A7. 支付</div>
      <div style="font-family: 'SF Mono', 'Consolas', monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /pay.do</div>
      <div style="font-size: 12px; color: #F97316; font-style: italic; margin-bottom: 6px;">依赖：需先调用创建订单</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Deposit（预存款）支付</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">VCC（虚拟信用卡）支付</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">MoR（商户代收）模式</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">信用卡：Visa / MC / AE / Discover</li>
      </ul>
    </div>
  </div>
</div>
