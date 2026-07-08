---
description: Build and validate the sandbox integration before UAT.
---

# Sandbox Development

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this page to build and validate the full Atlas integration in sandbox.

{% include "../../.gitbook/includes/sandbox-search-currency-note.md" %}

{% hint style="info" %}
Before you build the integration, run the [Sandbox Validation Test Kit](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/QGSV22o2k6o3CpQ1SZLf).

Use it to confirm credentials, network access, and the core happy path without writing code.
{% endhint %}

Start here when you need to:

* build the full sandbox booking flow
* validate webhook handling and follow-up logic
* confirm the integration is ready for UAT

### FAQ

#### What should be working before sandbox development starts?

Sandbox credentials should work first.

Headers, request format, and gzip handling should also be ready.

#### What proves sandbox development is complete?

The full booking flow should run end to end in a stable way.

Your team should also be able to reproduce expected success and failure paths.

### Goal of this phase

Build the end-to-end integration flow in sandbox.

This phase should cover both API execution and webhook follow-up.

### Fast setup check

Use the [Sandbox Validation Test Kit](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/QGSV22o2k6o3CpQ1SZLf) before full development work.

It validates `Search`, `Verify`, `Order`, and `Pay`.

If the final retrieve step times out, treat that as expected during ticketing polling.

### What sandbox can validate

Use sandbox to validate:

* request format and headers
* search, verify, order, payment, and query flow
* webhook handling and follow-up logic
* failure handling and edge cases
* UAT readiness

### What sandbox does not prove

Sandbox does **not** prove:

* live inventory quality
* production pricing accuracy
* real card charging behavior
* final airline-side behavior in all cases

Treat sandbox fares and outcomes as test-only.

### Before you start

Make sure you already have:

* sandbox credentials from ATRIP
* the sandbox base URL: `https://sandbox.atriptech.com/`
* request headers configured
* a basic server-side integration ready to test

### Use MCP during development

Use [MCP-Assisted Development](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/uEdQG85jAqXi5Zbbzq17) when you need help finding the right flow, page, or next API step.

It works well for:

* mapping `Search` to `Pay`
* checking which identifier to keep and reuse
* routing errors to the right troubleshooting page

### Development checklist

Complete these items in sandbox:

* configure authentication and headers
* point your client to sandbox
* implement search, verify, order, payment, and query
* register and validate webhooks
* test failure handling and edge cases

During this phase, keep and reuse:

* `routingIdentifier`
* `sessionId`
* `orderNo`

### Recommended build order

{% stepper %}
{% step %}
### Confirm sandbox setup

Make sure credentials, headers, gzip handling, and the sandbox base URL are working.
{% endstep %}

{% step %}
### Build the booking flow

Implement search, verify, order creation, payment, and order query.
{% endstep %}

{% step %}
### Add webhook handling

Register the webhook endpoint and validate event delivery and processing.
{% endstep %}

{% step %}
### Test expected failures

Simulate payment and flow failures and confirm error handling works as expected.
{% endstep %}

{% step %}
### Prepare for UAT

Keep traceable test orders and confirm the full sandbox flow is stable and repeatable.
{% endstep %}
{% endstepper %}

### Test mode

In test mode:

* bookings are simulated
* tickets are not issued with live airlines
* fares are sandbox fares
* test credentials only work in sandbox
* live credentials only work in production

Use test mode to validate:

* request construction
* booking state transitions
* payment and ticketing logic
* expected error handling
* webhook and follow-up behavior

### Sandbox fare behavior

Sandbox search results come from Atlas sandbox data.

Coverage and pricing are not the same as production.

Do not use sandbox prices for commercial comparison.

### Payment failure simulation

You can trigger common VCC error paths in `pay.do`.

#### Trigger payment decline

Use:

* Cardholder first name: `Reject`

Expected result:

* `604` — Payment declined by airline

#### Trigger 3DS error

Use:

* Cardholder first name: `Three DS`

Expected result:

* `616` — 3DS Authentication

Any card number and last name can be used for this specific failure simulation.

### Reference data for sandbox

Use these shared reference pages when you need published sandbox inputs:

* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [Webhook Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/1kDgZtL5TYuOLUmAxRd6)
* [Sandbox Test Routes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/tyXBAEpAntbScXsBHd0l)
* [Sandbox Test Cards](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/VXnL5n838qAJ6myXvikA)
* [Integration Reference](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/JKGPURw0UiwgbJIUMwZq)

### Complete this phase when

You can do all of these reliably in sandbox:

* run the booking flow end to end
* keep and reuse `routingIdentifier`, `sessionId`, and `orderNo`
* validate the required payment path
* receive and process the required webhook events
* reproduce expected success and failure cases

### Output of this phase

* stable sandbox booking flow
* validated webhook handling
* evidence ready for UAT

### Next step

Move to [UAT Validation](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/aH2Shbpf2B9zZldFkBrT) after the sandbox flow is stable.

### Related pages

* [Quick Start](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/MkEt9qjU24ig50fQ8be2)
* [Sandbox Access](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/O9n7Z0tHowy0I3hOF44f)
* [Sandbox Validation Test Kit](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/QGSV22o2k6o3CpQ1SZLf)
* [UAT Validation](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/aH2Shbpf2B9zZldFkBrT)
* [Webhook Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/1kDgZtL5TYuOLUmAxRd6)
