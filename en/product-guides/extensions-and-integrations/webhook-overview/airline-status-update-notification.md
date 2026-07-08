---
description: >-
  Webhook event sent when one or more airlines change operational status in
  Atlas.
---

# Airline Status Update Notification

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this webhook when you need to react to airline-level availability changes.

This is the first live scenario in Atlas multi-channel notifications.

Use [Multi-channel Notifications](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/KsOoqFTUcKVpOxUhs5R7) to configure ATRIP delivery across webhook, email, and team chat.

### Trigger

Atlas sends `airline.status` when an airline moves between active, maintenance, or inactive states.

Common reasons include data quality issues, system issues, insufficient balance, scheduled maintenance, and look-to-book limits.

### What you should do

When you receive this event:

* update internal airline availability flags
* adjust search caching or routing behavior
* suppress booking flows for inactive or maintenance airlines if needed

### Endpoint

POST to the webhook URL you registered with Atlas.

### Fields to read first

* `type`
* `data.airline`
* `data.airlineStatus`

### Airline status values

* `Active`
* `Maintenance`
* `Inactive`

### Typical payload

```json
{
  "data": {
    "airline": ["TO", "HV"],
    "airlineStatus": "Active"
  },
  "status": -1,
  "type": "airline.status"
}
```

{% hint style="info" %}
Email and chat deliveries may render this event with business fields such as airline, status, start time, reason, expected restoration time, and a details link. Those display fields are channel-specific and are not part of the webhook schema on this page.
{% endhint %}

### Notes

* `status` is internal and should not be used for business logic
* this event is operational, not order-specific
* treat `Maintenance` and `Inactive` as non-bookable until recovery

{% tabs %}
{% tab title="Schema" %}
**data**

* **Type:** Object
* **Required:** Yes
* **Description:** Contains airline information including the airline codes and their status.
* **Default:** None
*   **Example:**

    ```json
    {
      "airline": ["TO", "HV"],
      "airlineStatus": "Active"
    }
    ```

**data.airline**

* **Type:** Array of Strings
* **Required:** Yes
* **Description:** List of airline codes associated with the response.
* **Default:** None
* **Example:** `["TO", "HV"]`

**data.airlineStatus**

* **Type:** String
* **Required:** Yes
* **Description:** Indicates the operational status of the airline(s).
* **Valid values:**
  * Active = Online
  * Maintenance = Airline is under maintenance
  * Inactive = Offline
* **Default:** None
* **Example:** `"Active"`

**status**

* **Type:** Integer
* **Required:** Yes
* **Description:** Indicates the response status. Only for internal use by Atlas.
* **Default:** None
* **Example:** `-1`

**type**

* **Type:** String
* **Required:** Yes
* **Description:** Specifies the type of response message.
* **Valid value:**
  * airline.status
* **Default:** None
* **Example:** `"airline.status"`
{% endtab %}

{% tab title="Samples" %}
```json
{
  "data":{
     "airline":["TO","HV"],
     "airlineStatus":"Active"},
  "status":-1,
  "type":"airline.status"
}
```
{% endtab %}
{% endtabs %}

### Related pages

* [Multi-channel Notifications](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/KsOoqFTUcKVpOxUhs5R7)
* [Webhook Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/1kDgZtL5TYuOLUmAxRd6)
* [Search Errors](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ZZXG9HGTENPgRVyaaoYs)
