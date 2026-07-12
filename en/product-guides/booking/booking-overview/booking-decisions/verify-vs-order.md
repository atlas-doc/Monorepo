---
description: Decide whether an Atlas API booking request belongs in verify.do or order.do.
---

# Verify vs Order

{% include "../../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when you need to decide whether a booking problem belongs to `verify.do` or `order.do`.

### Short answer

Use `verify.do` to validate the current booking context.

Use `order.do` to create the actual booking.

`verify.do` tells you what is required.

`order.do` commits the booking request.

### FAQ

#### What is the main job of `verify.do`?

It refreshes fare, routing, and booking requirements.

It returns the `sessionId` and `bookingRequirement` you need for order creation.

#### What is the main job of `order.do`?

It creates the order.

It uses the verified context, passenger data, contact data, and ancillary selections.

#### Can I skip `verify.do` in the standard search flow?

No.

In the standard search flow, `order.do` depends on the `sessionId` returned by `verify.do`.

### Where the boundary sits

#### `verify.do`

Use it to answer:

* is the itinerary still valid
* what is the latest fare
* what passenger and document fields are required
* what `sessionId` should the order use

#### `order.do`

Use it to answer:

* can Atlas create the booking now
* does the passenger data satisfy the booking requirement
* do the ancillary selections still match the current context
* what `orderNo` should payment use next

### What each step returns

#### `verify.do` returns

* `sessionId`
* latest fare and routing context
* `bookingRequirement`
* ancillary context

#### `order.do` returns

* `orderNo`
* order status
* booking outcome tied to the current request

### What usually fails at verify?

Typical verify-stage failures include:

* expired `routingIdentifier`
* flight sold out after search
* target flight changed
* fare family sold out
* transient verify timeout

Typical codes include:

* `202`
* `205`
* `206`
* `207`
* `210`
* `299`

### What usually fails at order creation?

Typical order-stage failures include:

* expired `sessionId`
* passenger data missing or invalid
* stale ancillary `productCode`
* price changed after verify
* flight sold out before booking commit

Typical codes include:

* `301`
* `302`
* `307`
* `308`
* `309`
* `410`

### Decision guide

#### Use `verify.do` again when

* the current `sessionId` expired
* booking was delayed
* you need the latest `bookingRequirement`
* you need the current fare context again

#### Use `order.do` when

* the `sessionId` is still fresh
* passenger and contact data are complete
* ancillary selections match the current context
* you are ready to create the booking

### Common mistakes

#### Treating verify as optional validation only

Do not do this.

In the standard flow, it is the source of truth for `sessionId` and `bookingRequirement`.

#### Building the order from stale verify data

Do not do this.

Refresh verify when booking-critical input changed or the booking was delayed.

#### Expecting `order.do` to decide missing field requirements for you

Do not do this.

Read `bookingRequirement` first.

### Best practice

Right before `order.do`, confirm:

* `sessionId` is still valid
* `bookingRequirement` is the latest one
* passenger data matches required fields
* ancillary mapping matches the current verify context

### Related pages

* [Booking Overview](../)
* [Identifiers](../identifiers.md)
* [Verify](../../booking-step-guides/verify.md)
* [Create Order](../../booking-step-guides/create-order.md)
* [202 vs 301 vs 308](../../../../support-and-reference/troubleshooting-and-support/errors-handing/202-vs-301-vs-308.md)
* [Verify, Order & Ticketing Errors](../../../../support-and-reference/troubleshooting-and-support/errors-handing/verify-order-and-ticketing-errors.md)
