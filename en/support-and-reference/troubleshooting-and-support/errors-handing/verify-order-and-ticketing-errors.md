---
description: >-
  Common booking-flow errors from verification through order creation and ticket
  issuance.
---

# Verify, Order & Ticketing Errors

Use this page when failures happen after search and before final ticketing completes.

### 429 request-limit handling

Atlas may reject selected pre-booking requests with Atlas error code `429`.

This applies to:

* `verify.do` and `getOffers.do` with shared `60 QPM`
* `seatAvailability.do` and `getLuggage.do` with shared `60 QPM`

`order.do` and `pay.do` are not part of this request-limit policy.

**Action**

* read `retryAfter`
* wait for that delay before retrying
* lower request frequency and remove duplicate retries

### Verify-stage codes

#### `200` Illegal routing identifier

The `routingIdentifier` does not match a valid search result.

**Action**

* Use the latest identifier from search
* Do not modify the value

#### `202` Routing identifier expired

The identifier is older than 6 hours.

**Action**

* Run search again
* Use the new `routingIdentifier`

#### `206` / `207` No flights or target flight does not exist

Inventory changed after search.

**Action**

* Start from search again

#### `210` / `211` Fare family sold out or not found

Fare or cabin is no longer available.

**Action**

* Search again and re-select a valid offer

### Order-stage codes

#### `300` Invalid session information

The `sessionId` is wrong.

**Action**

* Use the `sessionId` returned by verify

#### `301` Session does not exist or timed out

The verification session is older than 2 hours.

**Action**

* If verify is still recent, repeat verify
* Otherwise start from search

#### `307` Illegal booking request parameters

One or more order fields are invalid.

This also includes inconsistent baggage selections across connected segments in the same direction.

Atlas may return baggage options per segment, but order validation still treats one direction as a single baggage choice for connecting flights.

**Action**

* Check `msg` for the exact invalid field
* Keep baggage consistent across all connected segments in each direction
* Resubmit after correction

#### `308` Price changed

Pricing changed between verify and order.

**Action**

* Restart from search or verify
* Reconfirm current price before booking

#### `309` Ancillary not found

The ancillary product code is invalid or outdated.

**Action**

* Re-read ancillary options from verify
* Use returned `productCode` values only

#### `312` / `315` Too many seats booked or not enough seats

Inventory changed or requested seat count exceeds availability.

**Action**

* Reduce seats or restart from search

#### `318` Duplicate booking

A booking with the same passenger and flight details may already exist.

**Action**

* Query existing orders before retrying

### Ticketing-stage codes

#### `602` / `603` Flight not found or sold out

The fare became unavailable after payment.

**Action**

* Start a new booking flow

#### `609` Contact email is blocked by airline

The airline rejected the supplied contact email.

**Action**

* Use another email
* Or use Atlas-generated contact email flow

#### `613` Payment rejected by airline risk control

The airline blocked fulfillment.

**Action**

* Try another card
* Or retry with deposit mode

#### `616` 3DS authentication required

Atlas cannot complete 3DS card authentication in this flow.

**Action**

* Use a non-3DS card
* Or pay with deposit mode

#### `617` Insufficient balance

Atlas deposit balance is too low at ticketing time.

**Action**

* Top up the account and retry

### Related pages

* [Verify](../../../product-guides/booking/booking-step-guides/verify.md)
* [Create Order](../../../product-guides/booking/booking-step-guides/create-order.md)
* [Payment & Ticketing](../../../product-guides/booking/booking-step-guides/payment-and-ticketing/)
* [Query Order](../../../product-guides/booking/booking-step-guides/query-order/)
