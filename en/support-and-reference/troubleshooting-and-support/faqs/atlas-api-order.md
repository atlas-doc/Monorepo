---
description: >-
  Common Atlas API order and ticketing questions about hold time, contact email,
  polling, split orders, and ancillaries.
---

# Orders & Ticketing

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page for order hold, contact email, split orders, and ancillary mapping questions.

Start here when you need to:

* understand what happens after `order.do`
* confirm how to handle `pay.do` and ticketing polling
* decide how to work with airline PNR, split orders, or ancillaries

### FAQ

#### Does `order.do` hold inventory and price?

Yes.

Atlas holds inventory and price for 30 minutes after order creation.

If payment is not completed in that window, the hold expires.

This 30-minute rule applies to the standard booking flow.

Orders created from `getOfferPrice.do` use a 5-minute fulfillment window instead.

### Does `order.do` hold inventory?

Yes.\
Atlas holds inventory and price for 30 minutes after order creation.

If payment is not completed in that window, the hold expires.

For fulfillment-flow orders created from `getOfferPrice.do`, the operational window is 5 minutes.

### Can we manually release held inventory?

No.\
Atlas releases it automatically after the hold period.

### Which email should we send in booking contact details?

You can use either:

* the traveler email
* your agency email
* an Atlas-generated email

Some airlines block repeated bookings from the same email address.\
To reduce that risk, use `useAtlasMailForContact`.

### What does `useAtlasMailForContact` do?

* `true`: Atlas generates a unique booking email and sends that to the airline
* `false`: Atlas uses the email you send in `order.do`

When Atlas-generated email is used, airline replies may appear in ATRIP email records.\
Delivery is best effort, not guaranteed.

If your own email is blocked by the airline, Atlas may cancel the booking and return error `321`.

#### Do we need to poll after `pay.do`?

Yes.

Payment and ticket issuance are not always the same moment.

Use `queryOrderDetails.do` until the order reaches the final ticketed state.

### Do we need to poll after `pay.do`?

Yes.\
Payment and ticket issuance are not always the same moment.

Use `queryOrderDetails.do` until the order reaches the final ticketed state.\
Webhook can help, but it should not be your only confirmation path.

### Is `pnrCode` the airline PNR?

No.\
`pnrCode` is the Atlas booking reference.

The airline PNR is returned later in order query after the airline generates it.

#### How should we handle split orders for round trips?

Use `allowGenerateMultipleOrders: true` when the itinerary may split into separate one-way orders.

Read each returned `orderNo` separately and pay each supported order separately.

### When do airline PNR and ticket numbers appear?

They appear after ticketing completes.\
Read them from `paxTicketInfos.airlinePNRs` and `ticketNos` in order query.

### What should we do if ticketing is still processing?

Do not retry payment blindly.\
Query the order state first.

Wait for final `orderStatus` and `ticketStatus`, or reconcile with webhook events if configured.

### Which seat selection scenarios are supported?

Atlas supports seat selection for airlines that support Atlas API seat capability.

Atlas supports Atlas-issued orders and seat selection purchased with the ticket in the booking flow.

Atlas does not support non-Atlas-issued orders or post-ticketing seat selection.

See [Seats](../../../product-guides/booking/optional-ancillaries/seats-and-baggage/) for the current support scope.

### Can VCC be used for a round trip built from two one-way fares?

Yes, but the booking may split into two separate orders.

Use:

* `allowGenerateMultipleOrders: true`

If Atlas cannot issue the itinerary as one round trip, it may return two comma-separated `orderNo` values.

### How should split-order payment work?

1. Create the order with `allowGenerateMultipleOrders: true`
2. Read each returned order separately
3. Call payment separately for each order

Check payment support for each returned order before paying.

### How should ancillaries be sent for connecting flights?

Every flown segment must have its own `segmentIndex` entry.

If verification returns two segments, the order request must also include two ancillary entries when the product applies to both segments.

#### How should ancillaries be mapped for connecting flights?

Map ancillaries at the flown-segment level.

If a product applies to two segments, send one entry per `segmentIndex`.

### Example

If one baggage product applies across a two-segment journey, send:

```json
"ancillaries": [
  {
    "productCode": "SCI_BAG_1PC_20KG",
    "segmentIndex": "1"
  },
  {
    "productCode": "SCI_BAG_1PC_20KG",
    "segmentIndex": "2"
  }
]
```

### Related pages

* [Create Order](../../../product-guides/booking/booking-step-guides/create-order.md)
* [Payment & Ticketing](../../../product-guides/booking/booking-step-guides/payment-and-ticketing/)
* [Query Order](../../../product-guides/booking/booking-step-guides/query-order/)
