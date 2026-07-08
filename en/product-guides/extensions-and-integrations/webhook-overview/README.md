---
description: >-
  Atlas API webhook setup, event coverage, delivery expectations, and incident
  follow-up guidance.
---

# Webhook Overview

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this section to register webhook endpoints and consume event notifications.

Start here when you need to:

* register webhook delivery before go-live
* understand which booking events Atlas can notify
* decide how webhook fits with order query and airline email
* configure webhook as one delivery option in Atlas notifications

{% hint style="info" %}
Need ATRIP notification setup across webhook, email, and team chat? Start with [Multi-channel Notifications](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/KsOoqFTUcKVpOxUhs5R7).
{% endhint %}

If you need channel setup first, open [Multi-channel Notifications](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/KsOoqFTUcKVpOxUhs5R7) before reading webhook event details.

### FAQ

#### Are Atlas webhooks guaranteed?

No.

Webhook delivery is best effort.

Use order query, airline email, and incident follow-up for final reconciliation.

#### What should webhook be used for?

Use webhook as the server-to-server delivery option in Atlas notifications.

Use webhook to speed up event handling for ticketing completion, void updates, schedule changes, airline status updates, email capture, and incident follow-up.

Use [Multi-channel Notifications](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/KsOoqFTUcKVpOxUhs5R7) when you also need ATRIP delivery in email, DingTalk, WeCom, Slack, or Teams.

Do not treat webhook as the only source of truth for booking state.

#### Can webhook replace order query in the fulfillment flow?

No.

Use webhook as an early signal.

Use `queryOrderDetails.do` for final ticketing confirmation.

### Overview

Webhooks will automatically notify you on airline changes that affect your customers’ bookings. For example, when an airline has changed the flight schedule affecting one of your orders, the Atlas API will send a notification about this event to your server, and you can process it. For example, you may take actions by updating your database or emailing the customer.

> Atlas provides the webhook functionality on the “best possible basis”. Atlas does not take the responsibility for providing all the notifications. For any schedule changes please always refer to the email sent by the airline to the email id provided in the booking request.

### Recommended webhook model

Use webhook as a near-real-time signal.

Then confirm the final state with order query, incident query, or airline email when needed.

### Fulfillment flow alerting

For orders created from `getOfferPrice.do`, monitor the order actively inside the 5-minute ticketing window.

Use webhook to shorten reaction time for completion, cancellation, and incident follow-up.

Then confirm the final outcome with `queryOrderDetails.do`.

{% hint style="warning" %}
Webhook should not be the only timeout detector for the fulfillment flow.

Keep active order polling during the ticketing window.
{% endhint %}

### Typical flow

{% stepper %}
{% step %}
### Register your endpoint

Use [Webhook Registration & Incidents](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/tHs475MBpb4mdFaxH0qc) to save the webhook URL before go-live.

If you also use mailbox or chat delivery, configure those channels in [Multi-channel Notifications](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/KsOoqFTUcKVpOxUhs5R7).
{% endstep %}

{% step %}
### Receive and process events

Handle ticketing, void, schedule, airline, email, and incident notifications.

Atlas sends webhook notifications for these common scenarios:

1. Ticket booked: [Ticketing Complete Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/zNIgwHcnNogdlVW0KpPO)
2. Void submitted or updated: [Void Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/4aywYMVHUfvNZttgiHPn)
3. Change in flight schedule: [Schedule Change Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/8TuCRQT1tW58vMulbndJ)
4. Airline status update: [Airline Status Update Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/pMAI2bv1LdjljhHdIseW)
5. Email received: [Email Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/5JKeyb6NAdTPL7cjz8W2)
{% endstep %}

{% step %}
### Reconcile when needed

Use incident queries and order APIs to confirm final state.

1. Incident notification: [Incident Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/IrfigjkYxz2qfdAQwbuX)
2. Incident query: [Incident Query](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/70gk6tmdLYkYGQSscSKw)
{% endstep %}
{% endstepper %}

### What webhook should not replace

Webhook should not replace:

* `queryOrderDetails.do` for final ticketing confirmation
* `queryVoidOrders.do` for final void reconciliation
* airline email for schedule-change awareness
* incident query for deeper incident reconciliation
* active order monitoring during the fulfillment-flow deadline
