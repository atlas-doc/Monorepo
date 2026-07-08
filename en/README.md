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

Start with [Quick Start](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/MkEt9qjU24ig50fQ8be2).

Then use [Integration Guides](https://app.gitbook.com/s/6LsKtmbJhZxgxraY5mHB/), [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3), and [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1).

#### Which pages should I check for request-limit guidance?

Start with [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3), [Search](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/9K7uEnLGfEbpjGjni5gD), [Search & Booking](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/XrP8GBROs9JgYdkjYKPj), and [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1).

### Popular starting points

#### New integration

Start with [Quick Start](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/MkEt9qjU24ig50fQ8be2) and [Integration Guides](https://app.gitbook.com/s/6LsKtmbJhZxgxraY5mHB/).

#### Booking flow

Start with [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3) and [Search & Booking](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/XrP8GBROs9JgYdkjYKPj).

Use [Identifiers](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ns5eKoKIPFUTFhjJkPyC) when you need the right token for the next step.

Use [Verify vs Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2hu9DU8aIIGLGqeathgL) when the booking boundary is the main question.

Use [Restart from Search vs Verify vs Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ZxJaikDjWinutACjHNEw) when the main question is where to restart.

Use [Seat fallback modes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/gwnqga4Hd9HkYrjG8NVb) when paid seat failure behavior must be defined before booking.

#### Troubleshooting

Start with [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1) and [FAQs](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/eSEVUFqqFzApLBAckuJD).

Use [429 vs 110](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/hqJgEqYKMP5CMQ8mArxT) when request frequency or search concurrency is the main issue.

Use [202 vs 301 vs 308](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/b6CraSfDmsTKoVEv4EZy) when you need to know which earlier step must be refreshed.

Use [402 vs 404 vs 406 vs 615](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/LSNWTatN3FFeRiN3ukJk) when the main risk is duplicate or unnecessary payment retry.

Use [307 vs 327 vs 410](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/cuGr1qmrKMXj5NCIRO1C) and [309 vs 409](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FQIV30qEvPMqZLZ6jwbF) when order input or ancillary mapping is the main failure area.

Use [401 vs 402 vs 404](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/259Et84h3iNJClFr0uOL) when the main question is whether the order expired or was already paid.

### Latest Atlas API documentation updates

#### VOID airline coverage expansion

Updated the VOID documentation to show the current supported airline scope.

What changed:

* documented 23 supported VOID airlines across the Americas, Europe, Japan, and Korea
* marked `ZG` as supported only for US routes
* added the latest newly supported airlines: `TS`, `Y4`, `EI`, and `VF`

Read next:

* [Void workflow](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/B8hsI0GKlmcexaJt4Npx)
* [Void](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/H8SaqS9SfWWq494hZlz5)
* [Refund, Query & Post-booking Errors](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/XUINxYxfOsv9CDtmb1pl)

#### Fulfillment API and `getOfferPrice.do` launch

Published new fulfillment guidance for the `getOfferPrice.do` flow and updated key booking pages with its timing and request-limit rules.

What changed:

* added [Fulfillment API](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/e7tapaArEz0MBOv62dxZ) for the new fulfillment-oriented booking path
* added [Get Offer vs Fulfillment API](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/hJ5KgpKJEmpzw2hRXmYp) to clarify when to use `getOffers.do` versus `getOfferPrice.do`
* added [Get Offer Price](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/zE0QlLrSj0ynAcagJTD3) under API Reference
* updated [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3), [Payment & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB), [Query Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n), [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE), [Orders & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/lbLT2qkyVzsb5Mak1Kpg), and [API Request Limits](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV)

Read next:

* [Fulfillment API](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/e7tapaArEz0MBOv62dxZ)
* [Payment & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB)
* [API Request Limits](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV)

#### Payment timeout, transient failure, and duplicate-booking clarification pack

Published three new pages for payment deadline recovery, transient booking-stage failures, and duplicate-booking handling.

What changed:

* added [401 vs 402 vs 404](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/259Et84h3iNJClFr0uOL) to distinguish expired payment windows from non-payable or already-paid order states
* added [205 vs 299 vs 304](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/CAbp9hZapWv0wuj4S8io) to clarify when to retry once, restart from search, or escalate transient verify and order failures
* added [318 vs 608 duplicate booking](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/SzdaH3BBGeQYPWIXQ7S1) to clarify how to confirm existing booking state before retrying

Read next:

* [Payment Errors](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/v1plEh7MJqP2ZqtiNvxk)
* [Verify, Order & Ticketing Errors](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/xgMYjsnxo91kS8079G1O)
* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)

#### Input validation and seat fallback clarification pack

Published three new pages for order input troubleshooting, ancillary mapping, and seat failure behavior.

What changed:

* added [307 vs 327 vs 410](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/cuGr1qmrKMXj5NCIRO1C) to distinguish generic order-field issues, booking-requirement mismatches, and contact phone formatting errors
* added [309 vs 409](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FQIV30qEvPMqZLZ6jwbF) to distinguish stale ancillary codes from baggage segment-mapping errors
* added [Seat fallback modes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/gwnqga4Hd9HkYrjG8NVb) to explain `STOP_TICKET`, `STOP_SEAT`, and `SIMILAR_SEAT`

Read next:

* [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE)
* [Seats](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/3ujCySdZ8OYYLfGI3iF3)
* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)

