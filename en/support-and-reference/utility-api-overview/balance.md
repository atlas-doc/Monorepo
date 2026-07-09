---
description: Balance query API for finance and operational checks.
---

# Balance

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this page to check the current account balance.

### Main API

* `balance.do`

### Use this when you need

* Finance checks before payment activity
* Balance reconciliation
* Support confirmation for insufficient balance cases

### Key input

Send:

* `currency`

Use the settlement currency of the balance account you want to check.

### What the response gives you

The response can include:

* account balance amount
* settlement currency

### Best practice

* query balance before high-volume payment activity
* check the correct currency account
* use the returned amount for operational checks only
* rely on response `status` for success handling

### What to watch

* balances are currency-specific
* low balance can block deposit payments
* `msg` is descriptive only and should not drive logic

### Full API reference

See the complete endpoint schemas and samples here:

[Balance](../../api-reference/utility-apis/balance.md)
