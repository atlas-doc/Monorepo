---
description: >-
  Atlas API void workflow overview for void-window checks, refund boundary
  decisions, and next-step routing.
---

# Void

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this section when the order may still qualify for void.

Start here when you need to:

* decide whether the case should use **Void** or **Refund**
* follow the standard void sequence
* confirm which identifiers to keep for follow-up

### FAQ

#### What is the standard Atlas API void flow?

The standard flow is `voidQuotation.do` → `void.do` → `queryVoidOrders.do`.

Request quotation first.

Then submit the void with the latest `voidOfferId`.

After submission, query status with `orderNo`.

Add `voidCode` when you want a specific void case.

#### When can a void request fail before submission?

Void can fail when the order is already outside the void window, the `orderNo` is wrong, or the quotation is no longer current.

Check current order state and request a fresh quotation first.

#### Does Atlas support partial-pax void?

No.

Atlas accepts full-order void only.

Do not plan a split-order or split-PNR workaround for Atlas void.

#### When should I use Void?

Use **Void** when the order is still inside the airline void window.

Start with quotation before submission.

#### When should I use Refund instead?

Use **Refunds** when the void window has passed or the case no longer qualifies for the dedicated void path.

Do not keep retrying void after the window closes.

### Current VOID coverage

Atlas VOID supports 23 airlines across four regions as of July 2026.

Coverage is airline-, route-, and account-specific.

#### Americas

* `AS`
* `DM`
* `F9`
* `G4`
* `PB`
* `SY`
* `TS`
* `Y4`

#### Europe

* `A3`
* `D8`
* `EI`
* `DY`
* `N0`
* `OA`
* `VF`
* `Z0`

#### Japan

* `ZG` — US routes only

#### Korea

* `7C`
* `BX`
* `LJ`
* `RS`
* `TW`
* `ZE`

Recent additions as of July 2026:

* `TS`
* `Y4`
* `EI`
* `VF`

If the booking is outside this scope, Atlas can return `843`.

### Typical flow

{% stepper %}
{% step %}
### Check void eligibility

Call `voidQuotation.do` first.

Confirm the order is still voidable.
{% endstep %}

{% step %}
### Submit the void

Use the latest `voidOfferId` from the quotation response.

Keep the returned `voidCode`.
{% endstep %}

{% step %}
### Query final status

Use `queryVoidOrders.do` with `orderNo` until the case is completed, rejected, or otherwise closed.

Add `voidCode` when you want to narrow the result to one void case.
{% endstep %}
{% endstepper %}

### What should you confirm before submission?

Confirm:

* the original `orderNo` is correct
* the order is still inside the void window
* the returned same-day deadline has not passed yet
* the latest `voidOfferId` is used
* the case should not move to the refund flow instead
* the request covers the full order, not only some passengers

### Which identifiers matter?

Keep these values through the flow:

* `orderNo` for quotation and query
* `voidOfferId` for submission
* `voidCode` for optional status filtering

Use the latest quotation result before submission.

Do not reuse an older `voidOfferId`.

Treat the returned deadline as strict.

After it passes, `void.do` is rejected immediately.

### Use this page when you need

* void eligibility checks
* void submission follow-up
* refund boundary decisions

### What this page does not cover

This page does not list full endpoint schemas or field-level definitions.

Use the API reference for request and response details.

### What comes next?

Open the endpoint page below for request and response details.

Then reconcile the outcome with the current order state.

### Full API reference

Use endpoint-level details here:

* [Void](../../api-reference/post-booking-apis/void.md)

### Related pages

* [Refunds](refunds.md)
* [Post-booking](./)
* [Post-booking APIs](../../api-reference/post-booking-apis/)
* [Refund, Query & Post-booking Errors](../../support-and-reference/troubleshooting-and-support/errors-handing/refund-query-and-post-booking-errors.md)
