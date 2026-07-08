---
description: >-
  Latest Atlas API documentation updates, new guides, troubleshooting changes,
  and recommended next reads.
---

# 📣 Atlas API Documentation Updates

{% include ".gitbook/includes/eva-help-hint.md" %}

Use this page to track the latest Atlas API documentation updates and jump to the right guide faster.

Use it as the update feed for **Support & Reference** when you want the newest guidance, revised troubleshooting content, or newly added entry points.

{% hint style="success" %}
Latest update: Atlas VOID coverage now includes 23 airlines across four regions, with new support for `TS`, `Y4`, `EI`, and `VF`.
{% endhint %}

It highlights new guides, major troubleshooting improvements, and the next pages to read by use case.

Start here if you need to:

* find the newest Atlas API guides
* see what changed for sandbox, booking, payment, or troubleshooting
* choose the right page to read next

### FAQ

#### What changed in the Atlas API docs recently?

Recent updates added booking-flow identifier guidance, clarified when to use `search.do` versus `getOffers.do`, explained `429` versus `110`, added decision guidance for `202` versus `301` versus `308`, clarified the Verify versus Create Order boundary, added polling guidance after `pay.do`, clarified payment-state recovery for `401`, `402`, `404`, `406`, and `615`, documented ancillary `productCode` freshness, added restart guidance for Search versus Verify versus Get Offer, clarified booking input errors `307`, `327`, and `410`, clarified ancillary mapping errors `309` and `409`, documented seat fallback modes, clarified transient verify and order failures `205`, `299`, and `304`, documented duplicate booking handling for `318` and `608`, added request-limit guidance for selected pre-booking APIs, published multi-channel notification setup, updated the ATRIP UAT flow, refined void guidance, and clarified seat-availability calling rules.

Use the change log below when you need page-level detail.

#### Where should a new integration team start?

Start with [Quick Start](readme-1/quick-start.md).

Then use [Integration Guides](readme-1/), [Booking Overview](product-guides/booking/booking-overview/), and [Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/).

#### Which pages should I check for request-limit guidance?

Start with [Booking Overview](product-guides/booking/booking-overview/), [Search](product-guides/booking/booking-step-guides/search.md), [Search & Booking](support-and-reference/troubleshooting-and-support/faqs/atlas-api-search-and-book.md), and [Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/).

### Popular starting points

#### New integration

Start with [Quick Start](readme-1/quick-start.md) and [Integration Guides](readme-1/).

#### Booking flow

Start with [Booking Overview](product-guides/booking/booking-overview/) and [Search & Booking](support-and-reference/troubleshooting-and-support/faqs/atlas-api-search-and-book.md).

Use [Identifiers](product-guides/booking/booking-overview/identifiers.md) when you need the right token for the next step.

Use [Verify vs Create Order](product-guides/booking/booking-overview/booking-decisions/verify-vs-order.md) when the booking boundary is the main question.

Use [Restart from Search vs Verify vs Get Offer](product-guides/booking/booking-overview/booking-decisions/restart-point.md) when the main question is where to restart.

Use [Seat fallback modes](product-guides/booking/optional-ancillaries/seats-and-baggage/seat-fallback-modes.md) when paid seat failure behavior must be defined before booking.

#### Troubleshooting

Start with [Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/) and [FAQs](support-and-reference/troubleshooting-and-support/faqs/).

Use [429 vs 110](support-and-reference/troubleshooting-and-support/errors-handing/429-vs-110.md) when request frequency or search concurrency is the main issue.

Use [202 vs 301 vs 308](support-and-reference/troubleshooting-and-support/errors-handing/202-vs-301-vs-308.md) when you need to know which earlier step must be refreshed.

Use [402 vs 404 vs 406 vs 615](support-and-reference/troubleshooting-and-support/errors-handing/402-vs-404-vs-406-vs-615.md) when the main risk is duplicate or unnecessary payment retry.