#### Payment-state and ancillary freshness clarification pack

Published three new pages for payment recovery, ancillary reuse safety, and flow restart decisions.

What changed:

* added [402 vs 404 vs 406 vs 615](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/LSNWTatN3FFeRiN3ukJk) to clarify when to query order, wait, or avoid another `pay.do`
* added [Baggage and seat productCode freshness](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Cxdx0FWp0CbRm6vH8YZg) to explain when ancillary selections are stale
* added [Restart from Search vs Verify vs Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ZxJaikDjWinutACjHNEw) to explain the earliest booking step that must be rerun

Read next:

* [Payment & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB)
* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)

#### Booking recovery and timing clarification pack

Published three new pages for booking-stage recovery decisions and post-payment follow-up.

What changed:

* added [202 vs 301 vs 308](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/b6CraSfDmsTKoVEv4EZy) to explain when to refresh search, refresh verify, or rebuild the booking context
* added [Verify vs Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2hu9DU8aIIGLGqeathgL) to clarify the validation boundary before booking creation
* added [Polling and Ticketing Timing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2qOXdnt78bFPEFbkcemP) to explain why payment success does not always mean final ticketing

Read next:

* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [Payment & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB)
* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)

#### Booking flow clarification pack

Published three new pages for common integration questions around flow choice, identifier handling, and request-pressure troubleshooting.

What changed:

* added [Identifiers](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ns5eKoKIPFUTFhjJkPyC) for `routingIdentifier`, `sessionId`, `OfferId`, `orderNo`, and fresh-identifier rules
* added [Search vs Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Pcq0icGceiiiaVBThnzx) to clarify when to use `search.do` versus `getOffers.do`
* added [429 vs 110](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/hqJgEqYKMP5CMQ8mArxT) to distinguish request-limit governance from search concurrency pressure

Read next:

* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [Search & Booking](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/XrP8GBROs9JgYdkjYKPj)
* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)

#### QPS and QPM request limit governance

Published new request-limit guidance for selected pre-booking APIs.

What changed:

* documented Atlas error code `429` behavior for over-limit requests
* added shared-pool rules for `verify.do` and `getOffers.do`, and for `seatAvailability.do` and `getLuggage.do`
* added retry guidance for `retryAfter`, request pacing, and duplicate-search reduction

Read next:

* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)
* [Search & Booking](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/XrP8GBROs9JgYdkjYKPj)

#### Multi-channel notifications launch

Published the new Atlas notification setup guidance for ATRIP delivery across webhook, email, DingTalk, WeCom, Slack, and Teams.

What changed:

* added a new setup guide for multi-channel notifications in ATRIP
* clarified that webhook is one delivery option in the notification model
* linked airline status updates to the first live multi-channel scenario

Read next:

