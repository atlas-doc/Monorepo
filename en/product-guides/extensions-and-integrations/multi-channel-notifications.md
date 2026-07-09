---
description: >-
  Configure Atlas notifications across webhook, email, DingTalk, WeCom, Slack,
  and Teams for airline status updates and future scenarios.
---

# Multi-channel Notifications

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this page when you need to configure Atlas business notifications in ATRIP and choose the right delivery channels for your team.

Start here when you need to:

* choose between webhook, email, and team-chat delivery
* configure notification delivery in ATRIP
* understand which scenario is live first

### Supported channels

Atlas supports these notification channels:

* **Webhook** for server-to-server delivery and downstream automation
* **Email** for formal operational follow-up and mailbox-based workflows
* **DingTalk**, **WeCom**, **Slack**, and **Microsoft Teams** for team collaboration and fast awareness

You can configure one or more channels.

### First live scenario

The first scenario on this notification framework is **airline status changes**.

Atlas sends a notification when an airline changes operational status and may affect search or booking availability.

Common reasons include:

* data quality issues
* system issues or scheduled maintenance
* insufficient balance or look-to-book limits

### What the notification shows

Airline status notifications can include these business fields:

* airline name and airline code
* current status
* start time
* reason
* expected restoration time when available
* a link to the airline details page

{% hint style="info" %}
Webhook payload fields are documented separately on [Airline Status Update Notification](webhook-overview/airline-status-update-notification.md). Chat and email deliveries may render the same event in a channel-specific format.
{% endhint %}

### Configure notifications in ATRIP

{% stepper %}
{% step %}
### Open Notification Reminders

Sign in to ATRIP.

Go to **Account Center → Profile Management → Notification Reminders**.
{% endstep %}

{% step %}
### Choose one or more channels

Select the channels your team wants to use:

* Webhook
* Email
* DingTalk
* WeCom
* Slack
* Teams
{% endstep %}

{% step %}
### Complete each channel setup

Open the target channel section.

Use **How to get it** for channel-specific setup instructions.
{% endstep %}

{% step %}
### Send a test notification

Use **Send Test Notification** after setup.

Confirm the test reaches the right mailbox, group, or endpoint.
{% endstep %}
{% endstepper %}

### Channel selection guidance

Choose channels based on how your team works:

* use **Webhook** when another system needs to react automatically
* use **Email** when operations or management needs an auditable trail
* use chat tools when multiple agents need fast shared visibility

### FAQ

#### Do I need to configure every channel?

No.

Configure only the channels your team uses.

#### How do I confirm the setup works?

Use **Send Test Notification** in **Notification Reminders**.

Then confirm the message reaches the destination channel.

#### Which page documents the webhook schema?

Use [Airline Status Update Notification](webhook-overview/airline-status-update-notification.md) for the current `airline.status` webhook payload.

### Related pages

* [Webhook Overview](webhook-overview/)
* [Webhook Registration & Incidents](../../api-reference/webhook-and-incident-apis/webhook-registration-and-incidents.md)
* [Airline Status Update Notification](webhook-overview/airline-status-update-notification.md)