Use [307 vs 327 vs 410](support-and-reference/troubleshooting-and-support/errors-handing/307-vs-327-vs-410.md) and [309 vs 409](support-and-reference/troubleshooting-and-support/errors-handing/309-vs-409.md) when order input or ancillary mapping is the main failure area.

Use [401 vs 402 vs 404](support-and-reference/troubleshooting-and-support/errors-handing/401-vs-402-vs-404.md) when the main question is whether the order expired or was already paid.

### Latest Atlas API documentation updates

#### VOID airline coverage expansion

Updated the VOID documentation to show the current supported airline scope.

What changed:

* documented 23 supported VOID airlines across the Americas, Europe, Japan, and Korea
* marked `ZG` as supported only for US routes
* added the latest newly supported airlines: `TS`, `Y4`, `EI`, and `VF`

Read next:

* [Void workflow](product-guides/post-booking/void.md)
* [Void](api-reference/post-booking-apis/void.md)
* [Refund, Query & Post-booking Errors](support-and-reference/troubleshooting-and-support/errors-handing/refund-query-and-post-booking-errors.md)

#### Fulfillment API and `getOfferPrice.do` launch

Published new fulfillment guidance for the `getOfferPrice.do` flow and updated key booking pages with its timing and request-limit rules.

What changed:

* added [Fulfillment API](product-guides/booking/booking-step-guides/get-offer-price.md) for the new fulfillment-oriented booking path
* added [Get Offer vs Fulfillment API](product-guides/booking/booking-overview/booking-decisions/get-offer-vs-get-offer-price.md) to clarify when to use `getOffers.do` versus `getOfferPrice.do`
* added [Get Offer Price](api-reference/booking-apis/get-offer-price.md) under API Reference
* updated [Booking Overview](product-guides/booking/booking-overview/), [Payment & Ticketing](product-guides/booking/booking-step-guides/payment-and-ticketing/), [Query Order](product-guides/booking/booking-step-guides/query-order/), [Create Order](product-guides/booking/booking-step-guides/create-order.md), [Orders & Ticketing](support-and-reference/troubleshooting-and-support/faqs/atlas-api-order.md), and [API Request Limits](product-guides/booking/booking-overview/api-request-limits.md)

Read next:

* [Fulfillment API](product-guides/booking/booking-step-guides/get-offer-price.md)
* [Payment & Ticketing](product-guides/booking/booking-step-guides/payment-and-ticketing/)
* [API Request Limits](product-guides/booking/booking-overview/api-request-limits.md)

#### Payment timeout, transient failure, and duplicate-booking clarification pack

Published three new pages for payment deadline recovery, transient booking-stage failures, and duplicate-booking handling.

What changed:

* added [401 vs 402 vs 404](support-and-reference/troubleshooting-and-support/errors-handing/401-vs-402-vs-404.md) to distinguish expired payment windows from non-payable or already-paid order states
* added [205 vs 299 vs 304](support-and-reference/troubleshooting-and-support/errors-handing/205-vs-299-vs-304.md) to clarify when to retry once, restart from search, or escalate transient verify and order failures
* added [318 vs 608 duplicate booking](support-and-reference/troubleshooting-and-support/errors-handing/318-vs-608-duplicate-booking.md) to clarify how to confirm existing booking state before retrying

Read next:

* [Payment Errors](support-and-reference/troubleshooting-and-support/errors-handing/payment-errors.md)
* [Verify, Order & Ticketing Errors](support-and-reference/troubleshooting-and-support/errors-handing/verify-order-and-ticketing-errors.md)
* [Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/)

#### Input validation and seat fallback clarification pack

Published three new pages for order input troubleshooting, ancillary mapping, and seat failure behavior.

What changed:

* added [307 vs 327 vs 410](support-and-reference/troubleshooting-and-support/errors-handing/307-vs-327-vs-410.md) to distinguish generic order-field issues, booking-requirement mismatches, and contact phone formatting errors
* added [309 vs 409](support-and-reference/troubleshooting-and-support/errors-handing/309-vs-409.md) to distinguish stale ancillary codes from baggage segment-mapping errors
* added [Seat fallback modes](product-guides/booking/optional-ancillaries/seats-and-baggage/seat-fallback-modes.md) to explain `STOP_TICKET`, `STOP_SEAT`, and `SIMILAR_SEAT`

