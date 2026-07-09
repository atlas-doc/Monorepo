---
description: >-
  A short pre-read for partners before kickoff, covering the main questions
  about flow choice, pricing, payment, ticketing, and launch readiness.
---

# Top Questions for Partners

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page as a short pre-read before the first integration call.

It is written for business, product, and technical stakeholders together.

### 1. Which booking flow should we use?

Use `search.do` when Atlas is your main shopping source.

Use `getOffers.do` when you already know the itinerary or need an independent real-time price check.

The standard flow is:

1. `search.do`
2. `verify.do`
3. `order.do`
4. `pay.do`
5. `queryOrderDetails.do`

See [Booking Overview](../../../product-guides/booking/booking-overview/).

### 2. Why can search price and booking price differ?

Search may use cached data.

Verify or Get Offer checks live fare and availability before booking.

Use the latest verified or offered price as the source of truth.

### 3. How should we protect price integrity?

Keep the refresh point close to booking.

Avoid long delays between price check and order creation.

Treat price refresh as a required business rule, not only a technical detail.

### 4. Does Atlas support fare families, baggage, and seats?

Yes, but support depends on airline and flow.

Fare families can be returned in search.

Baggage and seat queries should stay optional unless they are required for conversion.

See [Seats](../../../product-guides/booking/optional-ancillaries/seats-and-baggage/) and [Baggage](../../../product-guides/booking/optional-ancillaries/baggage.md).

### 5. Which payment modes are available?

The main options are:

* **Deposit**
* **VCC pass-through**

Atlas does not issue VCC cards.

You provide the card details when VCC pass-through is used.

See [Payments](atlas-api-payments.md).

### 6. Is ticketing synchronous?

Not always.

Payment and final ticket issuance may complete at different times.

Your system should poll order status after payment until the final state is confirmed.

### 7. Is `pnrCode` the airline PNR?

No.

`pnrCode` is the Atlas booking reference.

The airline PNR appears later after ticketing and should be read from order query.

### 8. Are webhooks enough for status tracking?

No.

Webhook delivery is best effort.

Use webhook as a helpful signal, not the only source of truth.

Your final reconciliation path should still include order query and airline communication when needed.

### 9. How are refunds and changes handled?

Refund behavior depends on payment mode.

VCC refunds usually return to the original card.

Deposit refunds are credited back after Atlas receives airline funds.

Booking changes are generally handled through ATRIP service requests, not a generic self-service API flow.

See [Post-booking](atlas-api-post-ticketing.md).

### 10. What should be ready before UAT and go-live?

Before UAT:

* sandbox integration is stable end to end
* main booking flow is working
* identifiers and authentication are handled correctly
* webhook handling is ready if required

Before go-live:

* UAT is approved
* production credentials are generated
* IP whitelist is ready
* endpoints are switched correctly
* first live orders can be monitored closely

See:

* [UAT Validation](../../../readme-1/uat-submission-guide.md)
* [Production Go-Live](../../../readme-1/production-go-live.md)

### If you only align 5 things first

Start with these:

* chosen booking flow
* price refresh rule
* payment mode
* polling and final status rule
* post-booking ownership

### Related pages

* [Before Integration](before-integration.md)
* [Kickoff Checklist](kickoff-checklist.md)
* [FAQs](./)
