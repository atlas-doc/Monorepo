---
description: >-
  Atlas API seat flow for seat availability, seat selection support, and
  conversion-focused booking decisions.
---

# Seats

{% include "../../../../.gitbook/includes/eva-help-hint.md" %}

Use this page to build seat selection into the booking flow.

Start here when you need to:

* surface seat options before booking
* confirm whether seat selection is supported
* add seat choice to the booking experience

### Service scope

Atlas supports seat selection for these scenarios:

* airlines that support Atlas API seat capability
* Atlas-issued orders
* seat selection purchased with the ticket in the booking flow

Atlas does not support seat selection for these scenarios:

* non-Atlas-issued orders
* post-ticketing seat selection

A non-Atlas-issued order is ticketed by another party.

In this case, Atlas is only used to add seat service after ticketing.

### FAQ

#### When should I call `seatAvailability.do`?

Call `seatAvailability.do` as a recommended step before payment.

Seat choice helps improve traveler confidence and order conversion.

Call it after `verify.do`, `getOffers.do`, or `getOfferPrice.do`.

#### Which identifiers can I use?

Use a valid `sessionId` from `verify.do` or `OfferId` from `getOffers.do` or `getOfferPrice.do`.

Do not call it with flight data alone.

#### What happens if the selected seat becomes unavailable?

This is a fulfillment-stage rule.

It applies when the selected seat is no longer available at ticketing time.

Atlas supports these handling modes:

* `STOP_TICKET` — stop ticket issuance, cancel the whole order, and refund it
* `STOP_SEAT` — issue the ticket, remove the seat, and refund the seat amount
* `SIMILAR_SEAT` — issue the ticket with a similar seat selected by operations

For deposit customers, `STOP_SEAT` may require a split fund order and a `credit note`.

Atlas does not expose similarity rules for `SIMILAR_SEAT`.

If manual handling is needed, operations selects the similar seat in OPSDeck.

Choose the handling mode in the order creation request for that booking.

#### What request limit applies to `seatAvailability.do`?

`seatAvailability.do` shares one `60 QPM` ancillary pool with `getLuggage.do`.

Over-limit requests return Atlas error code `429`.

Honor the returned `retryAfter` value before retrying.

### Ancillary request limits

Atlas counts `seatAvailability.do` and `getLuggage.do` together in a rolling 60-second window.

The default shared limit is `60 QPM`.

One busy ancillary API can consume the shared pool for the other.

#### How to reduce limit pressure

Avoid repeated seat checks without a booking context change.

Cache the current `sessionId` or `OfferId` mapping upstream.

Honor `retryAfter` when `429` is returned.

### Main API

* `seatAvailability.do`

### SeatAvailability call rules

`seatAvailability.do` only supports transaction-linked calls.

Use one of these identifiers:

* `sessionId` from `verify.do`
* `OfferId` from `getOffers.do`
* `OfferId` from `getOfferPrice.do`

Independent mode is no longer available.

Flight-only seat quote requests are not supported.

### What should you confirm first?

Confirm that the airline supports seat selection for the current flow.

Confirm that the current session or offer context is still valid for the ancillary request.

Confirm that the seat request still maps to the original booking context.

### Use this when you need

* Seat map and seat upsell support
* Seat-selection support checks
* Seat decisions before payment

### Best practice

Choose the itinerary first.

Then query seats as a recommended conversion step before payment.

Position seat choice as a standard part of the booking journey.

Keep ancillary mapping consistent with the current booking context before `order.do`.

If your upstream seat request arrives without the current booking context, cache `sessionId` or `OfferId` first.

Then match the incoming flight to that cached `sessionId` or `OfferId`.

If no match exists, do not send a flight-only `seatAvailability.do` request.

### Notes

* Availability depends on airline support
* `seatAvailability.do` requires a valid `sessionId` or `OfferId`
* Flight-only seat requests are not supported
* Seat rules may vary by carrier
* Seat fulfillment handling should be chosen before `order.do`

### What comes next?

Use [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE) to send the selected ancillary data with the booking when required.

If you also need baggage options, use [Baggage](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ftzqh42LAaE6QYzklv67).

### Related pages

* [Verify](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm)
* [Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FSGess6buGE1P02WnVNu)
* [Get Offer Price](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/e7tapaArEz0MBOv62dxZ)
* [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE)
* [Baggage](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ftzqh42LAaE6QYzklv67)
* [Post-ticketing Ancillaries](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ltyid7j3wXhOy02L4UBm)

### Full API reference

See the complete endpoint schemas and samples here:

[Seat](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/33ZWa8YpkzEg8kPsZLCo)