Read next:

* [Create Order](product-guides/booking/booking-step-guides/create-order.md)
* [Seats](product-guides/booking/optional-ancillaries/seats-and-baggage/)
* [Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/)

#### Payment-state and ancillary freshness clarification pack

Published three new pages for payment recovery, ancillary reuse safety, and flow restart decisions.

What changed:

* added [402 vs 404 vs 406 vs 615](support-and-reference/troubleshooting-and-support/errors-handing/402-vs-404-vs-406-vs-615.md) to clarify when to query order, wait, or avoid another `pay.do`
* added [Baggage and seat productCode freshness](product-guides/booking/optional-ancillaries/baggage-and-seat-productcode-freshness.md) to explain when ancillary selections are stale
* added [Restart from Search vs Verify vs Get Offer](product-guides/booking/booking-overview/booking-decisions/restart-point.md) to explain the earliest booking step that must be rerun

Read next:

* [Payment & Ticketing](product-guides/booking/booking-step-guides/payment-and-ticketing/)
* [Booking Overview](product-guides/booking/booking-overview/)
* [Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/)

#### Booking recovery and timing clarification pack

Published three new pages for booking-stage recovery decisions and post-payment follow-up.

What changed:

* added [202 vs 301 vs 308](support-and-reference/troubleshooting-and-support/errors-handing/202-vs-301-vs-308.md) to explain when to refresh search, refresh verify, or rebuild the booking context
* added [Verify vs Create Order](product-guides/booking/booking-overview/booking-decisions/verify-vs-order.md) to clarify the validation boundary before booking creation
* added [Polling and Ticketing Timing](product-guides/booking/booking-step-guides/query-order/post-payment-polling.md) to explain why payment success does not always mean final ticketing

Read next:

* [Booking Overview](product-guides/booking/booking-overview/)
* [Payment & Ticketing](product-guides/booking/booking-step-guides/payment-and-ticketing/)
* [Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/)

#### Booking flow clarification pack

Published three new pages for common integration questions around flow choice, identifier handling, and request-pressure troubleshooting.

What changed:

* added [Identifiers](product-guides/booking/booking-overview/identifiers.md) for `routingIdentifier`, `sessionId`, `OfferId`, `orderNo`, and fresh-identifier rules
* added [Search vs Get Offer](product-guides/booking/booking-overview/booking-decisions/search-vs-offer.md) to clarify when to use `search.do` versus `getOffers.do`
* added [429 vs 110](support-and-reference/troubleshooting-and-support/errors-handing/429-vs-110.md) to distinguish request-limit governance from search concurrency pressure

Read next:

* [Booking Overview](product-guides/booking/booking-overview/)
* [Search & Booking](support-and-reference/troubleshooting-and-support/faqs/atlas-api-search-and-book.md)
* [Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/)

#### QPS and QPM request limit governance

Published new request-limit guidance for selected pre-booking APIs.

What changed:

* documented Atlas error code `429` behavior for over-limit requests
* added shared-pool rules for `verify.do` and `getOffers.do`, and for `seatAvailability.do` and `getLuggage.do`
* added retry guidance for `retryAfter`, request pacing, and duplicate-search reduction

Read next:

* [Booking Overview](product-guides/booking/booking-overview/)
* [Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/)
* [Search & Booking](support-and-reference/troubleshooting-and-support/faqs/atlas-api-search-and-book.md)

#### Multi-channel notifications launch

Published the new Atlas notification setup guidance for ATRIP delivery across webhook, email, DingTalk, WeCom, Slack, and Teams.

What changed:

* added a new setup guide for multi-channel notifications in ATRIP
* clarified that webhook is one delivery option in the notification model
* linked airline status updates to the first live multi-channel scenario

Read next:

