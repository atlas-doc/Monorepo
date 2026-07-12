---
description: >-
  Common Atlas API onboarding questions about access, sandbox testing, pricing,
  performance, airline coverage, and escalation.
---

# Getting Started

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page for commercial, onboarding, performance, and support basics.

Start here when you need to:

* confirm how to get sandbox access
* understand what Atlas supports before development
* find basic guidance on pricing, performance, and escalation

### FAQ

#### How do we start with Atlas API?

Start by confirming commercial fit, NDA steps, and sandbox access.

Then generate sandbox credentials, run the first tests, and move to UAT only after the end-to-end flow is stable.

#### Which airlines can we sell through Atlas?

Atlas supports more than 150 airlines as of July 2026.

Availability varies by airline, market, account configuration, and booking workflow.

Review the current list on the [airline list](https://www.atriptech.com/#/airline/list) and in ATRIP.

#### Can we test before signing?

Yes.

Submit the [get started form](https://atlaslovestravel.com/get-started/).

Atlas will review your company, complete NDA steps, and then issue test credentials.

#### Where do we get sandbox credentials?

Generate them in ATRIP under `Profile` → `My Profile` → `Company Information`.

Use `x-atlas-client-id` and `x-atlas-client-secret` on every sandbox call.

#### Is there a Postman collection for first tests?

Yes.

Use the Postman collection in [Quick Start](../../../readme-1/quick-start.md).

Use the UAT guidance later when you prepare for formal verification.

#### How do we start UAT?

Start UAT only after the sandbox flow is stable end to end.

Open **UAT Testing** in ATRIP, choose the required function scope, and complete **flight booking** at minimum.

Then click **Confirm and Continue**, fill the case order details, and use **Submit Verification** for automatic validation.

#### Are airline capabilities always the same?

No. Capability depends on what each airline supports.

Atlas exposes supported functions per airline and flow.

#### How is Atlas priced?

Pricing depends on market, currency, account configuration, and commercial terms.

Use the [contact form](https://atlaslovestravel.com/contact/) to get local pricing details.

#### What performance should we expect?

Typical response times vary by API and airline conditions.

Use the timeout and response-time guidance below as operational expectations, not as hard guarantees for every request.

#### Does Atlas support promo fares or promo codes?

General promotional fare support is available.

Promo code support is not generally available as of July 2026.

Availability can vary by airline and account configuration.

#### What is the L2B ratio?

The look-to-book ratio is defined in your commercial agreement.

#### Does Atlas use cache?

Yes. Atlas uses a shared cache pool for search traffic.

Client-specific cache can also be supported.

#### What should we do during API failure?

Use support channels for immediate help.

Fallback portal availability depends on your account and operational setup.

#### Does Atlas provide fare guarantee?

Yes, after payment is completed in **deposit** mode.

Ticketing usually completes within 10 minutes. Rare cases can take up to one hour.

Fare guarantee does **not** apply to VCC pass-through payments.

#### What are the standard timeout limits?

* `search.do`: not fixed
* `realTimeSearch.do`: `120s`
* `verify.do`: `15s`
* `order.do`: `15s` for normal booking, `120s` for real-time booking
* `pay.do`: not fixed

#### What are the typical response times?

* `search.do`: under `500ms` for 98% of responses
* `verify.do`: about `8s` for 95% of responses
* `order.do`: about `14s` for 95% of responses
* `pay.do`: about `2s` for 95% of responses

These are typical operating results, not contractual SLAs.

Results vary by airline, request conditions, and system load.

#### How do we escalate unresolved issues?

Escalate unresolved service issues through **customerfeedback@atlaslovestravel.com**.

Atlas may first ask you to open or reference a Service Request in ATRIP.
