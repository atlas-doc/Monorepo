---
description: Webhook event sent when Atlas captures an airline email related to an order.
---

# Email Notification

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this webhook when you need to process airline email activity tied to orders.

### Trigger

Atlas sends `email.all` when Atlas email capture receives an airline email for an order.

### What you should do

When you receive this event:

* store `orderNo` and `uniqueCode`
* classify the email by `emailCategory`
* fetch or archive the email content quickly if you need the full body
* route the event into support, schedule-change, or post-booking workflows when needed

### Endpoint

POST to the webhook URL you registered with Atlas.

### Fields to read first

* `type`
* `data.orderNo`
* `data.emailCategory`
* `data.emailSubject`
* `data.emailLink`
* `data.createTime`

### Typical payload

```json
{
  "cid": "XXXXX",
  "data": {
    "orderNo": "XXXXXX",
    "emailCategory": "Payment Success",
    "emailSubject": "easyJet booking reference: XXXXX",
    "emailLink": "http://example.com/email.eml",
    "createTime": "2024-01-05 10:54:26"
  },
  "notificationId": "20240105105430470MJMOR",
  "status": -1,
  "type": "email.all"
}
```

### Notes

* `emailLink` is temporary and expires quickly
* if you need long-term access, store the email payload at your side
* `status` is internal and should be ignored for business logic

{% tabs %}
{% tab title="Schema" %}
**`cid`**

* **Type:** String
* **Required:** Yes
* **Description:** Unique client identifier.
* **Default:** None
* **Example:** `"XXXXX"`

**`notificationId`**

* **Type:** String
* **Required:** Yes
* **Description:** Unique identifier for the notification event.
* **Default:** None
* **Example:** `"20240105105430470MJMOR"`

**`status`**

* **Type:** Integer
* **Required:** Yes
* **Description:** In this type of notification status always = -1. This is an internal field and should be ignored.
* **Default:** None
* **Example:** `-1`

**`type`**

* **Type:** String
* **Required:** Yes
* **Description:** Notification type.
* **Default:** None
* **Example:** `"email.all"`

**`data`**

* **Type:** Object
* **Required:** Yes
* **Description:** Contains email-related details.
* **Default:** None
* **Example:** `{ ... }`

**`data.orderNo`**

* **Type:** String
* **Required:** Yes
* **Description:** Order number associated with the email.
* **Default:** None
* **Example:** `"XXXXXX"`

**`data.emailReceivingDate`**

* **Type:** String
* **Required:** Yes
* **Description:** Date and time when the email was received by Atlas (UTC). Format: `YYYY-MM-DD HH:mm:ss`.
* **Default:** None
* **Example:** `"2024-01-05 10:54:21"`

**`data.uniqueCode`**

* **Type:** String
* **Required:** Yes
* **Description:** Unique code for identifying the email.
* **Default:** None
* **Example:** `"e4afbecfd5727817ff73a71a94a2a64d"`

**`data.emailCategory`**

* **Type:** String
* **Required:** Yes
* **Description:** Atlas email categories. Atlas categorizes emails but does not guarantee accuracy in classification.
* **Valid values:**
  * Schedule change
  * Receipt
  * Payment Success
  * Verification
  * Trip Reminder
  * Promo code
  * Travel Itinerary
  * Advertisement
  * PNR Cancellation Success
  * Payment Due
  * Unidentified
  * Duplicated Schedule Change
  * Unaccounted Cancellation
* **Default:** None
* **Example:** `"Payment Success"`

**`data.from`**

* **Type:** String
* **Required:** Yes
* **Description:** Sender’s email address.
* **Default:** None
* **Example:** `"donotreply@easyjet.com"`

**`data.to`**

* **Type:** String
* **Required:** Yes
* **Description:** Recipient’s email address.
* **Default:** None
* **Example:** `"NSDLZCQTGJTEYXOMFOD@gorn.top"`

**`data.emailSubject`**

* **Type:** String
* **Required:** Yes
* **Description:** Subject of the email.
* **Default:** None
* **Example:** `"easyJet booking reference: XXXXX"`

**`data.emailLink`**

* **Type:** String
* **Required:** Yes
* **Description:** URL link to access the email content. Email Link is only valid for 10 mins.
* **Default:** None
* **Example:** `"http://order-oss-sg.oss-ap-southeast-1.aliyuncs.com/...eml?Expires=1704426870..."`

**`data.createTime`**

* **Type:** String
* **Required:** Yes
* **Description:** Create Time is the time when Atlas created this email record in the Email list. Generally, it will be later than the receiving time. Format: `YYYY-MM-DD HH:mm:ss`.
* **Default:** None
* **Example:** `"2024-01-05 10:54:26`
{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid":"XXXXX",
    "data":{
        "orderNo":"XXXXXX",
        "emailReceivingDate":"2024-01-05 10:54:21",
        "uniqueCode":"e4afbecfd5727817ff73a71a94a2a64d",
        "emailCategory":"Payment Success",
        "from":"donotreply@easyjet.com",
        "to":"NSDLZCQTGJTEYXOMFOD@gorn.top",
        "emailSubject":"easyJet booking reference: XXXXX",
        "emailLink":"http://order-oss-sg.oss-ap-southeast-1.aliyuncs.com/2024/01/e4afbecfd5727817ff73a71a94a2a64d.eml?Expires=1704426870&OSSAccessKeyId=LTAI5tDmTE9iwtNdsqxVXuom&Signature=zF8aNNsGgY8n2jhsW7V1gmPLw8c%3D",
        "createTime":"2024-01-05 10:54:26"
    },
    "notificationId":"20240105105430470MJMOR",
    "status":-1,
    "type":"email.all"
}
```
{% endtab %}
{% endtabs %}

### Related pages

* [Email Query](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/mQPRhePPYFLL0uCWyvMj)
* [Incident Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/IrfigjkYxz2qfdAQwbuX)
* [Webhook Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/1kDgZtL5TYuOLUmAxRd6)
