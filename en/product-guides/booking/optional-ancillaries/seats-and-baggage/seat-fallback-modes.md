---
description: >-
  How STOP_TICKET, STOP_SEAT, and SIMILAR_SEAT differ when selected seats are
  unavailable at fulfillment time.
---

# Seat fallback modes

{% include "../../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when your booking flow includes paid seats and you must decide what Atlas should do if the selected seat is no longer available.

### Short answer

Use `STOP_TICKET` when the seat is mandatory for the booking.

Use `STOP_SEAT` when ticketing matters more than the seat.

Use `SIMILAR_SEAT` when Atlas may complete ticketing with an alternative seat.

### FAQ

#### When are these modes used?

They apply when the selected seat is unavailable at fulfillment time.

You choose the mode in `order.do`.

#### Does the mode affect ticket issuance?

Yes.

Each mode defines whether Atlas should stop ticketing, continue without the seat, or continue with a similar seat.

#### Is similarity logic exposed in the API?

No.

Atlas does not expose similarity rules for `SIMILAR_SEAT`.

### Core difference

#### `STOP_TICKET`

**What it does**

Stops ticket issuance.

Cancels the whole order.

Refunds it.

**Use it when**

Use it when the selected seat is business-critical.

This fits products where losing the seat means the traveler should not be ticketed.

#### `STOP_SEAT`

**What it does**

Issues the ticket.

Removes the seat.

Refunds the seat amount.

**Use it when**

Use it when ticketing matters more than seat certainty.

This fits products where travel should continue even if the paid seat fails.

**Operational note**

For deposit customers, this may require a split fund order and a `credit note`.

#### `SIMILAR_SEAT`

**What it does**

Issues the ticket with a similar seat selected by operations.

**Use it when**

Use it when the traveler wants a seat outcome but does not need the exact original seat.

**Operational note**

If manual handling is needed, operations selects the similar seat in OPSDeck.

### Quick decision rule

Use this rule in production:

* exact seat is mandatory — `STOP_TICKET`
* trip must continue even without the seat — `STOP_SEAT`
* similar seat is acceptable — `SIMILAR_SEAT`

### Common mistakes

#### Leaving the mode undefined in the business design

Do not do this.

A missing business rule makes seat-failure handling unpredictable.

#### Choosing `STOP_TICKET` for low-value seat upsell

Do not do this by default.

It can cancel the whole booking for a non-critical ancillary.

#### Choosing `SIMILAR_SEAT` without business acceptance

Do not do this.

Your product team must accept that the final seat may differ.

### Best practice

Set the fallback mode as a product decision, not only as a technical field.

Decide it before `order.do` and keep it consistent with your traveler promise.

### Related pages

* [Seats](./)
* [Create Order](../../booking-step-guides/create-order.md)
* [Payment & Ticketing](../../booking-step-guides/payment-and-ticketing/)
* [Baggage and seat productCode freshness](../baggage-and-seat-productcode-freshness.md)
* [Error Codes](../../../../support-and-reference/troubleshooting-and-support/errors-handing/)