* [Multi-channel Notifications](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/KsOoqFTUcKVpOxUhs5R7)
* [Webhook Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/1kDgZtL5TYuOLUmAxRd6)
* [Airline Status Update Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/pMAI2bv1LdjljhHdIseW)

#### Standard headers cleanup

Updated the sandbox access guidance to remove an unnecessary standard request header.

What changed:

* removed `Accept: application/json` from the standard headers list
* kept `Accept-Encoding`, `Authorization`, and `Content-Type` guidance unchanged

Read next:

* [Sandbox Access](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/O9n7Z0tHowy0I3hOF44f)
* [Quick Start](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/MkEt9qjU24ig50fQ8be2)

#### UAT Testing flow update

Updated the UAT documentation to reflect the current ATRIP validation flow.

What changed:

* UAT now starts in **UAT Testing**
* partners must choose the target function scope before continuing
* **flight booking** is the required core function
* **Submit Verification** now triggers automatic validation and returns failure reasons directly

Read next:

* [UAT Validation](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/aH2Shbpf2B9zZldFkBrT)
* [Quick Start](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/MkEt9qjU24ig50fQ8be2)
* [Getting Started](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/rHs9a1GaRY814fF0fIkT)

#### Void workflow and notification updates

Updated the void documentation to reflect the current post-booking flow and webhook handling.

What changed:

* clarified the standard flow: `voidQuotation.do` → `void.do` → `queryVoidOrders.do`
* added stronger guidance for `voidOfferId`, `voidCode`, and void-window checks
* expanded `order.void` webhook coverage, status values, and retry-failure behavior

Read next:

* [Void workflow](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/B8hsI0GKlmcexaJt4Npx)
* [Void](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/H8SaqS9SfWWq494hZlz5)
* [Void Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/4aywYMVHUfvNZttgiHPn)

#### SeatAvailability call rules update

Updated the seat-selection guidance to reflect the current `seatAvailability.do` calling rules.

What changed:

* independent mode is no longer available
* `seatAvailability.do` now requires `sessionId` from `verify.do` or `OfferId` from `getOffers.do`
* flight-only seat quote requests are not supported

Read next:

* [Inflow Seat & Baggage](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/33ZWa8YpkzEg8kPsZLCo)
* [Seats & Baggage](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/3ujCySdZ8OYYLfGI3iF3)
* [Verify](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm)

#### MCP-Assisted Development

Read [MCP-Assisted Development](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/uEdQG85jAqXi5Zbbzq17) when you want to use GitBook MCP during Atlas API integration.

Best for:

* teams starting a sandbox build
* developers mapping the booking flow
* teams routing implementation questions faster

Read next:

* [Quick Start](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/MkEt9qjU24ig50fQ8be2)
* [API Reference](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/LfT8Y3jMIGXTnxwihZhV)

#### Sandbox Validation Test Kit

Read [Sandbox Validation Test Kit](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/QGSV22o2k6o3CpQ1SZLf) when you need a no-code sandbox validation run before development or after environment changes.

Best for:

* validate sandbox credentials before coding
* confirm network access and core booking flow readiness
* teams rechecking sandbox health after credential or IP changes

Read next:

* [Sandbox Development](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Xs5C4xGnhQl0A2GNjlwv)
* [UAT Validation](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/aH2Shbpf2B9zZldFkBrT)

#### Error Codes improvements

[Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1) now works better as the main troubleshooting entry point.

Best for:

* teams handling high-frequency integration failures
* developers defining safe retry behavior
* operations teams checking likely root causes

Read next:

* [Common & Access Errors](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Rm0Gc9akel1xG9nGdiHw)
* [Verify, Order & Ticketing Errors](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/xgMYjsnxo91kS8079G1O)

### Start here by use case

#### New Atlas API integration

Start with:

* [Quick Start](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/MkEt9qjU24ig50fQ8be2)
* [MCP-Assisted Development](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/uEdQG85jAqXi5Zbbzq17)
* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)

#### Sandbox validation

Start with:

