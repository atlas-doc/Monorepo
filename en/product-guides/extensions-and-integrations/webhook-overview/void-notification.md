---
description: Webhook event sent when a void request is submitted or its status changes.
---

# Void Notification

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this webhook when you need near-real-time void lifecycle updates.

Start here when you need to:

* detect successful void submission
* track void progress and final outcome
* capture rejection or retry-failure reasons

### FAQ

#### When is this webhook sent?

Atlas sends `order.void` after `void.do` succeeds.

Atlas also sends it when void status changes.

Atlas sends it again when automatic processing fails after 10 retries.

#### Should this replace void query?

No.

Use this webhook as a fast signal.

Use `queryVoidOrders.do` for final reconciliation.

#### How fast should we expect the first void result?

In most cases, Atlas returns within about 5 minutes whether the void request was accepted for processing.

Final completion or rejection can still take longer.

Use this webhook for progress changes.

### Trigger

Atlas sends `order.void` for these scenarios:

* successful void submission
* void status changes
* automatic failure after 10 retries

### What you should do

When you receive this event:

* match `data.orderNo` and `data.voidCode`
* update the case with `data.voidStatus`
* store `data.message` for operations follow-up

### Recommended handling

Process the event in this order:

1. Read `type` and confirm `order.void`.
2. Match `data.orderNo` to your order.
3. Match `data.voidCode` to the void case.
4. Update internal status from `data.voidStatus`.
5. Store `data.message` for audit and support.
6. Query void status if the case stays open.

### Endpoint

POST to the webhook URL you registered with Atlas.

Use the existing webhook registration flow.

No extra registration is required for `order.void`.

### Fields to read first

* `type`
* `data.orderNo`
* `data.voidCode`
* `data.voidStatus`
* `data.message`

### Void status values

* `0`: Atlas Processing
* `1`: Airline Processing
* `2`: Voided / Refunded
* `3`: Airline Voiding
* `4`: Rejected
* `5`: Completed
* `6`: Withdrew

### Typical payload

```json
{
  "cid": "XXXXXXX",
  "type": "order.void",
  "status": -1,
  "data": {
    "orderNo": "TESTA20250512100600259",
    "voidCode": "202505-0012",
    "voidStatus": 2,
    "message": "Void successful and confirmed by the airline."
  }
}
```

### Retry failure behavior

If automatic processing still fails after 10 retries, Atlas sends another `order.void` event.

In that case, expect `data.voidStatus = 4`.

Use `data.message` to route manual follow-up.

### Notes

* `status` is internal and is normally `-1`
* `message` is descriptive and can vary by case
* first submission feedback usually appears within about 5 minutes
* use void query if refund completion is still unclear

{% tabs %}
{% tab title="Schema" %}
**cid**

* **Type:** String
* **Required:** Yes
* **Description:** Unique client identifier.
* **Example:** `"XXXXXXX"`

**type**

* **Type:** String
* **Required:** Yes
* **Description:** Notification type. Always `order.void`.
* **Example:** `"order.void"`

**status**

* **Type:** Integer
* **Required:** Yes
* **Description:** Internal status field. `-1` means normal delivery.
* **Example:** `-1`

**data**

* **Type:** Object
* **Required:** Yes
* **Description:** Void event payload.

**data.orderNo**

* **Type:** String
* **Required:** Yes
* **Description:** Atlas order number.
* **Example:** `"TESTA20250512100600259"`

**data.voidCode**

* **Type:** String
* **Required:** Yes
* **Description:** Void case number returned by `void.do`.
* **Example:** `"202505-0012"`

**data.voidStatus**

* **Type:** Integer
* **Required:** Yes
* **Description:** Current void processing status.
* **Valid values:**
  * `0`: Atlas Processing
  * `1`: Airline Processing
  * `2`: Voided / Refunded
  * `3`: Airline Voiding
  * `4`: Rejected
  * `5`: Completed
  * `6`: Withdrew
* **Example:** `2`

**data.message**

* **Type:** String
* **Required:** No
* **Description:** Human-readable status or failure detail.
* **Example:** `"Void successful and confirmed by the airline."`
{% endtab %}

{% tab title="Samples" %}
**Success**

```json
{
  "cid": "XXXXXXX",
  "type": "order.void",
  "status": -1,
  "data": {
    "orderNo": "TESTA20250512100600259",
    "voidCode": "202505-0012",
    "voidStatus": 2,
    "message": "Void successful and confirmed by the airline."
  }
}
```

**Retry failure**

```json
{
  "cid": "XXXXXXX",
  "type": "order.void",
  "status": -1,
  "data": {
    "orderNo": "TESTA20250512100600259",
    "voidCode": "202505-0012",
    "voidStatus": 4,
    "message": "Automatic void processing failed after 10 retries."
  }
}
```
{% endtab %}
{% endtabs %}

### Related pages

* [Webhook Overview](./)
* [Webhook Registration & Incidents](../../../api-reference/webhook-and-incident-apis/webhook-registration-and-incidents.md)
* [Void](../../../api-reference/post-booking-apis/void.md)
* [Void workflow](../../post-booking/void.md)
