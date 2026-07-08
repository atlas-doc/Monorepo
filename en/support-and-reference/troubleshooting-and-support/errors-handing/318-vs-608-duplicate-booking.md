---
description: >-
  How Atlas duplicate-booking errors 318 and 608 differ, and how to confirm
  whether an existing booking already succeeded before retrying.
---

# 318 vs 608 duplicate booking

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when Atlas signals a possible duplicate booking and you need to confirm whether a real booking already exists.

### Short answer

`318` is an order-stage duplicate booking signal.

`608` is a ticketing-stage duplicate booking signal.

Both mean you should check existing booking state before trying again.

### FAQ

#### What does `318` usually mean?

It means a booking with the same passenger and flight details may already exist during order creation.

#### What does `608` usually mean?

It means duplicate booking was identified during ticketing.

#### Should I retry immediately?

No.

Check whether the booking already exists first.

### Core difference

#### `318` — duplicate booking at order creation

**Failed stage**

`order.do`

**What it usually means**

Atlas believes the same passenger and itinerary may already have an order.

**Next action**

Check existing orders before retrying.

#### `608` — duplicate booking at ticketing

**Failed stage**

Ticketing or post-payment fulfillment

**What it usually means**

A duplicate booking was identified later in the fulfillment chain.

**Next action**

Do not start a new booking blindly.

Check whether the traveler already has a confirmed booking.

### What to check first

When these codes appear, check:

* whether an order already exists for the same passenger and itinerary
* whether payment already succeeded on an earlier order
* whether airline PNR or ticket numbers already exist
* whether a prior retry created a second attempt

### Quick decision rule

Use this rule in production:

* `318` — search for an existing order before another `order.do`
* `608` — inspect fulfillment outcome before any new booking or payment action

### Common mistakes

#### Treating duplicate-booking signals like ordinary failures

Do not do this.

A new retry may create a real duplicate traveler booking.

#### Retrying from the start without checking existing orders

Do not do this.

Confirm whether the traveler already has a valid booking first.

#### Ignoring partial success after payment or ticketing activity

Do not do this.

A duplicate signal can happen after business processing already moved forward.

### Best practice

Use passenger name, itinerary, travel date, and any existing `orderNo` or airline PNR to reconcile the current state before another booking action.

### Related pages

* [Query Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n)
* [Polling and Ticketing Timing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2qOXdnt78bFPEFbkcemP)
* [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE)
* [Payment & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB)
* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)
* [Verify, Order & Ticketing Errors](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/xgMYjsnxo91kS8079G1O)