* [Sandbox Access](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/O9n7Z0tHowy0I3hOF44f)
* [Sandbox Validation Test Kit](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/QGSV22o2k6o3CpQ1SZLf)
* [Sandbox Development](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Xs5C4xGnhQl0A2GNjlwv)

#### Booking and payment flow

Start with:

* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [Payment & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB)
* [Hybrid Payment Guide](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/SkmHf0AK1tgebiGujAko)

#### Troubleshooting and support

Start with:

* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)
* [FAQs](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/eSEVUFqqFzApLBAckuJD)
* [Webhook Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/1kDgZtL5TYuOLUmAxRd6)

### FAQ

#### What changed in the Atlas API docs recently?

Recent updates added [Identifiers](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ns5eKoKIPFUTFhjJkPyC), [Search vs Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Pcq0icGceiiiaVBThnzx), [429 vs 110](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/hqJgEqYKMP5CMQ8mArxT), [202 vs 301 vs 308](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/b6CraSfDmsTKoVEv4EZy), [Verify vs Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2hu9DU8aIIGLGqeathgL), [Polling and Ticketing Timing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2qOXdnt78bFPEFbkcemP), [402 vs 404 vs 406 vs 615](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/LSNWTatN3FFeRiN3ukJk), [Baggage and seat productCode freshness](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Cxdx0FWp0CbRm6vH8YZg), [Restart from Search vs Verify vs Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ZxJaikDjWinutACjHNEw), [307 vs 327 vs 410](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/cuGr1qmrKMXj5NCIRO1C), [309 vs 409](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FQIV30qEvPMqZLZ6jwbF), [Seat fallback modes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/gwnqga4Hd9HkYrjG8NVb), [401 vs 402 vs 404](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/259Et84h3iNJClFr0uOL), [205 vs 299 vs 304](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/CAbp9hZapWv0wuj4S8io), and [318 vs 608 duplicate booking](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/SzdaH3BBGeQYPWIXQ7S1), added QPS and QPM request-limit guidance for selected pre-booking APIs, added [Multi-channel Notifications](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/KsOoqFTUcKVpOxUhs5R7) for ATRIP notification setup, added the new ATRIP **UAT Testing** flow to [UAT Validation](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/aH2Shbpf2B9zZldFkBrT), clarified that **flight booking** is required, added automatic verification guidance, expanded the [Void workflow](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/B8hsI0GKlmcexaJt4Npx), changed `seatAvailability.do` call rules, added [MCP-Assisted Development](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/uEdQG85jAqXi5Zbbzq17), published [Sandbox Validation Test Kit](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/QGSV22o2k6o3CpQ1SZLf), and improved [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1) as a troubleshooting entry point.

#### Which guide should I read first for sandbox integration?

Start with [Quick Start](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/MkEt9qjU24ig50fQ8be2). Then use [Sandbox Validation Test Kit](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/QGSV22o2k6o3CpQ1SZLf) to confirm readiness before coding.

#### Where should I start for booking, payment, or troubleshooting?

Use [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3) for the main flow, [Payment & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB) for payment and polling, and [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1) for failure handling.

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

* [Void workflow](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/B8hsI0GKlmcexaJt4Npx)
* [Void](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/H8SaqS9SfWWq494hZlz5)
* [Atlas API Documentation Updates](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/6ojNmuqNsaDSENrllwAh)
{% endupdate %}

{% update date="2026-07-06" %}
## Added Fulfillment API and `getOfferPrice.do`

Published the new fulfillment booking path for `getOfferPrice.do` and updated key workflow pages with fulfillment-specific timing and request-limit guidance.

What changed:

* added [Fulfillment API](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/e7tapaArEz0MBOv62dxZ) for fulfillment positioning, 5-minute timing, retry rules, and recovery guidance
* added [Get Offer vs Fulfillment API](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/hJ5KgpKJEmpzw2hRXmYp) to distinguish standard Get Offer from the fulfillment path
* added [Get Offer Price](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/zE0QlLrSj0ynAcagJTD3) under API Reference
* updated [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3) to add the new fulfillment branch
* updated [Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FSGess6buGE1P02WnVNu) to distinguish `getOffers.do` from `getOfferPrice.do`
* updated [Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/jZTJWTVq1f6NKaUF3DUE), [Payment & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB), and [Query Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n) for 5-minute fulfillment handling
* updated [Orders & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/lbLT2qkyVzsb5Mak1Kpg) to separate standard 30-minute hold from the fulfillment flow
* updated [API Request Limits](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV) to document the separate `getOfferPrice.do` QPM policy
{% endupdate %}

