---
description: >-
  Atlas API search.do reference for retrieving flight offers and the
  routingIdentifier required by verify.do.
---

# Search

{% include "../../.gitbook/includes/eva-help-hint.md" %}

{% include "../../.gitbook/includes/environment-endpoint-note.md" %}

Use this endpoint when Atlas is your main shopping entry point.

It returns the `routingIdentifier` used by `verify.do`.

{% hint style="info" %}
`Smart Search` (`smartSearch.do`) will be deprecated soon.

Use `search.do` for new integrations.
{% endhint %}

{% hint style="warning" %}
`search.do` uses `10 QPS` by default.

Over-limit requests return `HTTP 429 Too Many Requests`.

Wait for the returned `retryAfter` value before retrying.
{% endhint %}

Use [API Request Limits](/broken/spaces/6LsKtmbJhZxgxraY5mHB/pages/EsovwRrOMFnJMFfWhnMV) for shared rules and counting details.

{% openapi-operation spec="atlas-api" path="/search.do" method="post" %}
[OpenAPI atlas-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/9dcd4bc9b39af8e0697eeeb02edb459eb14088e6acf7e1f061779a4a67a31524.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260712%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260712T083621Z&X-Amz-Expires=172800&X-Amz-Signature=d96b093f0818d36d49f45a087a44719b31b391c1572dd5420d410d5ff0bfd5ee&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