* [Multi-channel Notifications](product-guides/extensions-and-integrations/multi-channel-notifications.md)
* [Webhook Overview](product-guides/extensions-and-integrations/webhook-overview/)
* [Airline Status Update Notification](product-guides/extensions-and-integrations/webhook-overview/airline-status-update-notification.md)

#### Standard headers cleanup

Updated the sandbox access guidance to remove an unnecessary standard request header.

What changed:

* removed `Accept: application/json` from the standard headers list
* kept `Accept-Encoding`, `Authorization`, and `Content-Type` guidance unchanged

Read next:

* [Sandbox Access](readme-1/making-requests.md)
* [Quick Start](readme-1/quick-start.md)

#### UAT Testing flow update

Updated the UAT documentation to reflect the current ATRIP validation flow.

What changed:

* UAT now starts in **UAT Testing**
* partners must choose the target function scope before continuing
* **flight booking** is the required core function
* **Submit Verification** now triggers automatic validation and returns failure reasons directly

Read next:

* [UAT Validation](readme-1/uat-submission-guide.md)
* [Quick Start](readme-1/quick-start.md)
* [Getting Started](support-and-reference/troubleshooting-and-support/faqs/atlas-api-general-information.md)

#### Void workflow and notification updates

Updated the void documentation to reflect the current post-booking flow and webhook handling.

What changed:

* clarified the standard flow: `voidQuotation.do` → `void.do` → `queryVoidOrders.do`
* added stronger guidance for `voidOfferId`, `voidCode`, and void-window checks
* expanded `order.void` webhook coverage, status values, and retry-failure behavior

Read next:

* [Void workflow](product-guides/post-booking/void.md)
* [Void](api-reference/post-booking-apis/void.md)
* [Void Notification](product-guides/extensions-and-integrations/webhook-overview/void-notification.md)

#### SeatAvailability call rules update

Updated the seat-selection guidance to reflect the current `seatAvailability.do` calling rules.

What changed:

* independent mode is no longer available
* `seatAvailability.do` now requires `sessionId` from `verify.do` or `OfferId` from `getOffers.do`
* flight-only seat quote requests are not supported

Read next:

* [Inflow Seat & Baggage](api-reference/booking-apis/inflow-seat-and-baggage.md)
* [Seats & Baggage](product-guides/booking/optional-ancillaries/seats-and-baggage/)
* [Verify](product-guides/booking/booking-step-guides/verify.md)

#### MCP-Assisted Development

Read [MCP-Assisted Development](readme-1/integration-tools/mcp-assisted-development.md) when you want to use GitBook MCP during Atlas API integration.

Best for:

* teams starting a sandbox build
* developers mapping the booking flow
* teams routing implementation questions faster

Read next:

* [Quick Start](readme-1/quick-start.md)
* [API Reference](api-reference/)

#### Sandbox Validation Test Kit

Read [Sandbox Validation Test Kit](readme-1/sandbox-development/sandbox-validation-test-kit.md) when you need a no-code sandbox validation run before development or after environment changes.

Best for:

* validate sandbox credentials before coding
* confirm network access and core booking flow readiness
* teams rechecking sandbox health after credential or IP changes

Read next:

* [Sandbox Development](readme-1/sandbox-development/)
* [UAT Validation](readme-1/uat-submission-guide.md)

#### Error Codes improvements

[Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/) now works better as the main troubleshooting entry point.

Best for:

* teams handling high-frequency integration failures
* developers defining safe retry behavior
* operations teams checking likely root causes

Read next:

* [Common & Access Errors](support-and-reference/troubleshooting-and-support/errors-handing/common-and-access-errors.md)
* [Verify, Order & Ticketing Errors](support-and-reference/troubleshooting-and-support/errors-handing/verify-order-and-ticketing-errors.md)

### Start here by use case

#### New Atlas API integration

Start with:

* [Quick Start](readme-1/quick-start.md)
* [MCP-Assisted Development](readme-1/integration-tools/mcp-assisted-development.md)
* [Booking Overview](product-guides/booking/booking-overview/)

#### Sandbox validation

Start with:

* [Sandbox Access](readme-1/making-requests.md)
* [Sandbox Validation Test Kit](readme-1/sandbox-development/sandbox-validation-test-kit.md)
* [Sandbox Development](readme-1/sandbox-development/)

#### Booking and payment flow

Start with:

* [Booking Overview](product-guides/booking/booking-overview/)
* [Payment & Ticketing](product-guides/booking/booking-step-guides/payment-and-ticketing/)
* [Hybrid Payment Guide](product-guides/booking/booking-step-guides/payment-and-ticketing/hybrid-payment-guide.md)

#### Troubleshooting and support

Start with:

* [Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/)
* [FAQs](support-and-reference/troubleshooting-and-support/faqs/)
* [Webhook Overview](product-guides/extensions-and-integrations/webhook-overview/)

### FAQ

#### What changed in the Atlas API docs recently?

Recent updates added [Identifiers](product-guides/booking/booking-overview/identifiers.md), [Search vs Get Offer](product-guides/booking/booking-overview/booking-decisions/search-vs-offer.md), [429 vs 110](support-and-reference/troubleshooting-and-support/errors-handing/429-vs-110.md), [202 vs 301 vs 308](support-and-reference/troubleshooting-and-support/errors-handing/202-vs-301-vs-308.md), [Verify vs Create Order](product-guides/booking/booking-overview/booking-decisions/verify-vs-order.md), [Polling and Ticketing Timing](product-guides/booking/booking-step-guides/query-order/post-payment-polling.md), [402 vs 404 vs 406 vs 615](support-and-reference/troubleshooting-and-support/errors-handing/402-vs-404-vs-406-vs-615.md), [Baggage and seat productCode freshness](product-guides/booking/optional-ancillaries/baggage-and-seat-productcode-freshness.md), [Restart from Search vs Verify vs Get Offer](product-guides/booking/booking-overview/booking-decisions/restart-point.md), [307 vs 327 vs 410](support-and-reference/troubleshooting-and-support/errors-handing/307-vs-327-vs-410.md), [309 vs 409](support-and-reference/troubleshooting-and-support/errors-handing/309-vs-409.md), [Seat fallback modes](product-guides/booking/optional-ancillaries/seats-and-baggage/seat-fallback-modes.md), [401 vs 402 vs 404](support-and-reference/troubleshooting-and-support/errors-handing/401-vs-402-vs-404.md), [205 vs 299 vs 304](support-and-reference/troubleshooting-and-support/errors-handing/205-vs-299-vs-304.md), and [318 vs 608 duplicate booking](support-and-reference/troubleshooting-and-support/errors-handing/318-vs-608-duplicate-booking.md), added QPS and QPM request-limit guidance for selected pre-booking APIs, added [Multi-channel Notifications](product-guides/extensions-and-integrations/multi-channel-notifications.md) for ATRIP notification setup, added the new ATRIP **UAT Testing** flow to [UAT Validation](readme-1/uat-submission-guide.md), clarified that **flight booking** is required, added automatic verification guidance, expanded the [Void workflow](product-guides/post-booking/void.md), changed `seatAvailability.do` call rules, added [MCP-Assisted Development](readme-1/integration-tools/mcp-assisted-development.md), published [Sandbox Validation Test Kit](readme-1/sandbox-development/sandbox-validation-test-kit.md), and improved [Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/) as a troubleshooting entry point.

#### Which guide should I read first for sandbox integration?

Start with [Quick Start](readme-1/quick-start.md). Then use [Sandbox Validation Test Kit](readme-1/sandbox-development/sandbox-validation-test-kit.md) to confirm readiness before coding.

#### Where should I start for booking, payment, or troubleshooting?

Use [Booking Overview](product-guides/booking/booking-overview/) for the main flow, [Payment & Ticketing](product-guides/booking/booking-step-guides/payment-and-ticketing/) for payment and polling, and [Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/) for failure handling.

### Full change log

{% updates format="full" %}
{% update date="2026-07-08" %}
## Expanded VOID airline coverage

