---
description: >-
  Definitions of Atlas API booking flows, identifiers, order lifecycle terms,
  and integration concepts.
---

# Atlas API concepts

This glossary defines the terms used across Atlas API documentation.

Use it to interpret workflow guides, endpoint references, and error guidance consistently.

### What is Atlas API?

Atlas API supports flight shopping, booking, payment, ticketing, and post-booking operations.

Start with [What is Atlas API?](../what-is-atlas-api.md) for product capabilities and documentation entry points.

### Booking flows

#### Standard booking

The standard path starts with `search.do`.

It uses `routingIdentifier` for `verify.do`, then `sessionId` for `order.do`.

See [Standard booking](../product-guides/booking/booking-flows/standard-booking-flow.md).

#### Get Offer

Get Offer prices a known itinerary with `getOffers.do`.

It returns an `OfferId` used for order creation.

See [Get Offer](../product-guides/booking/booking-flows/get-offer-flow.md).

#### Fulfilment API

Fulfilment API uses `getOfferPrice.do` to price an offer.

Its flow uses a short-lived `OfferId` and fast payment after order creation.

See [Fulfilment API](../product-guides/booking/booking-flows/fulfillment-flow.md).

### Core identifiers

#### `routingIdentifier`

`search.do` returns this route token.

Pass it to `verify.do` in the standard booking flow.

#### `sessionId`

`verify.do` returns this booking context.

Pass it to `order.do` in the standard booking flow.

#### `OfferId`

`getOffers.do` or `getOfferPrice.do` returns this offer context.

Use it for `order.do` in its matching booking flow.

#### `orderNo`

`order.do` returns the Atlas order identifier.

Use it for payment, order queries, ticketing follow-up, and post-booking actions.

See [Identifiers](../product-guides/booking/booking-overview/identifiers.md) for validity periods, flow mapping, and refresh rules.

### Order lifecycle

An order is created with `order.do`.

Payment and ticketing start through `pay.do` where the flow requires it. Use `queryOrderDetails.do` to check order status and ticketing progress.

See [Payment & Ticketing](../product-guides/booking/booking-step-guides/payment-and-ticketing/) and [Query Order](../product-guides/booking/booking-step-guides/query-order/).

### Webhooks and incidents

A webhook delivers Atlas event notifications to your endpoint.

Use webhooks for ticketing, void, schedule-change, airline-status, email, and incident notifications.

See [Webhook Overview](../product-guides/extensions-and-integrations/webhook-overview/).

### Related documentation

* [Product Guides](../product-guides/)
* [API Reference](../api-reference/)
* [Atlas API FAQs](troubleshooting-and-support/faqs/)
