---
description: >-
  Run a no-code happy path check to confirm sandbox credentials, network access,
  and core booking flow readiness.
---

# Sandbox Validation Test Kit

Use this page to validate your sandbox setup before development starts.

This check does not require any custom code.

It confirms that your credentials and network can complete the core booking flow.

Start here when you need to:

* validate sandbox access before writing integration code
* confirm credentials and network reachability quickly
* rerun a fast health check after environment changes

### FAQ

#### When should we run the test kit?

Run it as soon as sandbox credentials are available.

Run it again after any network, IP, or environment change.

#### What does a passing result prove?

It proves the sandbox happy path can run with your current setup.

It does not prove full production readiness or complete edge-case coverage.

### Goal of this check

Use this test kit as a pre-development go or no-go check.

It helps you catch access and environment issues before implementation starts.

### What this validates

The test kit runs the standard happy path in sandbox.

| Step     | What is checked                                     |
| -------- | --------------------------------------------------- |
| `Search` | Your credentials are valid and flights are returned |
| `Verify` | Price confirmation works and a session is created   |
| `Order`  | The order can be created successfully               |
| `Pay`    | Payment is accepted                                 |

If all four steps pass, your sandbox environment is ready for integration work.

### What this does not validate

This test kit does **not** validate:

* full webhook handling
* edge-case or failure-path coverage
* production pricing or live airline behavior

Use it as a fast entry check, not as full integration proof.

### When to use it

Run this test:

* after you receive sandbox credentials
* before you start coding
* after network or IP changes
* when you want a quick environment health check

### Download the test kit

Use these files:

* `Atlas_UAT_HappyPath.postman_collection.json`

{% file src="../../.gitbook/assets/Atlas_UAT_HappyPath.postman_collection (2).json" %}

* `Atlas_UAT_Environment.json`

{% file src="../../.gitbook/assets/Atlas_UAT_Environment (2).json" %}

Download both files to the same local folder.

### Before you run it

Make sure you already have:

* valid sandbox credentials
* outbound network access to Atlas sandbox
* the ability to run Newman locally
* a future travel date for the test request

### How to run

{% stepper %}
{% step %}
### Fill in the environment file

Open `Atlas_UAT_Environment.json`.

Set:

* `client_id`
* `client_secret`
* `currency`
* `from_date`

For first-time integrations, Atlas may not have settlement currency configured yet.

Set `currency` to `USD` for sandbox testing unless your test case requires a different value.

Update `from_date` to a future date before you run the collection.
{% endstep %}

{% step %}
### Install Newman

Install Newman and the HTML reporter.

{% code title="Install Newman" %}
```bash
npm install -g newman newman-reporter-htmlextra
```
{% endcode %}
{% endstep %}

{% step %}
### Run the collection

Run the happy path collection with the environment file.

{% code title="Run the test kit" %}
```bash
newman run Atlas_UAT_HappyPath.postman_collection.json -e Atlas_UAT_Environment.json --delay-request 10000 --reporters htmlextra --reporter-htmlextra-export report.html
```
{% endcode %}

If the command fails, run it with `npx` instead.

{% code title="Fallback with npx" %}
```bash
npx newman run Atlas_UAT_HappyPath.postman_collection.json -e Atlas_UAT_Environment.json --delay-request 10000 --reporters htmlextra --reporter-htmlextra-export report.html
```
{% endcode %}
{% endstep %}

{% step %}
### Review the result

Open `report.html` after the run completes.

Expected runtime is about 2 to 3 minutes.
{% endstep %}
{% endstepper %}

### Expected result

Your sandbox setup is ready when:

* `Search` passes
* `Verify` passes
* `Order` passes
* `Pay` passes

You can treat this as a sandbox go signal.

Move on to API integration after these checks pass.

### Pass and fail criteria

Treat the run as a pass when the four core steps succeed:

* `Search`
* `Verify`
* `Order`
* `Pay`

Treat the run as a fail when any of those four steps fails.

### Known behavior

The final retrieve step may time out while polling for ticket issuance.

This is expected.

Ticketing is asynchronous.

A timeout on the final retrieve step does not affect sandbox environment validation.

{% hint style="info" %}
Focus on the four core steps: `Search`, `Verify`, `Order`, and `Pay`.

The final retrieve polling step is informational only.
{% endhint %}

### Common failure reasons

If the run fails early, check these items first:

* `client_id` or `client_secret` is missing or incorrect
* the wrong environment file is selected
* outbound network access is blocked
* the request source IP changed after allowlisting
* the collection or environment file name was changed locally
* Newman is installed but the reporter package is missing

#### Quick checks

Use this order:

1. confirm the credentials in the environment file
2. confirm the sandbox endpoint values
3. confirm your network can reach Atlas
4. rerun the collection without editing the request sequence
5. open `report.html` and check the first failed request

{% hint style="warning" %}
If `Search` fails, fix credentials or network first.

Do not continue to integration work until the happy path passes.
{% endhint %}

### If the run fails

Use this recovery order:

1. Confirm `client_id` and `client_secret` are correct.
2. Confirm `from_date` is still in the future.
3. Confirm the selected environment file is the sandbox file.
4. Confirm your network and source IP can reach Atlas.
5. Re-run the collection and inspect the first failed request in `report.html`.

### Output of this check

* validated sandbox credentials
* validated network reachability
* confirmed happy-path execution baseline

### What to do after it passes

After the test kit passes:

* start the API integration
* keep the same sandbox credentials for development
* continue with [Sandbox Development](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Xs5C4xGnhQl0A2GNjlwv)

### Related pages

* [Quick Start](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/MkEt9qjU24ig50fQ8be2)
* [Sandbox Access](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/O9n7Z0tHowy0I3hOF44f)
* [Sandbox Development](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Xs5C4xGnhQl0A2GNjlwv)
* [UAT Validation](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/aH2Shbpf2B9zZldFkBrT)