Updated the VOID documentation to reflect the current supported airline scope.

What changed:

* documented 23 supported VOID airlines across four regions
* added `TS`, `Y4`, `EI`, and `VF` to the supported coverage list
* clarified that `ZG` support is limited to US routes

Updated pages:

* [Void workflow](product-guides/post-booking/void.md)
* [Void](api-reference/post-booking-apis/void.md)
* [Atlas API Documentation Updates](./)
{% endupdate %}

{% update date="2026-07-06" %}
## Added Fulfillment API and `getOfferPrice.do`

Published the new fulfillment booking path for `getOfferPrice.do` and updated key workflow pages with fulfillment-specific timing and request-limit guidance.

What changed:

* added [Fulfillment API](product-guides/booking/booking-step-guides/get-offer-price.md) for fulfillment positioning, 5-minute timing, retry rules, and recovery guidance
* added [Get Offer vs Fulfillment API](product-guides/booking/booking-overview/booking-decisions/get-offer-vs-get-offer-price.md) to distinguish standard Get Offer from the fulfillment path
* added [Get Offer Price](api-reference/booking-apis/get-offer-price.md) under API Reference
* updated [Booking Overview](product-guides/booking/booking-overview/) to add the new fulfillment branch
* updated [Get Offer](product-guides/booking/booking-step-guides/get-offer.md) to distinguish `getOffers.do` from `getOfferPrice.do`
* updated [Create Order](product-guides/booking/booking-step-guides/create-order.md), [Payment & Ticketing](product-guides/booking/booking-step-guides/payment-and-ticketing/), and [Query Order](product-guides/booking/booking-step-guides/query-order/) for 5-minute fulfillment handling
* updated [Orders & Ticketing](support-and-reference/troubleshooting-and-support/faqs/atlas-api-order.md) to separate standard 30-minute hold from the fulfillment flow
* updated [API Request Limits](product-guides/booking/booking-overview/api-request-limits.md) to document the separate `getOfferPrice.do` QPM policy
{% endupdate %}

{% update date="2026-07-05" %}
## Added identifier, flow-choice, and throttling guidance

Published fifteen new support pages for common booking-flow integration questions.

What changed:

* added [Identifiers](product-guides/booking/booking-overview/identifiers.md) for `routingIdentifier`, `sessionId`, `OfferId`, `orderNo`, and refresh rules
* added [Search vs Get Offer](product-guides/booking/booking-overview/booking-decisions/search-vs-offer.md) to clarify when to use `search.do` and when to use `getOffers.do`
* added [429 vs 110](support-and-reference/troubleshooting-and-support/errors-handing/429-vs-110.md) to explain request-limit governance versus search concurrency pressure
* added [202 vs 301 vs 308](support-and-reference/troubleshooting-and-support/errors-handing/202-vs-301-vs-308.md) to explain which earlier step must be refreshed
* added [Verify vs Create Order](product-guides/booking/booking-overview/booking-decisions/verify-vs-order.md) to clarify the validation boundary before order creation
* added [Polling and Ticketing Timing](product-guides/booking/booking-step-guides/query-order/post-payment-polling.md) to explain post-payment follow-up and safe polling behavior
* added [402 vs 404 vs 406 vs 615](support-and-reference/troubleshooting-and-support/errors-handing/402-vs-404-vs-406-vs-615.md) to clarify payment-state recovery and duplicate-payment risk
* added [Baggage and seat productCode freshness](product-guides/booking/optional-ancillaries/baggage-and-seat-productcode-freshness.md) to explain when ancillary selections are stale
* added [Restart from Search vs Verify vs Get Offer](product-guides/booking/booking-overview/booking-decisions/restart-point.md) to explain which booking step must be rerun after stale context or price drift
* added [307 vs 327 vs 410](support-and-reference/troubleshooting-and-support/errors-handing/307-vs-327-vs-410.md) to clarify passenger, document, and contact input errors at order creation
* added [309 vs 409](support-and-reference/troubleshooting-and-support/errors-handing/309-vs-409.md) to clarify stale ancillary codes versus baggage segment-mapping errors
* added [Seat fallback modes](product-guides/booking/optional-ancillaries/seats-and-baggage/seat-fallback-modes.md) to explain `STOP_TICKET`, `STOP_SEAT`, and `SIMILAR_SEAT`
* added [401 vs 402 vs 404](support-and-reference/troubleshooting-and-support/errors-handing/401-vs-402-vs-404.md) to clarify payment deadline expiration versus non-payable or already-paid orders
* added [205 vs 299 vs 304](support-and-reference/troubleshooting-and-support/errors-handing/205-vs-299-vs-304.md) to clarify transient verify and order failures
* added [318 vs 608 duplicate booking](support-and-reference/troubleshooting-and-support/errors-handing/318-vs-608-duplicate-booking.md) to clarify duplicate-booking handling before another retry

