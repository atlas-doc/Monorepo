---
description: >-
  Use GitBook MCP to find workflows, understand endpoints, and speed up Atlas
  API integration.
---

# MCP-Assisted Development

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use GitBook MCP to speed up Atlas API development.

It helps you find the right pages, understand the flow, and narrow down the next step faster.

If you want a packaged assistant setup, use [Atlas AI Assistant Skill](atlas-ai-assistant-skill.md).

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

* [Sandbox Development](../sandbox-development/)
* [Booking Overview](../../product-guides/booking/booking-overview/)
* [API Reference](../../api-reference/)

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

* [Error Codes](../../support-and-reference/troubleshooting-and-support/errors-handing/)
* [FAQs](../../support-and-reference/troubleshooting-and-support/faqs/)
* [Webhook Overview](../../product-guides/extensions-and-integrations/webhook-overview/)

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

* treat [API Reference](../../api-reference/) as the source of truth for fields and schemas
* keep production secrets out of prompts
* validate request details against your actual environment
* complete [UAT Validation](../uat-submission-guide.md) before go-live

{% hint style="info" %}
GitBook MCP is available at [the MCP endpoint](https://resources.atriptech.com/~gitbook/mcp).
{% endhint %}

### Suggested workflow

1. Use MCP to find the right flow.
2. Open the matching overview or guide page.
3. Confirm fields and schemas in [API Reference](../../api-reference/).
4. Build and validate in [Sandbox Development](../sandbox-development/).
5. Use troubleshooting pages when a call or state transition fails.
6. Move to [UAT Validation](../uat-submission-guide.md) when the flow is stable.

### Related pages

* [Quick Start](../quick-start.md)
* [Sandbox Validation Test Kit](../sandbox-development/sandbox-validation-test-kit.md)
* [Booking Overview](../../product-guides/booking/booking-overview/)
* [Troubleshooting & Support](../../support-and-reference/troubleshooting-and-support/)
