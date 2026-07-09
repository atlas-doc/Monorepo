---
description: >-
  Common Atlas API post-booking errors for refund, void, order query, and
  post-ticketing ancillary workflows.
---

# Refund, Query & Post-booking Errors

Use this page when issues happen after ticketing.

Start here when you need to:

* understand a refund, void, order-query, or ancillary failure after booking
* decide whether to wait, retry, or fix the request first
* route the case to the correct post-booking workflow

### FAQ

#### Which post-booking errors usually mean we should wait first?

Codes such as `809`, `814`, and `117` usually mean the order or refund process is not ready for the next step yet.

Wait for ticketing or the in-flight submission to finish before retrying.

#### Which post-booking errors usually mean we should not resubmit?

Codes such as `816`, `817`, `818`, `504`, and `505` usually mean a refund or baggage action already exists or was already applied.

Query the current status instead of submitting again.

#### Which errors are most specific to the dedicated void flow?

Codes such as `822` and `823` point to void-only submission problems.

Use the dedicated [Void](../../../product-guides/post-booking/void.md) flow when the order is still inside the airline void window.

### Refund quotation and submission

#### `801` Order does not exist

The order number is wrong.

**Action**

* Check the original ticket order number

#### `809` Order not ticketed

Refund was requested before ticketing completed.

**Action**

* Wait until ticketing finishes
* Retry refund later

#### `811` Completed itineraries are not entered

The refund request does not include the required full itinerary.

**Typical causes**

* Missing one segment of a connection
* Partial refund on a round trip that must be handled together
* Sector already flown

**Action**

* Submit the full required itinerary
* Contact the airline or Atlas for partially flown cases

#### `814` Refund submission is in progress

A previous refund submission is still processing.

**Action**

* Wait before retrying

#### `816` / `817` / `818` Refund already submitted

A matching refund or claim already exists.

**Action**

* Do not resubmit
* Query refund status instead

### Void flow

Void uses dedicated endpoints and should follow the void quotation → void submission → void query sequence.

If the order is still inside the airline void window, use [Void](../../../product-guides/post-booking/void.md) instead of the refund flow.

#### `822` Exceed the ticket void deadline

The void request was submitted after the airline void window closed.

Atlas rejects this request immediately.

Typical message:

* `Void deadline exceeded. This ticket can no longer be voided`

**Action**

* Do not retry the same void submission
* Re-check whether the case should move to the refund flow

#### `823` Void not all pax

The void request does not cover the required passenger scope.

Atlas accepts full-order void only.

**Action**

* Do not submit void for only some passengers
* Submit the void only when the request covers the full order

### Query order

#### `703` No order found

The lookup parameters do not match an existing order.

**Action**

* Re-check `orderNo`, `airlinePNR`, and carrier values

#### `705` Timeout

The order retrieval request timed out.

**Action**

* Retry after a short wait

### Post-booking ancillaries

#### `117` Order is not in ticketed status

Ancillary search was attempted too early.

**Action**

* Wait until the original order is ticketed

#### `118` Ancillary not supported for this airline

Atlas cannot support this ancillary flow for the airline.

**Action**

* Check direct airline flow or open a service request

#### `502` Price changed during ancillary order

Ancillary price changed after search.

**Action**

* Search ancillary options again

#### `504` / `505` Additional baggage not allowed

The baggage was already added in the booking flow or in a previous post-booking order.

**Action**

* Do not submit duplicate baggage orders

### Quick retry guide

#### Wait, then retry

Examples:

* `809`
* `814`
* `117`
* `705`

#### Fix the request first

Examples:

* `801`
* `811`
* `822`
* `823`
* `703`
* `502`

#### Do not resubmit

Examples:

* `816`
* `817`
* `818`
* `504`
* `505`

### What comes next?

Use [Refunds](../../../product-guides/post-booking/refunds.md) for refund flow guidance.

Use [Void](../../../product-guides/post-booking/void.md) for the dedicated void flow.

Use [Query Order](../../../product-guides/booking/booking-step-guides/query-order/) when the current order state is still unclear.

Use [Post-booking](../../../product-guides/post-booking/) to route the case to the right post-booking workflow.

### Related pages

* [Refunds](../../../product-guides/post-booking/refunds.md)
* [Void](../../../product-guides/post-booking/void.md)
* [Post-booking](../../../product-guides/post-booking/)
* [Post-ticketing Ancillaries](../../../product-guides/post-booking/post-ticketing-ancillaries.md)
* [Order Maintenance](../../../product-guides/post-booking/order-maintenance.md)