Updated pages:

* [Atlas API Documentation Updates](./)
* [Booking Overview](product-guides/booking/booking-overview/)
* [Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/)
* [Payment & Ticketing](product-guides/booking/booking-step-guides/payment-and-ticketing/)
{% endupdate %}

{% update date="2026-07-03" %}
## Added QPS and QPM request-limit guidance

Updated booking, troubleshooting, and FAQ pages to document request-limit governance for selected pre-booking APIs.

What changed:

* added Atlas error code `429` guidance with `retryAfter`
* documented default limits for Search, Fulfillment, and Ancillary resource pools
* clarified that `verify.do` and `getOffers.do` share one fulfillment pool
* clarified that `seatAvailability.do` and `getLuggage.do` share one ancillary pool
* confirmed that `order.do` and `pay.do` are not part of this request-limit policy

Updated pages:

* [Booking Overview](product-guides/booking/booking-overview/)
* [Search](product-guides/booking/booking-step-guides/search.md)
* [Get Offer](product-guides/booking/booking-step-guides/get-offer.md)
* [Verify](product-guides/booking/booking-step-guides/verify.md)
* [Seats](product-guides/booking/optional-ancillaries/seats-and-baggage/)
* [Baggage](product-guides/booking/optional-ancillaries/baggage.md)
* [Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/)
* [Search Errors](support-and-reference/troubleshooting-and-support/errors-handing/search-errors.md)
* [Verify, Order & Ticketing Errors](support-and-reference/troubleshooting-and-support/errors-handing/verify-order-and-ticketing-errors.md)
* [Search & Booking](support-and-reference/troubleshooting-and-support/faqs/atlas-api-search-and-book.md)
{% endupdate %}

{% update date="2026-06-30" %}
## Added multi-channel notification setup guidance

Published [Multi-channel Notifications](product-guides/extensions-and-integrations/multi-channel-notifications.md) for ATRIP delivery across webhook, email, DingTalk, WeCom, Slack, and Teams.

What changed:

* added a new guide for channel selection, ATRIP setup, and test notifications
* clarified in [Webhook Overview](product-guides/extensions-and-integrations/webhook-overview/) that webhook is one delivery option in the broader notification model
* updated [Airline Status Update Notification](product-guides/extensions-and-integrations/webhook-overview/airline-status-update-notification.md) to position airline status as the first live multi-channel scenario

Updated pages:

* [Multi-channel Notifications](product-guides/extensions-and-integrations/multi-channel-notifications.md)
* [Webhook Overview](product-guides/extensions-and-integrations/webhook-overview/)
* [Airline Status Update Notification](product-guides/extensions-and-integrations/webhook-overview/airline-status-update-notification.md)
{% endupdate %}

{% update date="2026-06-29" %}
## Removed `Accept: application/json` from standard headers

Updated the sandbox access guidance to keep the standard request headers aligned with current usage.

What changed:

* removed `Accept: application/json` from the standard headers list
* kept the remaining standard header guidance unchanged

Updated pages:

* [Sandbox Access](readme-1/making-requests.md)
{% endupdate %}

{% update date="2026-06-29" %}
## Updated UAT Validation for ATRIP UAT Testing

