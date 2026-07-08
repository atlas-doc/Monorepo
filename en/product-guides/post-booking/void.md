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

After submission, query status with `voidCode` until the case is closed.

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

Atlas VOID currently supports 23 airlines across four regions.

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

Recent additions:

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

Use `queryVoidOrders.do` until the case is completed, rejected, or otherwise closed.
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

* `orderNo` for quotation
* `voidOfferId` for submission
* `voidCode` for status follow-up

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

* [Void](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/H8SaqS9SfWWq494hZlz5)

### Related pages

* [Refunds](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/BrRnHjluVQUVmDfiLe3t)
* [Post-booking](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/R6rkbsTfrs5gZzElecNB)
* [Post-booking APIs](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/8P9YQq692vHSOmVjquJF)
* [Refund, Query & Post-booking Errors](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/XUINxYxfOsv9CDtmb1pl)
