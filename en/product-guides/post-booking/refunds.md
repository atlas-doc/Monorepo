---
description: >-
  Atlas API refund flow for refund quotation, refund submission, and refund
  status tracking.
---

# Refunds

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this section for the full refund lifecycle.

Start here when you need to:

* decide whether the case should use **Refund** or **Void**
* follow the standard refund sequence
* confirm which identifiers to keep for follow-up

### FAQ

#### What is the standard Atlas API refund flow?

The standard flow is `refundQuotation.do` → `refund.do` → `queryRefundOrders.do`.

Start with quotation before submission.

#### When can a refund request fail even before submission?

Refund requests can fail when ticketing is not complete, the refund offer expired, the order number is wrong, or the itinerary is incomplete.

Check current order state and refund conditions first.

#### When should I use Refund instead of Void?

Use Refund when the case is outside the void window or needs the refund flow.

Use [Void](void.md) when the order is still eligible for the dedicated void flow.

### Typical flow

{% stepper %}
{% step %}
### Check refund eligibility

Call `refundQuotation.do` first.

Confirm the latest refundable amount and conditions.
{% endstep %}

{% step %}
### Submit the refund

Use the latest `refundOfferId` when the flow requires quotation-based submission.

Keep the returned `refundCode`.
{% endstep %}

{% step %}
### Query final status

Use `queryRefundOrders.do` until the case is completed, rejected, or otherwise closed.
{% endstep %}
{% endstepper %}

### What should you confirm before refund submission?

Confirm:

* the original `orderNo` is correct
* ticketing is complete when required
* the itinerary in the refund request is complete
* the latest `refundOfferId` or quotation result is still valid

The refund path and reconciliation timing can also depend on the payment mode.

### Use this page when you need

* voluntary refunds
* involuntary refunds
* refund status follow-up

### What this page does not cover

This page does not list full endpoint schemas or field-level definitions.

Use the API reference for request and response details.

### Full API reference

Use endpoint-level details here:

* [Refunds](../../api-reference/post-booking-apis/refunds.md)

### Related pages

* [Void](void.md)
* [Finance](../../support-and-reference/troubleshooting-and-support/faqs/atlas-api-finance.md)
* [Post-booking](../../support-and-reference/troubleshooting-and-support/faqs/atlas-api-post-ticketing.md)
* [Error Codes](../../support-and-reference/troubleshooting-and-support/errors-handing/)
* [Post-booking APIs](../../api-reference/post-booking-apis/)
