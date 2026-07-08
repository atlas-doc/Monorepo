---
description: >-
  Use this checklist in the first integration call to align flow choice,
  payment, ticketing, post-booking, and launch readiness.
---

# Kickoff Checklist

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page in the first integration call.

Its goal is simple.

Leave the meeting with the main flow, ownership, and launch path agreed.

{% hint style="info" %}
Need a shorter customer pre-read first?

Use [Top Questions for Partners](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/rj5WM4KAQ5YcHyUoIR75).
{% endhint %}

### What this meeting should achieve

By the end of kickoff, both sides should agree on:

* the booking flow to implement
* the price refresh point before booking
* the payment mode by business case
* the ticketing status handling model
* whether seat or baggage must be supported before purchase
* who owns refund and change follow-up
* what is required before UAT and go-live

### Recommended meeting order

{% stepper %}
{% step %}
### Confirm the commercial and product fit

Clarify whether Atlas is the main shopping source or the final booking and pricing layer.
{% endstep %}

{% step %}
### Choose the booking flow

Decide whether the standard search flow or Get Offer flow is the main implementation path.
{% endstep %}

{% step %}
### Confirm payment and ticketing design

Align deposit or VCC usage, polling logic, and final state handling.
{% endstep %}

{% step %}
### Confirm post-booking ownership

Agree how refund, change, schedule change, and urgent cases will be handled.
{% endstep %}

{% step %}
### Confirm launch path

Agree sandbox scope, UAT expectations, and go-live prerequisites.
{% endstep %}
{% endstepper %}

### Section 1: Business and system fit

Ask these first:

* Is Atlas your main shopping source?
* Or do you already have your own shopping engine?
* Do you need Atlas mainly for final bookable price confirmation?
* Do you need one flow for all airlines, or selective routing by carrier?

#### Decision to record

Write down one of these as the main role of Atlas:

* primary shopping and booking layer
* final pricing and booking layer
* selective supplier in a multi-source system

### Section 2: Booking flow

Choose the main path.

#### Standard search path

Use this when Atlas is your main shopping source.

Main chain:

1. `search.do`
2. `verify.do`
3. `order.do`
4. `pay.do`
5. `queryOrderDetails.do`

#### Get Offer path

Use this when the target itinerary is already known.

Main chain:

1. `getOffers.do`
2. `order.do`
3. `pay.do`
4. `queryOrderDetails.do`

#### Questions to settle

* Which path is the default production path?
* When do you refresh price before booking?
* Will your system block stale pricing after long delays?
* Will you support both flows or only one?

See:

* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [Get Offer](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/FSGess6buGE1P02WnVNu)
* [Verify](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Hg2lCO93wE6SPAXEYPOm)

### Section 3: Pricing integrity

This is usually the highest-risk topic.

Align on these rules:

* search result is not the final booking promise
* verify or Get Offer should be used close to booking time
* long delays increase failure and mismatch risk
* latest verified or offered price is the source of truth for order creation

#### Questions to settle

* What is the latest point where price must be refreshed?
* What happens if the user returns after a delay?
* Will markup be applied before or after final refresh?
* Which value is shown to the user when price changes?

### Section 4: Fare content and ancillaries

Set expectations early.

#### Questions to settle

* Do you need fare family display?
* Do you need baggage upsell before booking?
* Do you need seat map before booking?
* Do you need post-ticketing baggage or seat sales?
* Can ancillary lookup stay optional in the first release?

#### Important rule

Do not force ancillary queries into the base flow unless they are required.

See [Seats & Baggage](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/3ujCySdZ8OYYLfGI3iF3).

### Section 5: Payment model

Confirm the primary payment path before build starts.

#### Main options

* **Deposit**
* **VCC pass-through**

#### Questions to settle

* Which payment mode is the default?
* Will payment mode differ by airline?
* Does the client provide VCC cards?
* What happens when VCC is unavailable for a specific order?
* How will refund expectations be shown to operations teams?

#### Important rule

Atlas does not issue VCC cards.

See [Payments](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/I4apn7RVlP6yFkpJazm3).

### Section 6: Ticketing and booking status

Treat ticketing as asynchronous.

#### Questions to settle

* Will the client poll after `pay.do`?
* Which state is treated as final success?
* When will the client surface airline PNR to agents or users?
* How will duplicate payment be prevented?
* What identifiers are stored for follow-up?

#### Minimum identifiers to retain

* `routingIdentifier`
* `sessionId` or `OfferId`
* `orderNo`
* `pnrCode`
* airline PNR when available

See [Query Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n).

### Section 7: Post-booking operations

This part is often under-scoped.

#### Questions to settle

* Who submits refunds?
* Who follows up delayed refunds?
* How are changes requested?
* Who monitors schedule changes?
* What is the process for urgent departure-day cases?

#### Important rules

* refund path depends on payment mode
* change handling is routed through ATRIP service requests
* webhook should not be the only reconciliation source

See:

* [Post-booking](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/uvnvVffeDxSurkQpIoj0)
* [Webhook Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/1kDgZtL5TYuOLUmAxRd6)

### Section 8: Delivery plan

End the kickoff with delivery expectations.

#### Questions to settle

* Which scope is included in sandbox first?
* What is required before UAT starts?
* Which UAT track applies?
* Who prepares evidence?
* What must be ready before production launch?

See:

* [Quick Start](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/MkEt9qjU24ig50fQ8be2)
* [UAT Validation](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/aH2Shbpf2B9zZldFkBrT)
* [Production Go-Live](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/RbSfDpgzWXL0fCAdyLQy)

### Final output of the kickoff

Do not end the meeting with only open discussion.

Leave with a written decision log for:

* chosen booking flow
* pricing refresh rule
* payment mode
* polling rule
* ancillary scope
* post-booking ownership
* UAT owner
* go-live prerequisites

### Related pages

* [Before Integration](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/atRqZqfIII5j9gLe0jRu)
* [Top Questions for Partners](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/rj5WM4KAQ5YcHyUoIR75)
* [FAQs](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/eSEVUFqqFzApLBAckuJD)
* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [Post-booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/dYHx2vNQK9JRsoUPWN7X)
