---
description: FR-only order confirmation step before payment.
---

# Confirm Order (FR only)

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page only for FR booking flows.

This page uses `Confirm Order` as the primary name.

You may also see this step called `Order Commit`.

{% hint style="info" %}
Most airlines do not use this step.

For standard booking flows, call `order.do` and then `pay.do`.

Only FR inserts `orderCommit.do` between those two steps.
{% endhint %}

### Main API

* `orderCommit.do`

### When this step applies

Use `Confirm Order` only when:

* the airline is FR
* the booking flow returns an FR confirmation page
* the user must complete FR confirmation before payment

Skip this step when:

* the airline is not FR
* the order can go directly from `order.do` to `pay.do`

If you are building a standard booking flow, do not add `Confirm Order` as a required step.

### Where it sits in the flow

#### Standard flow

* `verify.do`
* `order.do`
* `pay.do`

#### FR flow

* `verify.do`
* `order.do`
* `orderCommit.do`
* user completes FR confirmation
* `pay.do`

### Notes

* This step is airline-specific
* It is required for FR
* Payment must wait until FR confirmation finishes
* `Confirm Order` and `Order Commit` are the same step

### What you get back

Atlas returns a `confirmationUrl`.

Use it in:

* popup mode
* iframe mode

### Related pages

* [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE)
* [Payment & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB)
* [FR Integration](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/HyzW7wts21GuPr6cO9gM)
* [Booking APIs](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/beDx3cjbYPiOQ1Pwk6bC)

### Full API reference

See endpoint-level details here:

* [Confirm Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ReW5cc40i6p8ngk42VF3)