{% update date="2026-07-05" %}
## Added identifier, flow-choice, and throttling guidance

Published fifteen new support pages for common booking-flow integration questions.

What changed:

* added [Identifiers](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ns5eKoKIPFUTFhjJkPyC) for `routingIdentifier`, `sessionId`, `OfferId`, `orderNo`, and refresh rules
* added [Search vs Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Pcq0icGceiiiaVBThnzx) to clarify when to use `search.do` and when to use `getOffers.do`
* added [429 vs 110](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/hqJgEqYKMP5CMQ8mArxT) to explain request-limit governance versus search concurrency pressure
* added [202 vs 301 vs 308](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/b6CraSfDmsTKoVEv4EZy) to explain which earlier step must be refreshed
* added [Verify vs Create Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2hu9DU8aIIGLGqeathgL) to clarify the validation boundary before order creation
* added [Polling and Ticketing Timing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2qOXdnt78bFPEFbkcemP) to explain post-payment follow-up and safe polling behavior
* added [402 vs 404 vs 406 vs 615](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/LSNWTatN3FFeRiN3ukJk) to clarify payment-state recovery and duplicate-payment risk
* added [Baggage and seat productCode freshness](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Cxdx0FWp0CbRm6vH8YZg) to explain when ancillary selections are stale
* added [Restart from Search vs Verify vs Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ZxJaikDjWinutACjHNEw) to explain which booking step must be rerun after stale context or price drift
* added [307 vs 327 vs 410](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/cuGr1qmrKMXj5NCIRO1C) to clarify passenger, document, and contact input errors at order creation
* added [309 vs 409](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FQIV30qEvPMqZLZ6jwbF) to clarify stale ancillary codes versus baggage segment-mapping errors
* added [Seat fallback modes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/gwnqga4Hd9HkYrjG8NVb) to explain `STOP_TICKET`, `STOP_SEAT`, and `SIMILAR_SEAT`
* added [401 vs 402 vs 404](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/259Et84h3iNJClFr0uOL) to clarify payment deadline expiration versus non-payable or already-paid orders
* added [205 vs 299 vs 304](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/CAbp9hZapWv0wuj4S8io) to clarify transient verify and order failures
* added [318 vs 608 duplicate booking](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/SzdaH3BBGeQYPWIXQ7S1) to clarify duplicate-booking handling before another retry

Updated pages:

* [Atlas API Documentation Updates](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/6ojNmuqNsaDSENrllwAh)
* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)
* [Payment & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB)
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

* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [Search](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/9K7uEnLGfEbpjGjni5gD)
* [Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FSGess6buGE1P02WnVNu)
* [Verify](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm)
* [Seats](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/3ujCySdZ8OYYLfGI3iF3)
* [Baggage](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Ftzqh42LAaE6QYzklv67)
* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)
* [Search Errors](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/ZZXG9HGTENPgRVyaaoYs)
* [Verify, Order & Ticketing Errors](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/xgMYjsnxo91kS8079G1O)
* [Search & Booking](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/XrP8GBROs9JgYdkjYKPj)
{% endupdate %}

{% update date="2026-06-30" %}
## Added multi-channel notification setup guidance

Published [Multi-channel Notifications](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/KsOoqFTUcKVpOxUhs5R7) for ATRIP delivery across webhook, email, DingTalk, WeCom, Slack, and Teams.

What changed:

* added a new guide for channel selection, ATRIP setup, and test notifications
* clarified in [Webhook Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/1kDgZtL5TYuOLUmAxRd6) that webhook is one delivery option in the broader notification model
* updated [Airline Status Update Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/pMAI2bv1LdjljhHdIseW) to position airline status as the first live multi-channel scenario

