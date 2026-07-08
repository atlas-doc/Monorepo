---
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

Use [Void workflow](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/B8hsI0GKlmcexaJt4Npx).

### FAQ

#### What is the standard Atlas API void flow?

The standard flow is `voidQuotation.do` → `void.do` → `queryVoidOrders.do`.

Request quotation first.

Then submit the void with the latest `voidOfferId`.

After submission, query status until the case is completed or rejected.

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

Atlas VOID currently supports 23 airlines across four regions.

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

Recent additions:

* `TS`
* `Y4`
* `EI`
* `VF`

Coverage is airline- and route-specific.

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
* `voidCode` is used for status follow-up

### Main APIs

* `voidQuotation.do`
* `void.do`
* `queryVoidOrders.do`

### Request model

Use the dedicated void flow with these inputs:

* `voidQuotation.do`: `orderNo`
* `void.do`: `orderNo` + `voidOfferId`
* `queryVoidOrders.do`: `voidCode`

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

In most cases, Atlas returns within about 5 minutes whether the void request was accepted for processing.

Final completion or rejection can still take longer.

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

Read [Void Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/4aywYMVHUfvNZttgiHPn).

### Related pages

* [Refunds](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/4SLUBW4WrcN15Hl7KYDP)
* [Void Notification](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/4aywYMVHUfvNZttgiHPn)
* [Error Codes](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/Jk40OgfAM5G1NDZxwAS1)
* [Post-booking APIs](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/8P9YQq692vHSOmVjquJF)

{% openapi-operation spec="atlas-api" path="/voidQuotation.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/6d498c79f43546e63a2289f81c033345c8210830410d2835d33def093c5f3f29.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260708%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260708T131021Z&X-Amz-Expires=172800&X-Amz-Signature=a7df629c73fe758cf3eba4a8807d31e59e90f716b8c4749c291410c9e4c62e50&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="atlas-api" path="/void.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/6d498c79f43546e63a2289f81c033345c8210830410d2835d33def093c5f3f29.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260708%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260708T131021Z&X-Amz-Expires=172800&X-Amz-Signature=a7df629c73fe758cf3eba4a8807d31e59e90f716b8c4749c291410c9e4c62e50&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="atlas-api" path="/queryVoidOrders.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/6d498c79f43546e63a2289f81c033345c8210830410d2835d33def093c5f3f29.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260708%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260708T131021Z&X-Amz-Expires=172800&X-Amz-Signature=a7df629c73fe758cf3eba4a8807d31e59e90f716b8c4749c291410c9e4c62e50&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
