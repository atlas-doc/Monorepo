---
description: Supported locale values by airline for request fields such as FR order locale.
---

# Locale Reference

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when an airline requires a supported locale value in the request.

### What this page covers

This page lists supported locale values by airline.

Use these values in request fields such as `locale` when the airline flow requires them.

### When locale matters

Locale is most relevant when:

* the airline requires a market-specific language or country code
* the booking flow displays airline-hosted confirmation or checkout content
* FR-specific order flows require a locale value

### Where to use it

Use locale with:

* [Create Order](../../../product-guides/booking/booking-step-guides/create-order.md)
* [FR Integration](../../../product-guides/extensions-and-integrations/special-integrations/fr-integration.md)

### FR supported locale values

**FR:**

| Value | Language   | Country        | Culture |
| ----- | ---------- | -------------- | ------- |
| ie/en | English    | Ireland        | en-IE   |
| gb/en | English    | Great Britain  | en-GB   |
| at/de | German     | Austria        | de-AT   |
| be/nl | Dutch      | Belgium        | nl-BE   |
| be/fr | French     | Belgium        | fr-BE   |
| bg/bg | Bulgarian  | Bulgaria       | bg-BG   |
| cn/zh | Chinese    | China          | zh-CN   |
| cz/cs | Czech      | Czech Republic | cs-CZ   |
| dk/da | Danish     | Denmark        | da-DK   |
| fr/fr | French     | France         | fr-FR   |
| de/de | German     | Germany        | de-DE   |
| gr/el | Greek      | Greece         | el-GR   |
| hu/hu | Hungarian  | Hungary        | hu-HU   |
| it/it | Italian    | Italy          | it-IT   |
| lv/lv | Latvian    | Latvia         | lv-LV   |
| lt/lt | Lithuanian | Lithuania      | lt-LT   |
| lu/fr | French     | Luxembourg     | fr-LU   |
| nl/nl | Dutch      | Netherlands    | nl-NL   |
| no/no | Norwegian  | Norway         | nb-NO   |
| pl/pl | Polish     | Poland         | pl-PL   |
| pt/pt | Portuguese | Portugal       | pt-PT   |
| ro/ro | Romanian   | Romania        | ro-RO   |
| es/ca | Catalan    | Spain          | ca-ES   |
| es/es | Spanish    | Spain          | es-ES   |
| se/sv | Swedish    | Sweden         | sv-SE   |
| us/en | English    | United States  | en-US   |

### Tips

* use only values published for the airline
* do not assume culture values are interchangeable with request locale values
* keep locale consistent with the airline-specific flow you expose to users

### Related pages

* [Reference Data](./)
* [Integration Reference](../)
* [FR Integration](../../../product-guides/extensions-and-integrations/special-integrations/fr-integration.md)
* [Create Order](../../../product-guides/booking/booking-step-guides/create-order.md)
* [Special Integrations](../../../product-guides/extensions-and-integrations/special-integrations/)
