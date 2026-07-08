---
description: >-
  Start here for Atlas API onboarding, sandbox setup, implementation lifecycle,
  UAT, and production go-live.
---

# 集成指南

{% include "../.gitbook/includes/eva-help-hint.md" %}

Use this section for Atlas onboarding and the full implementation lifecycle from sandbox to go-live.

Start here when you need to:

* get access and credentials
* build the integration in the right order
* prepare UAT evidence
* complete production cutover safely

### What belongs in Integration Guides

Use this section for:

* onboarding and access setup
* sandbox implementation
* validation and go-live preparation
* integration-stage setup tasks

Use [Product Guides](../product-guides/) when you need to choose the right booking flow or product capability.

Use [API Reference](../api-reference/) when you need exact endpoint fields and schemas.

### Recommended reading order

1. [Quick Start](quick-start.md)
2. [Sandbox Access](making-requests.md)
3. [Sandbox Development](sandbox-development/)
4. [UAT Validation](uat-submission-guide.md)
5. [Production Go-Live](production-go-live.md)

Use [Integration Tools](integration-tools/) when you want optional implementation accelerators such as [Atlas AI Assistant Skill](integration-tools/atlas-ai-assistant-skill.md) or [MCP-Assisted Development](integration-tools/mcp-assisted-development.md).

### Common starting points

#### New Atlas API integration

Start with [Quick Start](quick-start.md).

Then move to [Sandbox Access](making-requests.md) and [Sandbox Development](sandbox-development/).

#### UAT and launch preparation

Use [UAT Validation](uat-submission-guide.md) and [Production Go-Live](production-go-live.md).

#### Notification setup during integration

Use [Webhook Overview](../product-guides/extensions-and-integrations/webhook-overview/) for webhook event coverage and handling guidance.

Use [Multi-channel Notifications](../product-guides/extensions-and-integrations/multi-channel-notifications.md) for channel setup across webhook, email, DingTalk, WeCom, Slack, and Teams.

#### Need to choose a booking flow?

Use [Product Guides](../product-guides/).

Start with [Booking Overview](../product-guides/booking/booking-overview/) when you are deciding between the three main booking paths.

### Typical implementation lifecycle

{% stepper %}
{% step %}
### Access and kickoff

Collect sandbox credentials and confirm required request headers.
{% endstep %}

{% step %}
### Sandbox development

Build the integration in sandbox and validate the main implementation path.
{% endstep %}

{% step %}
### UAT validation

Run the required UAT track and submit the evidence package.
{% endstep %}

{% step %}
### Production go-live

Switch to production credentials and endpoints after UAT approval and account activation.
{% endstep %}
{% endstepper %}

### Related sections

* [Product Guides](../product-guides/)
* [API Reference](../api-reference/)
* [Support & Reference](../support-and-reference/)
