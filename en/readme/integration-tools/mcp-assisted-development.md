---
description: >-
  Use GitBook MCP to find workflows, understand endpoints, and speed up Atlas
  API integration.
---

# MCP-Assisted Development

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use GitBook MCP to speed up Atlas API development.

It helps you find the right pages, understand the flow, and narrow down the next step faster.

If you want a packaged assistant setup, use [Atlas AI Assistant Skill](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/JeSfAw1uWsyn9tGwrTFH).

### When to use MCP

Use MCP when you need to:

* find the correct API flow for a task
* understand which identifier is needed next
* compare similar APIs such as `search.do` and `getOffer.do`
* locate the right troubleshooting page for an error
* move faster in sandbox without guessing

### What MCP is best at

MCP works best as a docs assistant during development.

Use it to:

* map the booking flow from `Search` to `Pay`
* identify which page explains a field or status
* find related guides for webhooks, refunds, or utility APIs
* narrow down which page to open before coding

### Recommended Atlas use cases

#### Start a sandbox build

Ask MCP to outline the minimum sandbox flow.

Then validate against these pages:

* [Sandbox Development](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Xs5C4xGnhQl0A2GNjlwv)
* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [API Reference](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/LfT8Y3jMIGXTnxwihZhV)

#### Move through the booking flow

Use MCP to confirm the next step after each successful call.

Typical sequence:

* `Search` → keep `routingIdentifier`
* `Verify` → keep `sessionId`
* `Create Order` → keep `orderNo`
* `Payment & Ticketing` → poll and confirm final status

#### Troubleshoot faster

Use MCP to route errors to the right troubleshooting section.

Good starting points:

* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)
* [FAQs](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/eSEVUFqqFzApLBAckuJD)
* [Webhook Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/1kDgZtL5TYuOLUmAxRd6)

### Prompt patterns that work well

Use short, task-based prompts.

Examples:

* Show the minimum Atlas sandbox booking flow.
* I have `routingIdentifier`. What should I call next?
* Compare `Verify` and `Get Offer` for new integrations.
* Which pages should I read before implementing ticketing polling?
* Where should I look for payment decline troubleshooting?
* Which webhook pages matter after ticketing completes?

### Ground rules

Use MCP as a navigation and implementation aid.

Keep these rules:

* treat [API Reference](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/LfT8Y3jMIGXTnxwihZhV) as the source of truth for fields and schemas
* keep production secrets out of prompts
* validate request details against your actual environment
* complete [UAT Validation](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/aH2Shbpf2B9zZldFkBrT) before go-live

{% hint style="info" %}
GitBook MCP is available at [the MCP endpoint](https://resources.atriptech.com/~gitbook/mcp).
{% endhint %}

### Suggested workflow

1. Use MCP to find the right flow.
2. Open the matching overview or guide page.
3. Confirm fields and schemas in [API Reference](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/LfT8Y3jMIGXTnxwihZhV).
4. Build and validate in [Sandbox Development](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Xs5C4xGnhQl0A2GNjlwv).
5. Use troubleshooting pages when a call or state transition fails.
6. Move to [UAT Validation](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/aH2Shbpf2B9zZldFkBrT) when the flow is stable.

### Related pages

* [Quick Start](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/MkEt9qjU24ig50fQ8be2)
* [Sandbox Validation Test Kit](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/QGSV22o2k6o3CpQ1SZLf)
* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [Troubleshooting & Support](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/tPfxQTN6n9wpKCsa6jJW)