Updated the UAT guidance to reflect the latest ATRIP flow.

What changed:

* UAT now starts from **UAT Testing**
* partners choose the target function scope before continuing
* **flight booking** is now documented as the required core function
* **Confirm and Continue** and **Submit Verification** are now part of the documented flow
* failed cases now point users to the ATRIP failure reason directly

Updated pages:

* [UAT Validation](readme-1/uat-submission-guide.md)
* [Quick Start](readme-1/quick-start.md)
* [Getting Started](support-and-reference/troubleshooting-and-support/faqs/atlas-api-general-information.md)
{% endupdate %}

{% update date="2026-06-10" %}
## Expanded Void workflow and webhook guidance

Updated the void documentation to reflect the current post-booking flow.

What changed:

* clarified the standard `voidQuotation.do` → `void.do` → `queryVoidOrders.do` sequence
* added guidance for `voidOfferId`, `voidCode`, and strict void-window handling
* expanded `order.void` webhook trigger rules, status values, and retry-failure behavior

Updated pages:

* [Void workflow](product-guides/post-booking/void.md)
* [Void](api-reference/post-booking-apis/void.md)
* [Void Notification](product-guides/extensions-and-integrations/webhook-overview/void-notification.md)
{% endupdate %}

{% update date="2026-06-09" %}
## Updated SeatAvailability call rules

Updated seat-selection documentation to reflect the latest `seatAvailability.do` requirements.

What changed:

* independent mode is no longer available
* use `sessionId` from `verify.do` or `OfferId` from `getOffers.do`
* flight-only seat quote requests are not supported

Updated pages:

* [Inflow Seat & Baggage](api-reference/booking-apis/inflow-seat-and-baggage.md)
* [Seats & Baggage](product-guides/booking/optional-ancillaries/seats-and-baggage/)
* [Verify](product-guides/booking/booking-step-guides/verify.md)
* [Get Offer](product-guides/booking/booking-step-guides/get-offer.md)
* [Booking Overview](product-guides/booking/booking-overview/)
* [Search & Booking](support-and-reference/troubleshooting-and-support/faqs/atlas-api-search-and-book.md)
{% endupdate %}

{% update date="2026-04-15" %}
## Added MCP-Assisted Development

Published [MCP-Assisted Development](readme-1/integration-tools/mcp-assisted-development.md) for teams using GitBook MCP during Atlas API integration.

Use it when you need to:

* find the correct workflow before coding
* understand which identifier or API comes next
* jump from development questions to the right reference or troubleshooting page

The guide also includes prompt patterns and usage boundaries for production-safe development.
{% endupdate %}

{% update date="2026-04-09" %}
## Added Sandbox Validation Test Kit

Published [Sandbox Validation Test Kit](readme-1/sandbox-development/sandbox-validation-test-kit.md) for a no-code sandbox validation run.

Use it when you need to:

* confirm credentials and network access before development
* run the core sandbox happy path with Newman
* verify `Search`, `Verify`, `Order`, and `Pay` in one pass
* quickly check sandbox readiness after environment changes

The page also explains the expected final retrieve timeout during ticketing polling.
{% endupdate %}

{% update date="2026-04-08" %}
## Improved Error Codes landing page

Updated [Error Codes](support-and-reference/troubleshooting-and-support/errors-handing/) with:

* retry policy guidance
* a quick decision table for high-frequency codes
* high-risk mistakes to avoid during retry
* pattern-based checks for common integration issues

This makes the page more useful as the main troubleshooting entry point.
{% endupdate %}

{% update date="2026-04-03" %}
## Added Hybrid Payment Guide

Published [Hybrid Payment Guide](product-guides/booking/booking-step-guides/payment-and-ticketing/hybrid-payment-guide.md) under **Payment & Ticketing**.

Use it when you need to:

* switch from VCC pass-through to deposit
* decide whether to reuse or regenerate an order
* handle hybrid payment fallback in ATRIP and API flows
{% endupdate %}
{% endupdates %}
