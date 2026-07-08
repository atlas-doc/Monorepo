---
description: >-
  Webhook event sent when Atlas receives a confirmed flight schedule change or
  cancellation.
---

# Schedule Change Notification

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this webhook when a booked itinerary changes after ticketing.

### Trigger

Atlas sends `order.schedulechange` when flight segments change or are canceled.

### What you should do

When you receive this event:

* compare `previousSegs`, `revisedSegs`, and `originalSegs`
* determine whether the change is a schedule update or cancellation
* notify affected travelers
* create any required internal reissue, refund, or support workflow

### Endpoint

POST to the webhook URL you registered with Atlas.

### Fields to read first

* `type`
* `data.orderNo`
* `data.scheduleChangeType`
* `data.previousSegs`
* `data.revisedSegs`
* `data.originalSegs`

### Schedule change types

* `1`: schedule change
* `2`: flight cancel

### Typical payload

```json
{
  "cid": "XXXXXXX",
  "notificationId": "20230917143240511TATVO",
  "status": 0,
  "type": "order.schedulechange",
  "data": {
    "orderNo": "ATXFQ20230720193244809",
    "scheduleChangeType": 1,
    "previousSegs": [],
    "revisedSegs": [],
    "originalSegs": []
  }
}
```

### Notes

* `status` reflects incident confirmation state, not booking success
* `revisedSegs` can be empty for cancellation scenarios
* `originalSegs` preserves the itinerary booked by the traveler

{% tabs %}
{% tab title="Schema" %}
**cid**

* **Type:** String
* **Required:** Yes
* **Description:** Unique client identifier for tracking requests.
* **Default:** None
* **Example:** `"XXXXXXX"`

**notificationId**

* **Type:** String
* **Required:** Yes
* **Description:** Unique identifier for the notification event.
* **Default:** None
* **Example:** `"20230917143240511TATVO"`

**status**

* **Type:** Integer
* **Required:** Yes
*   **Description:** Incident staus.

    Valid values:

    * 0: Unconfirmed
    * 1: Confirmed
* **Default:** None
* **Example:** `0`

**type**

* **Type:** String
* **Required:** Yes
* **Description:** Notification type. Always `order.schedulechange` for schedule change.
* **Default:** None
* **Example:** `"order.schedulechange"`

**data**

* **Type:** Object
* **Required:** Yes
* **Description:** Contains previous, original and revised flight segments.
* **Default:** None
*   **Example:**

    ```json
    {
      "orderNo": "ATXFQ20230720193244809",
      "previousSegs": [ ... ],
      "revisedSegs": [ ... ],
      "originalSegs": [ ... ],
      "scheduleChangeType": 1
    }
    ```

**data.orderNo**

* **Type:** String
* **Required:** Yes
* **Description:** Unique order number associated with the flight booking.
* **Default:** None
* **Example:** `"ATXFQ20230720193244809"`

**data.scheduleChangeType**

* **Type:** Integer
* **Required:** Yes
*   **Description:** Type of schedule change.

    Valid values:

    * 1: Schedule change
    * 2: Flight cancel
* **Default:** None
* **Example:** `1`

**data.previousSegs**

* **Type:** Array of Objects
* **Required:** Yes
* **Description:** Contains the details of the flight segments before this scheduled change.
* **Default:** None

**data.previousSegs\[]**

* **Type:** Object
* **Required:** Yes
* **Description:** Individual flight segment details before this schedule change.
*   **Example:**

    ```json
    {
      "depAirport": "HKG",
      "arrAirport": "SGN",
      "depTime": "2023-07-24 19:50:00",
      "arrTime": "2023-07-24 21:30:00",
      "carrier": "VJ",
      "flightNumber": "VJ877",
      "depTerminal": "",
      "arrTerminal": "",
      "direction": 1
    }
    ```

**data.previousSegs\[].depAirport**

* **Type:** String
* **Required:** Yes
* **Description:** Departure airport code (IATA).
* **Default:** None
* **Example:** `"HKG"`

**data.previousSegs\[].arrAirport**

* **Type:** String
* **Required:** Yes
* **Description:** Arrival airport code (IATA).
* **Default:** None
* **Example:** `"SGN"`

**data.previousSegs\[].depTime**

* **Type:** String
* **Required:** Yes
* **Description:** Departure time in `YYYY-MM-DD HH:MM:SS` format.
* **Default:** None
* **Example:** `"2023-07-24 19:50:00"`

**data.previousSegs\[].arrTime**

* **Type:** String
* **Required:** Yes
* **Description:** Arrival time in `YYYY-MM-DD HH:MM:SS` format.
* **Default:** None
* **Example:** `"2023-07-24 21:30:00"`

**data.previousSegs\[].carrier**

* **Type:** String
* **Required:** Yes
* **Description:** Airline carrier code.
* **Default:** None
* **Example:** `"VJ"`

**data.previousSegs\[].flightNumber**

* **Type:** String
* **Required:** Yes
* **Description:** Flight number assigned by the airline.
* **Default:** None
* **Example:** `"VJ877"`

