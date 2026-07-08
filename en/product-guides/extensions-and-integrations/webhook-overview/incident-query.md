---
description: >-
  Atlas API incident query for webhook reconciliation, event filtering, and
  schedule-change or cancellation follow-up.
---

# Incident Query

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page to search incident records when webhook delivery or event state needs confirmation.

Start here when you need to:

* reconcile missed or unclear webhook events
* search incidents by order, airline, passenger, or time range
* investigate schedule-change or cancellation history

### FAQ

#### When should I use Incident Query?

Use Incident Query when webhook delivery, incident history, or event confirmation still needs deeper reconciliation.

#### Which filters should I start with?

Start with `orderNo` for one affected booking.

Add `eventType`, airline, or time range filters when the incident set is broader.

### Main API

* `event/getPageList.do`

### Use this when you need

* Reconcile missed webhook events
* Filter incidents by order, passenger, or airline
* Review event confirmation status
* Investigate schedule change or cancellation history

### Common query patterns

#### Find incidents for one order

Use:

* `orderNo`
* `pageSize`

#### Find schedule changes for one airline

Use:

* `eventType`
* `airline`
* `eventTimeStart`
* `eventTimeEnd`
* `pageSize`

#### Find unresolved incidents

Use:

* `eventStatus`
* `pageSize`

### Common filters

* `eventId`
* `orderNo`
* `eventType`
* `pnr`
* `paxName`
* `paxEmail`
* `airline`
* `eventStatus`
* `eventTimeStart`
* `eventTimeEnd`
* `pageIndex`
* `pageSize`

### Required field

* `pageSize`

### Response highlights

* `records`
* `pageIndex`
* `pageSize`
* `total`
* Event status and confirmation fields

### Tips

* always send `pageSize`
* start with `orderNo` when debugging one affected booking
* add time ranges when querying broad incident sets
* use this together with webhook payload logs and order query results

### What comes next?

Use the query result together with [Query Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n) and [Incident Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/IrfigjkYxz2qfdAQwbuX) to confirm the final operational state.

### Full API reference

See endpoint-level details here:

* [Webhook Registration & Incidents](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/tHs475MBpb4mdFaxH0qc)

### Related pages

* [Incident Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/IrfigjkYxz2qfdAQwbuX)
* [Schedule Change Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/8TuCRQT1tW58vMulbndJ)
* [Query Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n)
