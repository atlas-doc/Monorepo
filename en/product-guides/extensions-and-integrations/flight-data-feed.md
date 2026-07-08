---
description: >-
  Scheduled full and incremental fare data delivery for local pricing databases
  and low-latency shopping.
---

# Flight Data Feed

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this page when you need Atlas to deliver fare data into your own storage.

{% hint style="info" %}
Use `Flight Data Feed` when your product needs fast local query, bulk pricing data, or AI-ready fare storage.

Use `Transaction API` when your product needs real-time verify, booking, payment, and ticketing.
{% endhint %}

Start here when you need to:

* build local flight storage for fast search and ranking
* choose between Data Feed, Transaction API, or both
* understand when bulk fare delivery fits better than real-time booking APIs

### FAQ

#### Does Flight Data Feed replace Transaction API?

No.

Use Data Feed for local display, comparison, and analytics.

Use Transaction API for real-time verify, order creation, payment, and ticketing.

#### When should we use Flight Data Feed?

Use it when your product needs low-latency local query, bulk fare storage, or large-scale fare retrieval for AI, metasearch, or packaging workflows.

### At a glance

* delivery model: full push + incremental push
* shortest incremental interval: `2 minutes`
* throughput: up to `5,000,000` flights per hour
* typical full push: about `500k` flights in `7 minutes`
* transport: `SFTP`
* file formats: `CSV`, `JSON`, `XML`

### What it is

`Atlas Flight Data Feed` is the data delivery layer of Atlas Flight Infrastructure.

It pushes full datasets and incremental updates to your server.

Use it to build a local flight knowledge base.

This is not a booking API.

It complements the real-time booking flow.

### Where it fits in Atlas

* `Layer 1` — Data Feed for local data storage and fast retrieval
* `Layer 2` — Transaction API for real-time verify, order, and payment
* `Layer 3` — Agentic Fulfillment for automated post-booking operations

### Choose the right product path

{% tabs %}
{% tab title="Use Data Feed" %}
Choose this path when you need:

* local fare storage
* low-latency search and comparison
* bulk analytics or packaging logic
* AI retrieval over structured fare data
{% endtab %}

{% tab title="Use Transaction API" %}
Choose this path when you need:

* real-time price confirmation
* live order creation
* payment and ticket issuance
* booking-state follow-up
{% endtab %}

{% tab title="Use both together" %}
Choose this path when you want:

* local display from your own database
* lower search-time API pressure
* real-time verify before checkout
* fast shopping with live booking completion
{% endtab %}
{% endtabs %}

### Core capabilities

#### Full and incremental delivery

Atlas supports two delivery modes:

* full push for first setup or backfill
* incremental push for changed prices and availability
* update intervals as short as `2 minutes`

Use full push for completeness.

Use incremental push for freshness.

{% hint style="success" %}
This model gives you both coverage and freshness.

Full delivery protects completeness.

Incremental delivery keeps local prices current.
{% endhint %}

#### Scale

Current delivery capacity supports:

* up to `5,000,000` flights per hour
* about `14.4 GB` transferred per day
* `10+` customer feeds in parallel

A typical full push for `500k` flights takes about `7 minutes`.

#### Format and mapping

Atlas can deliver:

* `CSV`, `JSON`, or `XML`
* custom field names and field order
* `GZ` or `ZIP` compression

#### Secure transport

Atlas uses `SFTP` for encrypted file delivery.

Transfer success is above `99.9%`.

Atlas can validate files after transfer completes.

#### Configurable scope

You can configure:

* airline coverage
* route or region scope
* full and incremental frequency
* format, compression, and file naming

### What you receive

The exact payload depends on your configuration.

Typical fields include:

* airline, flight number, airports, and travel dates
* base fare, tax, fee, total price, and currency
* cabin, fare family, and seats left
* adult, child, and infant pricing when configured
* baggage allowance and rule summary when configured
* generation time, validity, and freshness markers

