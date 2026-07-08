---
description: >-
  Common Atlas API search errors for request validation, balance, route
  restrictions, timeouts, and smart search follow-up.
---

# Search Errors

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when `search.do`, `smartSearch.do`, or `getOffers.do` fails.

Start here when you need to:

* understand why a search request failed
* decide whether the issue is input, balance, route, timeout, or concurrency related
* know whether to retry, fix, or restart the search

### FAQ

#### Which search errors are usually safe to retry?

Timeout and transient load cases such as `112` or `127` are usually retryable after a short wait.

QPS and route-control cases such as `110` or `108` usually need back-off or a condition change first.

#### Which search errors usually need an input fix first?

Codes such as `102`, `124`, and `126` usually mean the request fields, settlement currency, or smart search context are not valid for reuse.

Fix the input or restart the flow before retrying.

### Highest-frequency codes

#### `102` Illegal request param

One or more search fields are invalid.

**Typical causes**

* No adult passenger
* Too many passengers
* Invalid city code
* Missing `fromDate` or `retDate`
* Bad date format

**Action**

* Validate trip type
* Validate passenger counts
* Validate city and airport codes
* Use `YYYYMMDD` for dates

#### `107` Insufficient balance

Account balance is below the required threshold.

**Action**

* Top up the account
* Re-run the search after balance is updated

#### `108` Route restricted / system limitations

Atlas has closed sales for this route or flow.

**Action**

* Retry later
* Check with Atlas if this route should be available

#### `110` Too many concurrent requests

Search QPS is above the allowed limit.

**Action**

* Throttle request bursts
* Add retry and queue control
* Contact Atlas if higher throughput is required

#### `429`

Atlas rejected the request because the active request limit was exceeded.

This is the Atlas request-limit error code.

**Action**

* read `retryAfter`
* wait for that delay before retrying
* reduce duplicate search bursts and improve cache reuse

#### `112` or `127` Search timeout

The search did not complete in time.

**Action**

* Retry the search
* Reduce burst load
* Use smart search or polling when applicable

#### `123` Too many requests but too few paid orders

Search volume is high compared to paid orders.

**Action**

* Reduce unnecessary search traffic
* Avoid synthetic or duplicate search bursts

#### `124` Unsupported settlement currency

The currency is not allowed for settlement.

**Action**

* Switch to the account settlement currency

#### `126` `requestId` does not exist or has already ended

The smart search `requestId` is invalid or expired.

**Action**

* Start a new smart search
* Use the new `requestId`

### Quick retry guide

#### Retry after a short wait

Examples:

* `112`
* `127`

#### Retry only after changing the condition

Examples:

* `429`
* `108`
* `110`

#### Fix the request before retry

Examples:

* `102`
* `124`
* `126`

### Quick troubleshooting checklist

1. Validate required fields and date format
2. Check balance and settlement currency
3. Confirm the route is supported
4. Check concurrency and retry behavior
5. Re-run smart search if `requestId` expired

### `110` versus `429`

Use this distinction during troubleshooting:

* `110` is an Atlas business code for search concurrency pressure
* `429` is an Atlas request-limit error code

Both require lower request frequency.

For `429`, always honor `retryAfter` before retrying.

### What comes next?

After you fix the search issue, return to [Search](https://app.gitbook.com/s/cAlPPpTunfEGdmk5fy1e/readme/booking-overview/search) and continue the booking flow with the correct identifier.

### Related pages

* [Search](https://app.gitbook.com/s/cAlPPpTunfEGdmk5fy1e/readme/booking-overview/search)
* [Booking APIs](https://app.gitbook.com/s/cAlPPpTunfEGdmk5fy1e/api-reference/booking-apis)
* [Finance](https://app.gitbook.com/s/cAlPPpTunfEGdmk5fy1e/troubleshooting-and-support/faqs/atlas-api-finance)
