---
description: >-
  How to follow an order after pay.do, when to keep polling
  queryOrderDetails.do, and why this is not a separate booking step.
---

# Post-payment polling

{% include "../../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when payment succeeded but ticketing is not final yet.

This is not a separate booking step.

The standard flow still ends with order follow-up through `queryOrderDetails.do`.

### Short answer

`pay.do` success does not always mean ticketing is complete.

Keep polling `queryOrderDetails.do` until the final ticketing state is confirmed.

Treat this page as follow-up guidance for the `Query Order` step.

Use webhook as a supplement, not as the only confirmation path.

### FAQ

#### When should I start polling?

Start after `pay.do` returns and the order enters post-payment follow-up.

#### When can I stop polling?

Stop when the order reaches a final ticketed outcome or another confirmed terminal state.

#### Should webhook replace polling?

No.

Webhook helps, but order query should remain your main status source.

### What payment success does not guarantee

Payment success does not always guarantee:

* airline PNR is already available
* ticket numbers are already issued
* ticketing is already complete

Treat payment and final ticketing as separate milestones.

### Main status source

Use `queryOrderDetails.do` as the main source of truth after payment.

Check at least:

* `orderStatus`
* `ticketStatus`
* airline PNR details
* ticket numbers when available

### Recommended polling pattern

Use a controlled polling loop.

A practical pattern is:

1. call `queryOrderDetails.do` after `pay.do`
2. continue polling with back-off while ticketing is still in progress
3. stop only after a final outcome is confirmed

#### Suggested pacing

Start with short intervals.

Then widen the interval if ticketing is still in progress.

Do not hammer the order query endpoint in tight loops.

### When not to retry payment

Do not retry `pay.do` just because ticket numbers are not present yet.

Check order state first.

This is especially important for cases such as:

* `402`
* `404`
* `406`
* `615`

### Common timing scenarios

#### Payment succeeded and ticketing is still running

Keep polling.

This is normal.

#### Payment is in progress

Do not send another payment request.

Wait and query the order again.

#### Payment succeeded but PNR is still missing

Do not retry payment.

Monitor the order state instead.

#### Ticketing is delayed longer than expected

Keep the order under follow-up.

Escalate with order context if the state is stuck or repeated errors appear.

### Common mistakes

#### Stopping after the first successful payment response

Do not do this.

The order may still be ticketing.

#### Retrying payment while the first payment is still processing

Do not do this.

This creates duplicate-payment risk.

#### Using webhook as the only completion signal

Do not do this.

Keep polling until the final order state is confirmed.

### Best practice

Log these values through the full follow-up chain:

* `orderNo`
* payment request time
* latest `orderStatus`
* latest `ticketStatus`
* airline PNR when available
* final ticket numbers when available

### Related pages

* [Payment & Ticketing](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/WK8UWUaHjby25uukAxCB)
* [Query Order](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/2yNUkts3yozduQUMF05n)
* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)
* [Payment Errors](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/v1plEh7MJqP2ZqtiNvxk)
* [Webhook Overview](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/1kDgZtL5TYuOLUmAxRd6)
