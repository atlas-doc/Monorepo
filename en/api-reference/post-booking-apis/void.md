---
description: >-
  Atlas API void reference for checking void eligibility, submitting void
  requests, and tracking their status.
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Void

{% include "../../.gitbook/includes/eva-help-hint.md" %}

Use this section for the dedicated void lifecycle.

Start here when you need to:

* check whether an order is still voidable
* submit a void request with the latest `voidOfferId`
* track void processing and outcome

Need the workflow guide first?

Use [Void workflow](../../product-guides/post-booking/void.md).

### FAQ

#### What is the standard Atlas API void flow?

The standard flow is `voidQuotation.do` → `void.do` → `queryVoidOrders.do`.

Request quotation first.

Then submit the void with the latest `voidOfferId`.

After submission, query status with `orderNo`.

Add `voidCode` when you want a specific void case.

#### Will Atlas reject a void request after the deadline?

Yes.

If the returned same-day void deadline has already passed, `void.do` fails in real time.

Typical error message:

* `Void deadline exceeded. This ticket can no longer be voided`

#### Does Atlas support partial-pax void?

No.

Atlas accepts full-order void only.

Do not submit void for only some passengers.

#### Is `voidQuotation.do` still required when the service fee is fixed?

Yes.

Call `voidQuotation.do` before every `void.do` request.

#### When should I use Void instead of Refund?

Use Void when the order is still inside the airline void window.

Use Refund when the void window has passed or the case needs the refund flow.

### Current VOID coverage

Atlas VOID supports 23 airlines across four regions as of July 2026.

Coverage is airline-, route-, and account-specific.

#### Americas

* `AS`
* `DM`
* `F9`
* `G4`
* `PB`
* `SY`
* `TS`
* `Y4`

#### Europe

* `A3`
* `D8`
* `EI`
* `DY`
* `N0`
* `OA`
* `VF`
* `Z0`

#### Japan

* `ZG` — US routes only

#### Korea

* `7C`
* `BX`
* `LJ`
* `RS`
* `TW`
* `ZE`

Recent additions as of July 2026:

* `TS`
* `Y4`
* `EI`
* `VF`

If the booking is outside this scope, Atlas can return `843`.

### What this section covers

* Request void quotations
* Submit void requests
* Query void status and results

### Typical flow

{% stepper %}
{% step %}
### Void Quotation

Check whether the order is voidable.

Read the latest amount, method, and `voidOfferId`.
{% endstep %}

{% step %}
### Submit Void

Submit the void request with the latest quotation result.

Keep the returned `voidCode` for follow-up.
{% endstep %}

{% step %}
### Query Void Status

Track progress until the void is completed, rejected, or otherwise closed.

Use `orderNo` as the main query key.

Add `voidCode` when you want to narrow the result to one void case.
{% endstep %}
{% endstepper %}

### What should you confirm before void submission?

Confirm:

* the original `orderNo` is correct
* the order is still inside the airline void window
* the returned same-day deadline has not passed yet
* the latest `voidOfferId` is used
* the case should go through Void, not Refund

Void handling is usually stricter than refund handling.

Window expiry can make the order non-voidable even if refund is still possible.

If the deadline already passed, Atlas rejects the void request immediately.

### Key behavior

* Void uses dedicated endpoints
* quotation should run before submission
* `voidOfferId` is used for submission
* `orderNo` is used for void query
* `voidCode` can narrow query follow-up to one void case

### Main APIs

* `voidQuotation.do`
* `void.do`
* `queryVoidOrders.do`

### Request model

Use the dedicated void flow with these inputs:

* `voidQuotation.do`: `orderNo`
* `void.do`: `orderNo` + `voidOfferId`
* `queryVoidOrders.do`: `orderNo` + optional `voidCode`

{% hint style="warning" %}
Void should be handled at order level.

Do not treat Void like a partial refund flow.

Atlas accepts full-order void only.
{% endhint %}

### Endpoint notes

#### `voidQuotation.do`

Use quotation to get the latest void eligibility and amount.

Expect the response to answer:

* whether the order is voidable
* which `voidMethod` applies
* which `voidOfferId` to use next

Important fields to read first:

* `isVoidable`
* `voidOfferId`
* `expectedConfirmationDate`
* `expectedRefundDate`
* `voidWindow.sameDayDeadlineTime`
* `voidWindow.sameDayTimezone`

#### `void.do`

Submit the void with the latest `voidOfferId`.

Keep the returned `voidCode`.

Use that code for all later status follow-up.

Do not skip quotation, even when the service fee is fixed.

If the returned same-day deadline already passed, Atlas rejects the request in real time.

#### `queryVoidOrders.do`

Use query to track the void after submission.

Pass `orderNo` as the main query key.

Add `voidCode` when you want one specific void case under that order.

Atlas usually returns a processing decision within about five minutes.

Final completion or rejection can still take longer.

This is a typical operating result, not a contractual SLA.

Important fields to read first:

* `voidCode`
* `voidStatus`
* `cancelReason`
* `actualRefundAmount` when available

### Status handling

The main outcome states to watch are:

* processing
* refunded or fulfillment done
* rejected

If the void is rejected, check `cancelReason` first.

If the void window expired, move the case to the refund flow when applicable.

### Integration notes

Use the latest quotation result before submission.

Do not reuse an older `voidOfferId`.

Treat the void window as strict.

If the order is no longer voidable, do not keep retrying the void path.

### Webhook option

Atlas can also send `order.void` to your registered webhook URL.

Use it after `void.do` for near-real-time status updates.

Webhook is the recommended way to follow progress changes after submission.

Read these fields first:

* `data.orderNo`
* `data.voidCode`
* `data.voidStatus`
* `data.message`

No extra webhook registration is required.

Use the same URL registered through `updateWebhookURL.do`.

Use `queryVoidOrders.do` when you need final reconciliation.

Read [Void Notification](../../product-guides/extensions-and-integrations/webhook-overview/void-notification.md).

### Related pages

* [Refunds](refunds.md)
* [Void Notification](../../product-guides/extensions-and-integrations/webhook-overview/void-notification.md)
* [Error Codes](../../support-and-reference/troubleshooting-and-support/errors-handing/)
* [Post-booking APIs](./)

{% openapi-operation spec="atlas-api" path="/voidQuotation.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T083622Z&X-Amz-Expires=172800&X-Amz-Signature=8ecfe8fda6f5a32473da008d6ddf175f45c50f70ab0fd5ec308bd5af9cad3aaa&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="atlas-api" path="/void.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T083622Z&X-Amz-Expires=172800&X-Amz-Signature=8ecfe8fda6f5a32473da008d6ddf175f45c50f70ab0fd5ec308bd5af9cad3aaa&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="atlas-api" path="/queryVoidOrders.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T083622Z&X-Amz-Expires=172800&X-Amz-Signature=8ecfe8fda6f5a32473da008d6ddf175f45c50f70ab0fd5ec308bd5af9cad3aaa&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
