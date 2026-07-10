---
description: >-
  Common Atlas API access errors for authentication, request format, missing
  fields, and account-scope failures.
---

# Common & Access Errors

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when a request fails before business processing starts.

Start here when you need to:

* understand why a request failed before the business flow started
* check credentials, JSON format, or access scope
* decide whether to fix the request or retry once

### FAQ

#### Which common access errors usually need a request fix first?

Codes such as `100`, `901`, and `902` usually mean required fields, request format, or permission scope are not correct.

Fix the request before retrying.

#### Which common access errors can be retried once?

Codes such as `9999` or `-1` can be retried once when the issue looks transient.

If the same failure repeats, capture request context and escalate.

### What this page covers

* Missing fields
* Invalid request format
* Credential and access failures
* Generic system errors

### Common codes

#### `100` Missing required request data

A mandatory field is missing.

**Action**

* Check required parameters
* Rebuild the request body
* Retry after validation

#### `900` Unauthorized access

Credentials are wrong, account status is invalid, or the request targets data outside your scope.

**Action**

* Check `x-atlas-client-id`
* Check `x-atlas-client-secret`
* Confirm the account is active

#### `901` Illegal request data

The request format is invalid.

**Action**

* Send JSON
* Check field types and nesting
* Validate required structure before retry

#### `902` Access denied

The request is blocked due to permission or account scope.

**Action**

* Re-check credentials
* Confirm the account can access this capability
* Contact Atlas if the request should be allowed

#### `9999` System error

Unexpected platform-side failure.

**Action**

* Retry once
* If it repeats, capture request IDs and escalate

#### `-1` Common error

Fallback error used when a more specific code is not returned.

**Action**

* Check the request context
* Retry if transient
* Escalate if repeated

### Quick retry guide

#### Fix the request first

Examples:

* `100`
* `901`
* `902`

#### Retry once, then escalate if repeated

Examples:

* `9999`
* `-1`

### Recommended troubleshooting order

1. Confirm credentials and account status
2. Validate JSON format and required fields
3. Retry once for transient failures
4. Escalate with request context if the error repeats

### What comes next?

After the access or request issue is fixed, return to the workflow page you were trying to use and continue from there.

### Related pages

* [Authentication & Request Basics](../../../readme-1/making-requests.md)
* [Help & Support](../)
