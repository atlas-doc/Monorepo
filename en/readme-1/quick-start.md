---
description: >-
  Quick start guide for Atlas API integration from sandbox access to sandbox
  development, UAT, and production go-live.
---

# Quick Start

{% include "../.gitbook/includes/eva-help-hint.md" %}

Use this guide to move from Atlas sandbox access to live launch.

{% hint style="warning" %}
**🆕 New booking path:** Start with [🆕 Fulfilment API](../product-guides/booking/booking-flows/fulfillment-flow.md) when you use `getOfferPrice.do` and can move to payment immediately after order creation.

Use [Get Offer vs Fulfilment API](../product-guides/booking/booking-overview/booking-decisions/get-offer-vs-get-offer-price.md) when you need a fast path decision.
{% endhint %}

{% include "../.gitbook/includes/sandbox-search-currency-note.md" %}

If you want an importable assistant for workflow guidance and troubleshooting, use [Atlas AI Assistant Skill](integration-tools/atlas-ai-assistant-skill.md).

{% hint style="warning" %}
All API Reference endpoint examples use sandbox base URLs.

When you move to production, get the live API base URLs in ATRIP under `My Profile` → `Company Information`.

Production uses one base URL for `search` and another for all other transaction APIs.
{% endhint %}

<figure><img src="../.gitbook/assets/FlowChart_1_QuickStart (1).png" alt=""><figcaption><p>End-to-end integration flow from sandbox access to go-live</p></figcaption></figure>

Start here when you need to:

* understand the full Atlas API integration path
* know what to finish before moving to the next phase
* find the right page for sandbox, UAT, or go-live work

### FAQ

#### How do I start an Atlas API integration?

Start with sandbox credentials and request basics.

Then build the full booking flow in sandbox, complete UAT, and move to production only after approval and environment switch.

#### When should I move to the next phase?

Move forward only when the current phase is stable.

Each phase should produce a clear output that the next phase depends on.

### Goal of this guide

Use this page to understand the full integration path before implementation starts.

Use it to decide which page to open next and what must be finished first.

### Integration flow

{% stepper %}
{% step %}
### Sandbox Access

Generate sandbox credentials and confirm the request basics.
{% endstep %}

{% step %}
### Sandbox Development

Build and validate the full integration in sandbox.
{% endstep %}

{% step %}
### UAT Validation

Complete the required UAT track after sandbox development is stable.
{% endstep %}

{% step %}
### Production Go-Live

After UAT passes and your account is switched to `LIVE`, generate production credentials and switch to production endpoints for go-live.
{% endstep %}
{% endstepper %}

### What each phase means

#### Sandbox Access

Get sandbox credentials, confirm headers, and validate basic request handling.

#### Sandbox Development

Build and test the booking flow, payment path, order query, and webhook handling in sandbox.

#### UAT Validation

Complete the required UAT verification and get approval for production readiness.

#### Production Go-Live

Generate production credentials, switch endpoints, run smoke tests, and monitor first live traffic.

### How the full flow works

#### 1. Sandbox Access

This is the starting point of the integration.

Generate your sandbox client ID and client secret in ATRIP.

Before moving forward, confirm:

* standard headers
* request format
* identifier handling
* gzip handling

You are ready for the next phase when sandbox requests can be sent successfully.

Use [Sandbox Access](making-requests.md) for this setup.

#### 2. Sandbox Development

Use sandbox to complete the actual integration work.

This phase usually includes:

* sandbox environment setup
* search, verify, order, and payment
* order query and ticketing follow-up
* webhook registration and event handling
* sandbox test data and failure simulation

The goal is not only to call APIs successfully.

The goal is to complete the end-to-end business flow in sandbox.

Use these pages during development:

* [Sandbox Development](sandbox-development/)
* [Booking paths](../product-guides/booking/booking-flows/)
* [MCP-Assisted Development](integration-tools/mcp-assisted-development.md)
* [Booking Overview](../product-guides/booking/booking-overview/)
* [Webhook Overview](../product-guides/extensions-and-integrations/webhook-overview/)

If your product can pay immediately after `order.do`, start with [🆕 Fulfilment API](../product-guides/booking/booking-flows/fulfillment-flow.md).

During this phase, keep these identifiers for later steps:

* Search: `routingIdentifier`
* Verify: `sessionId`
* Order: `orderNo`

Move to UAT only after the sandbox flow is stable and repeatable.

#### 3. UAT Validation

UAT is the validation phase before production.

Use this phase to prove that your integration is ready for go-live.

Run UAT in ATRIP under **UAT Testing**.

Choose the required function scope and always complete **flight booking**.

Then click **Confirm and Continue**, fill the case order details, and use **Submit Verification** for automatic validation.

The main output of this phase is UAT approval.

Use [UAT Validation](uat-submission-guide.md) for the verification steps.

#### 4. Production Go-Live

Start this phase when your sandbox work is complete and you are ready for production.

Then:

* complete the required UAT work
* wait for your customer manager to switch the account to `LIVE`
* generate production credentials
* replace sandbox endpoints
* run a controlled smoke test
* monitor the first live orders and webhooks
* go live in production

This completes the move from test integration to live operation.

Use [Production Go-Live](production-go-live.md) for the go-live checklist.

### What should you keep across the booking flow?

Keep these identifiers through the main flow:

* `routingIdentifier`
* `sessionId`
* `orderNo`

If you use the Get Offer or Fulfilment API path, keep `OfferId` instead of `sessionId`.

### What each phase produces

* Sandbox Access → sandbox client ID and client secret
* Sandbox Development → stable sandbox booking and webhook flow
* UAT Validation → approved validation result
* Production Go-Live → production-ready environment

### Move to the next phase when

Use these exit checks:

* Move past Sandbox Access when authenticated sandbox requests work reliably.
* Move past Sandbox Development when the full sandbox flow is stable and repeatable.
* Move past UAT Validation when the required scope is approved.
* Move past Production Go-Live when live smoke tests pass and first live traffic is monitored.

### Recommended first path

1. Use [Sandbox Access](making-requests.md) to get credentials and confirm request basics.
2. Run [Sandbox Validation Test Kit](sandbox-development/sandbox-validation-test-kit.md) for a fast no-code health check.
3. Use [Sandbox Development](sandbox-development/) to implement the full flow.
4. Move to [UAT Validation](uat-submission-guide.md) after the sandbox flow is stable.
5. Finish with [Production Go-Live](production-go-live.md).

Use [Integration Tools](integration-tools/) if you want optional help with workflow lookup, endpoint discovery, or troubleshooting during implementation.

### First end-to-end test resource

If you want a no-code environment check first, use [Sandbox Validation Test Kit](sandbox-development/sandbox-validation-test-kit.md).

Then use this Postman collection during sandbox development:

{% file src="../.gitbook/assets/TheAtlas UAT Test Shopping & Ticketing Services Only Postman Collection (1).zip" %}

### Next step

If you are starting fresh, continue with [Sandbox Access](making-requests.md).

If sandbox access is already done, continue with [Sandbox Development](sandbox-development/).

### Related pages

* [Sandbox Access](making-requests.md)
* [Sandbox Development](sandbox-development/)
* [UAT Validation](uat-submission-guide.md)
* [Production Go-Live](production-go-live.md)