<details>

<summary>Why this matters for product and engineering</summary>

Use flight basics for search and display.

Use price and cabin fields for sorting, filtering, and packaging.

Use freshness markers to control cache logic and data trust.

</details>

### Typical delivery flow

{% stepper %}
{% step %}
### Generate the dataset

Atlas builds a full dataset or an incremental delta.
{% endstep %}

{% step %}
### Transform the file

Atlas applies the target format, field mapping, and compression.
{% endstep %}

{% step %}
### Deliver over SFTP

Atlas pushes the file to your server through an encrypted channel.
{% endstep %}

{% step %}
### Load into your database

Your system parses the file and updates local storage.
{% endstep %}
{% endstepper %}

### Typical use cases

{% tabs %}
{% tab title="AI travel agent" %}
Use the feed as a local flight knowledge base.

This supports fast retrieval and complex reasoning without high-frequency live calls.
{% endtab %}

{% tab title="Metasearch" %}
Use the feed for broad coverage and fast result rendering.

Incremental delivery keeps cache freshness high while limiting runtime query cost.
{% endtab %}

{% tab title="Dynamic packaging" %}
Use the feed for large-scale local combination pricing.

This works well when flight and hotel combinations must be precomputed.
{% endtab %}
{% endtabs %}

### When to use Data Feed

Use Data Feed when you need:

* fast local search and comparison
* large-scale local pricing, packaging, and analytics
* AI retrieval over structured fare data

### Data Feed and Transaction API

Use `Data Feed` for display, comparison, and local computation.

Use `Transaction API` for verify, order, payment, and ticketing.

Use both when you want fast search and real-time booking.

{% tabs %}
{% tab title="Display stage" %}
Use `Data Feed`.

Read from your local database.

This gives you low latency and lower API dependency.
{% endtab %}

{% tab title="Checkout stage" %}
Use `Transaction API`.

Verify the latest fare and inventory before order creation.
{% endtab %}

{% tab title="Best-practice chain" %}
Recommended sequence:

1. search from local feed data
2. let the user choose an itinerary
3. verify in real time
4. create the order
5. pay and ticket
{% endtab %}
{% endtabs %}

### Best fit

This product fits:

* AI travel agents and metasearch products
* dynamic packaging and data analysis teams
* OTAs that want fast display with Atlas booking

### What comes next?

If you need live booking after local search, continue with [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3).

If you are still evaluating onboarding and product fit, use [Getting Started](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/rHs9a1GaRY814fF0fIkT).

### Integration options

#### Standard setup

Use this path when the standard format is enough.

Typical setup takes `1–3 days`.

You provide SFTP access.

Atlas configures the feed.

#### Custom setup

Use this path when you need custom mapping or rules.

Typical setup takes about `2 weeks`.

Atlas aligns fields, tests the output, and then switches to production.

### Service expectations

Atlas monitors data quality and transfer health `7x24`.

Data accuracy is above `99.9%`.

Fault recovery target is under `30 minutes`.

### FAQ

#### Does this replace Transaction API?

No.

Use Data Feed for local data access.

Use Transaction API for booking completion.

#### How fresh is the data?

Incremental delivery can run every `2 minutes`.

End-to-end delay stays within minutes.

#### What happens if delivery fails?

Atlas retries transient failures automatically.

Persistent failures trigger alerts and support follow-up.

### Why teams choose this model

* faster search from local reads
* lower display-stage API cost
* better support for bulk comparison and ranking
* stronger fit for AI and analytics workloads
* cleaner separation between display and booking

{% hint style="warning" %}
Data Feed is not the final booking source of truth.

Always use real-time transaction calls before order creation and payment.
{% endhint %}

### Related pages

* [Booking Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/82DaHlpWfsy0ANSplNI3)
* [Quick Start](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/MkEt9qjU24ig50fQ8be2)
* [Getting Started](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/rHs9a1GaRY814fF0fIkT)