**data.previousSegs\[].depTerminal**

* **Type:** String
* **Required:** No
* **Description:** Departure terminal information.
* **Default:** `""`
* **Example:** `""`

**data.previousSegs\[].arrTerminal**

* **Type:** String
* **Required:** No
* **Description:** Arrival terminal information.
* **Default:** `""`
* **Example:** `""`

**data.previousSegs\[].direction**

* **Type:** Integer
* **Required:** Yes.
* **Description:** 1 represents the outbound segment, and 2 represents the return segment.
* **Default:** None
* **Example:** `1`

**data.revisedSegs**

* **Type:** Array of Objects
* **Required:** Yes
* **Description:** Contains details of the flight segments after the schedule change. If the `data.scheduleChangeType` indicates a flight cancellation, this node shall be an empty array (i.e., there are no protected flights).
* **Default:** None

**data.revisedSegs\[]**

* **Type:** Object
* **Required:** Yes
* **Description:** Individual flight segment details after the schedule change.
*   **Example:**

    ```json
    {
      "depAirport": "SGN",
      "arrAirport": "HKG",
      "depTime": "2023-10-19 15:10:00",
      "arrTime": "2023-10-19 18:50:00",
      "carrier": "VJ",
      "flightNumber": "VJ876",
      "codeShare": false,
      "depTerminal": "",
      "arrTerminal": "",
      "direction": 1
    }
    ```

**data.originalSegs**

* **Type:** Array of Objects
* **Required:** Yes
* **Description:** Contains details of the original flight segments before any schedule change. Multiple schedule changes may occur after the ticket is issued and this node is used to display the flight segment details at the time the passenger booked the ticket.
* **Default:** None

**data.originalSegs\[]**

* **Type:** Object
* **Required:** Yes
* **Description:** Individual flight segment details at the time the passenger booked the ticket.
*   **Example:**

    ```json
    {
      "depAirport": "HKG",
      "arrAirport": "SGN",
      "depTime": "2023-07-24 19:50:00",
      "arrTime": "2023-07-24 21:30:00",
      "carrier": "VJ",
      "flightNumber": "VJ877",
      "codeShare": false,
      "depTerminal": "",
      "arrTerminal": "",
      "direction": 1
    }
    ```
{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid": "XXXXXXX",
    "notificationId": "20230917143240511TATVO",
    "status": 0,
    "type": "order.schedulechange",
    "data": {
        "orderNo": "ATXFQ20230720193244809",
        "scheduleChangeType": 1,
        "previousSegs": [
            {
                "arrAirport": "SGN",
                "arrTerminal": "",
                "arrTime": "2023-07-24 21:30:00",
                "carrier": "VJ",
                "codeShare": false,
                "depAirport": "HKG",
                "depTerminal": "",
                "depTime": "2023-07-24 19:50:00",
                "flightNumber": "VJ877",
                "direction": 1
            },
            {
                "arrAirport": "HKG",
                "arrTerminal": "",
                "arrTime": "2023-10-18 18:50:00",
                "carrier": "VJ",
                "codeShare": false,
                "depAirport": "SGN",
                "depTerminal": "",
                "depTime": "2023-10-18 14:55:00",
                "flightNumber": "VJ876",
                "direction": 1
            }
        ],
        "revisedSegs": [
            {
                "arrAirport": "SGN",
                "arrTerminal": "",
                "arrTime": "2023-07-24 21:30:00",
                "carrier": "VJ",
                "codeShare": false,
                "depAirport": "HKG",
                "depTerminal": "",
                "depTime": "2023-07-24 19:50:00",
                "flightNumber": "VJ877",
                "direction": 1
            },
            {
                "arrAirport": "HKG",
                "arrTerminal": "",
                "arrTime": "2023-10-19 18:50:00",
                "carrier": "VJ",
                "codeShare": false,
                "depAirport": "SGN",
                "depTerminal": "",
                "depTime": "2023-10-19 15:10:00",
                "flightNumber": "VJ876",
                "direction": 1
            }
        ],
        "originalSegs": [
            {
                "arrAirport": "SGN",
                "arrTerminal": "",
                "arrTime": "2023-07-24 21:30:00",
                "carrier": "VJ",
                "codeShare": false,
                "depAirport": "HKG",
                "depTerminal": "",
                "depTime": "2023-07-24 19:50:00",
                "flightNumber": "VJ877",
                "direction": 1
            },
            {
                "arrAirport": "HKG",
                "arrTerminal": "",
                "arrTime": "2023-10-18 18:50:00",
                "carrier": "VJ",
                "codeShare": false,
                "depAirport": "SGN",
                "depTerminal": "",
                "depTime": "2023-10-18 14:55:00",
                "flightNumber": "VJ876",
                "direction": 1
            }
        ]
    }
}
```
{% endtab %}
{% endtabs %}

### Related pages

* [Webhook Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/1kDgZtL5TYuOLUmAxRd6)
* [Incident Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/IrfigjkYxz2qfdAQwbuX)
* [Incident Query](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/70gk6tmdLYkYGQSscSKw)
