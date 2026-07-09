---
description: Atlas API 产品功能全景图，展示所有核心接口能力与依赖关系
---

# Atlas API 产品功能树

Atlas API 全能力全景图，涵盖搜索、预订、支付、退票、改签等核心业务流程。

---

{% raw %}
<style>
  :root {
    --primary: #1E3A8A;
    --secondary: #3B82F6;
    --accent: #F97316;
    --bg: #EFF6FF;
    --text: #1E40AF;
    --dark: #0F172A;
    --gray: #64748B;
    --light: #F8FAFC;
    --border: #CBD5E1;
    --success: #10B981;
    --white: #FFFFFF;
  }
  .card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
    gap: 16px;
    margin-bottom: 24px;
  }
  .card {
    background: var(--white);
    border-radius: 10px;
    border: 1px solid var(--border);
    overflow: hidden;
    transition: all 0.2s;
  }
  .card:hover {
    box-shadow: 0 4px 16px rgba(30, 58, 138, 0.08);
  }
  .card-top {
    height: 4px;
  }
  .card-body {
    padding: 16px;
  }
  .card-title {
    font-size: 15px;
    font-weight: 700;
    color: var(--primary);
    margin-bottom: 4px;
  }
  .card-api {
    font-family: 'SF Mono', 'Consolas', monospace;
    font-size: 11px;
    color: var(--secondary);
    margin-bottom: 8px;
  }
  .card-desc {
    font-size: 13px;
    color: var(--dark);
    line-height: 1.5;
  }
  .card-dep {
    font-size: 12px;
    color: var(--accent);
    font-style: italic;
    margin-bottom: 6px;
  }
  .card ul {
    padding-left: 16px;
    margin-top: 6px;
  }
  .card li {
    font-size: 12px;
    color: var(--dark);
    line-height: 1.6;
  }
</style>

<div class="card-grid">
  <div class="card">
    <div class="card-top" style="background:var(--primary)"></div>
    <div class="card-body">
      <div class="card-title">A1. 票价查询</div>
      <div class="card-api">POST /search.do</div>
      <div class="card-dep">依赖：无（入口接口）</div>
      <ul>
        <li>行程类型（单程 / 往返）</li>
        <li>乘客数（成人 / 儿童 / 婴儿）</li>
        <li>出发 / 到达城市或机场 IATA 码</li>
        <li>出发 / 返回日期 (yyyyMMdd)</li>
        <li>指定航司 / 航班号（可选过滤）</li>
        <li>多运价舱位、结算币种</li>
      </ul>
    </div>
  </div>
  <div class="card">
    <div class="card-top" style="background:var(--secondary)"></div>
    <div class="card-body">
      <div class="card-title">A2. 验价</div>
      <div class="card-api">POST /verify.do</div>
      <div class="card-dep">依赖：需先调用票价查询</div>
      <ul>
        <li>传入 Search 的 routingIdentifier</li>
        <li>实时价格（原始价 vs 新价）</li>
        <li>返回 sessionId（用于后续下单）</li>
        <li>返回 bookingRequirement</li>
        <li>退改签规则 / 行李额度</li>
      </ul>
    </div>
  </div>
  <div class="card">
    <div class="card-top" style="background:var(--primary)"></div>
    <div class="card-body">
      <div class="card-title">A7. 支付</div>
      <div class="card-api">POST /pay.do</div>
      <div class="card-dep">依赖：需先调用创建订单</div>
      <ul>
        <li>Deposit（预存款）支付</li>
        <li>VCC（虚拟信用卡）支付</li>
        <li>MoR（商户代收）模式</li>
        <li>信用卡：Visa / MC / AE / Discover</li>
      </ul>
    </div>
  </div>
</div>
{% endraw %}

---

## 方式二：使用 include（仅限代码展示）

`{% include %}` 适合展示代码文件，不适合渲染网页：

```markdown
{% include "/.gitbook/assets/some-code.js" %}
```

---

## 关键结论

| 方案 | 是否渲染为网页 | 适用场景 |
|------|:--------------:|----------|
| **`{% raw %} HTML 内容 {% endraw %}`** | ✅ **完美渲染** | 产品功能树、流程图、交互式组件 |
| **`{% include "file.html" %}`** | ❌ 显示为代码 | 展示代码文件 |
| **iframe** | ✅ 渲染 | 外部托管的网页 |

---

## 为什么这样有效？

GitBook 在处理 Markdown 时：
1. 遇到 `{% raw %}` 标签，会跳过内部的 Markdown 解析
2. 直接把内部的 HTML/CSS 传给浏览器渲染
3. 所以所有样式、交互、动画都会完美保留

✅ **完整交互**：所有悬停效果、跳转、动画完美保留  
✅ **可搜索**：HTML 文本可被 GitBook 全文索引  
✅ **可复制**：流程图文本可以直接复制粘贴  
✅ **响应式**：自动适配 GitBook 明暗主题和屏幕尺寸
