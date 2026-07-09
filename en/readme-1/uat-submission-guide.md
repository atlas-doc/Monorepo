---
description: >-
  Atlas API UAT validation guide for execution scope, evidence, verification,
  and approval before go-live.
---

# UAT Validation

{% include "../.gitbook/includes/eva-help-hint.md" %}

Use this page when your sandbox integration is ready for go-live validation.

Start here when you need to:

* choose the correct UAT track
* complete UAT in ATRIP
* understand what must pass before go-live

### FAQ

#### When should we start UAT?

Start UAT only after the sandbox flow is stable end to end.

Your team should be able to run the required test scenarios reliably before starting verification in ATRIP.

#### What does a UAT pass prove?

It proves the validated sandbox integration is ready for production transition.

It does not replace the production credential switch or go-live monitoring steps.

### Goal of this phase

Validate that the sandbox integration is ready for production.

This phase converts a completed sandbox integration into an approved go-live result.

### Do not start UAT yet if

Wait before starting UAT when any of these are still unstable:

* the sandbox booking flow still fails intermittently
* the required identifiers are not tracked reliably
* webhook handling is incomplete for the selected scope
* your team cannot reproduce the same result with fresh test orders

### When to start UAT

Start UAT after:

* sandbox credentials are working
* the core booking flow is integrated
* request headers and authentication are stable
* webhook handling is ready if full integration UAT is required
* your team can execute test cases end to end

### UAT flow in ATRIP

Complete UAT in ATRIP under **UAT Testing**.

Use this path:

1. Sign in to ATRIP.
2. Open **UAT Testing**.
3. Choose the function scope you need to complete.
4. Complete **flight booking** at minimum.
5. Click **Confirm and Continue**.
6. Fill the order details required by each test case.
7. Click **Submit Verification**.
8. Review the automatic verification result.

If a case fails, ATRIP shows the failure reason directly.

{% hint style="info" %}
Before UAT, run the [Sandbox Validation Test Kit](sandbox-development/sandbox-validation-test-kit.md).

Use it to confirm credentials, network access, and the basic booking path before formal validation starts.
{% endhint %}

### UAT tracks

There are two UAT tracks.

#### 1. Shopping and Ticketing UAT

Use this track when you need to validate the standard search-to-ticket flow.

This usually covers:

* search
* verify
* order
* payment
* ticketing result

#### 2. Full Integration UAT

Use this track when you need to validate the end-to-end integration between Atlas and your booking platform.

This usually covers:

* passenger type combinations
* trip type combinations
* direct and connecting itineraries
* payment methods
* ancillaries
* webhooks
* operational follow-up flows

### How do you choose the right UAT track?

Use **Shopping and Ticketing UAT** for the standard search-to-ticket path.

Use **Full Integration UAT** when you need broader coverage across passenger combinations, trip types, ancillaries, webhook handling, and operational follow-up.

### Required function coverage

Choose the functions that match your integration scope.

`flight booking` is the core function.

You must complete it in every UAT run.

If your rollout also includes more functions, complete those in the same UAT scope.

### What to prepare before verification

Prepare these items before starting UAT in ATRIP:

* valid order details for each test case
* relevant order numbers or request IDs
* webhook evidence when full integration is tested
* the Postman collection used by your team, if needed

### UAT preparation checklist

Make sure these items are ready before you submit verification:

* a confirmed UAT scope
* fresh test orders for each required case
* traceable `orderNo` values and request context
* screenshots or exported evidence for failed or retried cases
* webhook payload samples when the scope requires webhook coverage

### Best practice

Prepare the order information before you enter **UAT Testing**.

Use fresh and traceable test orders for every required case.

Keep order numbers, request IDs, screenshots, and webhook samples linked to the same test case.

### Recommended execution order

{% stepper %}
{% step %}
### Sign in and open UAT Testing

Go to ATRIP and open **UAT Testing**.
{% endstep %}

{% step %}
### Choose the required function scope

Select the integration functions you need to complete.

Always include **flight booking**.
{% endstep %}

{% step %}
### Confirm the selected scope

Click **Confirm and Continue**.
{% endstep %}

{% step %}
### Fill the case order details

Enter the required order information for each test case.
{% endstep %}

{% step %}
### Submit verification

Click **Submit Verification** to start the system check.
{% endstep %}

{% step %}
### Review the result

Check whether each case passes.

If a case fails, review the error reason, fix the issue, and run the verification again.
{% endstep %}
{% endstepper %}

### Verification result

After you click **Submit Verification**, ATRIP validates the case automatically.

When a case fails, ATRIP returns the error reason directly.

Use that reason to correct the order data, rerun the test flow, or replace the test order before you submit again.

### Common reasons a verification fails

* `flight booking` is not completed
* the wrong function scope is selected
* the order details do not match the test case
* the order status does not satisfy the case requirement
* required webhook coverage is missing for full integration UAT

### If verification fails

Use this recovery order:

1. Confirm the selected UAT scope matches the tested workflow.
2. Check that the submitted order details match the exact case.
3. Re-run the failed flow with a fresh test order if the status is unclear.
4. Confirm webhook evidence exists when the selected scope requires it.
5. Submit verification again only after the failed condition is corrected.

### What comes next?

After approval, continue with [Production Go-Live](production-go-live.md).

At that point, ask for `LIVE` status, generate production credentials, switch endpoints, and run a controlled smoke test.

### Complete this phase when

You have all of these:

* selected the correct UAT track
* completed the required function scope
* passed the required verification cases
* resolved any reported failure reason

### Output of this phase

* passed UAT result
* confirmed go-live readiness
* approved transition to production setup

### Next step

After UAT passes:

* ask your customer manager to switch the account to `LIVE`
* generate production credentials
* set up the production IP whitelist
* replace sandbox endpoints
* run a controlled smoke test
* monitor the first live orders and webhook events

### Related pages

* [Sandbox Development](sandbox-development/)
* [Sandbox Validation Test Kit](sandbox-development/sandbox-validation-test-kit.md)
* [Quick Start](quick-start.md)
* [Production Go-Live](production-go-live.md)
* [Webhook Overview](../product-guides/extensions-and-integrations/webhook-overview/)
