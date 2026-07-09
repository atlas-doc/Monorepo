---
description: >-
  Atlas API webhook registration and incident query reference for endpoint
  setup, updates, and event reconciliation.
---

# Webhook Registration & Incidents

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this page to register your webhook endpoint and query incident records from the API reference layer.

Start here when you need to:

* register or update the webhook URL before go-live
* query incidents after missed or unresolved events
* reconcile webhook delivery with incident records

### FAQ

#### When should we register the webhook URL?

Register the webhook URL before go-live.

Then update it whenever the receiving endpoint changes.

The same URL receives all supported events, including `order.void`.

#### When should we query incidents?

Query incidents when webhook delivery, schedule-change handling, or operational follow-up needs deeper reconciliation.

Use incident lookup when the event trail is incomplete or still unclear after webhook processing.

#### How should fulfillment-flow orders use webhook and incident query?

Use webhook as the early signal.

Use incident query when the event trail is incomplete.

Keep active order polling during the 5-minute fulfillment window.

### What this page covers

* `updateWebhookURL.do` for webhook registration
* `event/getPageList.do` for incident lookup

### What comes next?

Use [Webhook Overview](../../product-guides/extensions-and-integrations/webhook-overview/) for the operating model and event coverage.

Use [Incident Query](../../product-guides/extensions-and-integrations/webhook-overview/incident-query.md) and [Incident Notification](../../product-guides/extensions-and-integrations/webhook-overview/incident-notification.md) when you need deeper incident follow-up.

### Typical flow

{% stepper %}
{% step %}
### Register your webhook URL

Save the endpoint that Atlas should call for webhook delivery.
{% endstep %}

{% step %}
### Receive webhook events

Handle ticketing, void, schedule change, airline status, email, and incident notifications.

For fulfillment-flow orders, use these events to reduce reaction time, not to replace order query.
{% endstep %}

{% step %}
### Query incidents when needed

Use incident lookup to reconcile missed or unresolved events.
{% endstep %}
{% endstepper %}

### Use this when you need

* initial webhook setup
* webhook endpoint updates
* incident reconciliation
* operational follow-up after schedule changes or cancellations

### Registration scope

Register one webhook URL with `updateWebhookURL.do`.

Atlas uses that URL for all supported webhook event types.

That includes `order.void`.

The same registration should already be live before you start fulfillment traffic with `getOfferPrice.do`.

### Related pages

* [Webhooks](../../product-guides/extensions-and-integrations/webhook-overview/)
* [Fulfillment API](../../product-guides/booking/booking-step-guides/get-offer-price.md)
* [Incident Query](../../product-guides/extensions-and-integrations/webhook-overview/incident-query.md)
* [Incident Notification](../../product-guides/extensions-and-integrations/webhook-overview/incident-notification.md)

{% openapi-operation spec="atlas-api" path="/updateWebhookURL.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/6d498c79f43546e63a2289f81c033345c8210830410d2835d33def093c5f3f29.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260709%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260709T022316Z&X-Amz-Expires=172800&X-Amz-Signature=24c7d9ddd0fa08c4e26f3f05e8ac36368708509984309cc2f4d26ea6bccf77e8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="atlas-api" path="/event/getPageList.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/6d498c79f43546e63a2289f81c033345c8210830410d2835d33def093c5f3f29.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260709%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260709T022316Z&X-Amz-Expires=172800&X-Amz-Signature=24c7d9ddd0fa08c4e26f3f05e8ac36368708509984309cc2f4d26ea6bccf77e8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
