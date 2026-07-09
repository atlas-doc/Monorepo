---
description: 展示如何在 GitBook 中嵌入 HTML 产品功能树
---

# Atlas API 产品功能树

本文档演示如何在 GitBook 中嵌入交互式 HTML 产品功能树。

---

## 方式一：使用 include 引入（推荐）

把独立的 HTML 文件放在 `.gitbook/assets/` 目录，然后通过 `include` 引用：

```markdown
{% include "/.gitbook/assets/product-feature-tree.html" %}
```

**效果预览：**

{% include "/.gitbook/assets/product-feature-tree.html" %}

---

## 方式二：直接写 HTML 到 Markdown

对于简单的 HTML，可以直接在 Markdown 中写：

```markdown
{% raw %}
<div style="background: #f8fafc; padding: 20px; border-radius: 8px;">
  <h3>产品功能卡片</h3>
  <ul>
    <li>✓ 票价查询 - /search.do</li>
    <li>✓ 预订流程 - /order.do</li>
    <li>✓ 支付出票 - /pay.do</li>
  </ul>
</div>
{% endraw %}
```

**效果预览：**

{% raw %}
<div style="background: #f8fafc; padding: 20px; border-radius: 8px;">
  <h3>产品功能卡片</h3>
  <ul>
    <li>✓ 票价查询 - /search.do</li>
    <li>✓ 预订流程 - /order.do</li>
    <li>✓ 支付出票 - /pay.do</li>
  </ul>
</div>
{% endraw %}

---

## 方式三：使用 iframe（适合外部链接）

如果 HTML 托管在其他地方，可以用 iframe：

```markdown
<iframe src="https://example.com/product-tree.html" 
        style="width: 100%; height: 600px; border: none;">
</iframe>
```

---

## 方案对比

| 方案 | 推荐度 | 适用场景 |
|------|:------:|----------|
| **include + 独立 HTML** | ⭐⭐⭐⭐⭐ | 复杂交互、多页面复用 |
| **直接写 HTML** | ⭐⭐⭐ | 简单卡片、小工具 |
| **iframe** | ⭐⭐ | 外部托管内容 |

---

## 优势

✅ **完整交互**：所有悬停效果、跳转、动画完美保留  
✅ **可搜索**：HTML 文本可被 GitBook 全文索引  
✅ **可复制**：流程图文本可以直接复制粘贴  
✅ **版本管理**：HTML 文件随文档一起 Git 管理  
✅ **响应式**：自动适配 GitBook 明暗主题和屏幕尺寸