Updated pages:

* [Multi-channel Notifications](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/KsOoqFTUcKVpOxUhs5R7)
* [Webhook Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/1kDgZtL5TYuOLUmAxRd6)
* [Airline Status Update Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/pMAI2bv1LdjljhHdIseW)
{% endupdate %}

{% update date="2026-06-29" %}
## Removed `Accept: application/json` from standard headers

Updated the sandbox access guidance to keep the standard request headers aligned with current usage.

What changed:

* removed `Accept: application/json` from the standard headers list
* kept the remaining standard header guidance unchanged

Updated pages:

* [Sandbox Access](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/O9n7Z0tHowy0I3hOF44f)
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

* [UAT Validation](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/aH2Shbpf2B9zZldFkBrT)
* [Quick Start](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/MkEt9qjU24ig50fQ8be2)
* [Getting Started](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/rHs9a1GaRY814fF0fIkT)
{% endupdate %}

{% update date="2026-06-10" %}
## Expanded Void workflow and webhook guidance

Updated the void documentation to reflect the current post-booking flow.

What changed:

* clarified the standard `voidQuotation.do` → `void.do` → `queryVoidOrders.do` sequence
* added guidance for `voidOfferId`, `voidCode`, and strict void-window handling
* expanded `order.void` webhook trigger rules, status values, and retry-failure behavior

Updated pages:

* [Void workflow](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/B8hsI0GKlmcexaJt4Npx)
* [Void](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/H8SaqS9SfWWq494hZlz5)
* [Void Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/4aywYMVHUfvNZttgiHPn)
{% endupdate %}

{% update date="2026-06-09" %}
## Updated SeatAvailability call rules

Updated seat-selection documentation to reflect the latest `seatAvailability.do` requirements.

What changed:

* independent mode is no longer available
* use `sessionId` from `verify.do` or `OfferId` from `getOffers.do`
* flight-only seat quote requests are not supported

Updated pages:

* [Inflow Seat & Baggage](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/33ZWa8YpkzEg8kPsZLCo)
* [Seats & Baggage](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/3ujCySdZ8OYYLfGI3iF3)
* [Verify](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm)
* [Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FSGess6buGE1P02WnVNu)
* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [Search & Booking](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/XrP8GBROs9JgYdkjYKPj)
{% endupdate %}

{% update date="2026-04-15" %}
## Added MCP-Assisted Development

Published [MCP-Assisted Development](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/uEdQG85jAqXi5Zbbzq17) for teams using GitBook MCP during Atlas API integration.

Use it when you need to:

* find the correct workflow before coding
* understand which identifier or API comes next
* jump from development questions to the right reference or troubleshooting page

The guide also includes prompt patterns and usage boundaries for production-safe development.
{% endupdate %}

{% update date="2026-04-09" %}
## Added Sandbox Validation Test Kit

Published [Sandbox Validation Test Kit](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/QGSV22o2k6o3CpQ1SZLf) for a no-code sandbox validation run.

Use it when you need to:

* confirm credentials and network access before development
* run the core sandbox happy path with Newman
* verify `Search`, `Verify`, `Order`, and `Pay` in one pass
* quickly check sandbox readiness after environment changes

The page also explains the expected final retrieve timeout during ticketing polling.
{% endupdate %}

{% update date="2026-04-08" %}
## Improved Error Codes landing page

Updated [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1) with:

* retry policy guidance
* a quick decision table for high-frequency codes
* high-risk mistakes to avoid during retry
* pattern-based checks for common integration issues

This makes the page more useful as the main troubleshooting entry point.
{% endupdate %}

{% update date="2026-04-03" %}
## Added Hybrid Payment Guide

Published [Hybrid Payment Guide](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/SkmHf0AK1tgebiGujAko) under **Payment & Ticketing**.

Use it when you need to:

* switch from VCC pass-through to deposit
* decide whether to reuse or regenerate an order
* handle hybrid payment fallback in ATRIP and API flows
{% endupdate %}
{% endupdates %}
