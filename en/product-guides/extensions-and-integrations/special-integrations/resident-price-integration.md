---
description: >-
  Resident fare flow for Spain domestic routes with eligibility, discount codes,
  and required passenger proof data.
---

# Resident Price Integration

{% include "../../../.gitbook/includes/eva-help-hint.md" %}

Use this page when you need resident fare support for eligible Spain domestic bookings.

### When to use this flow

Use the resident fare flow only when:

* the passenger is eligible for Spain resident or family discount programs
* the route is a supported Spain domestic route
* you can collect the required proof fields during booking
* the airline supports resident fare handling

### Supported airlines

* `FR`
* `VY`

### Eligible passenger groups

This flow applies to legal residents of:

* Canary Islands
* Balearic Islands
* Ceuta
* Melilla

Residency proof is required, such as `DNI` or `NIE`, depending on the fare type.

### Eligible routes

Only domestic Spain routes are eligible, and the itinerary must match the resident program rules.

| Resident region  | Allowed route range                                        | Example     |
| ---------------- | ---------------------------------------------------------- | ----------- |
| Canary Islands   | Any airport in Spain ↔ any airport in the Canary Islands   | `MAD → TFS` |
| Balearic Islands | Any airport in Spain ↔ any airport in the Balearic Islands | `VLC → PMI` |
| Ceuta            | `JCU` ↔ `SVQ` / `XRY` / `AGP`                              | `JCU → AGP` |

### What the discount applies to

Resident pricing can apply to:

* base fare
* first baggage piece per passenger per segment
* infant fee
* mandatory seat selection fee

Government taxes and fees are **not** discounted.

### Discount codes

Use `residentCode` in the search request.

| Discount type                | Resident code | Discount |
| ---------------------------- | ------------- | -------- |
| Family Discount              | `DSC2`        | `5%`     |
| Large Family Discount        | `DSC3`        | `10%`    |
| SARA Resident Discount       | `DSC1`        | `75%`    |
| SARA + Family Discount       | `DSC4`        | `80%`    |
| SARA + Large Family Discount | `DSC5`        | `85%`    |

### Integration flow

{% stepper %}
{% step %}
### Search with `residentCode`

Pass `residentCode` in the search request to retrieve resident pricing.

If the route and traveler are eligible, the discounted price is applied in the search result.
{% endstep %}

{% step %}
### Verify and create the order

Continue the normal booking flow with verify and order creation.

The resident fare logic continues through later steps if the original search used `residentCode`.
{% endstep %}

{% step %}
### Send `residentInfo` during booking or ticketing flow

Pass resident proof fields for each relevant passenger.
{% endstep %}

{% step %}
### Airline performs final verification

The airline checks resident eligibility after ticketing.
{% endstep %}
{% endstepper %}

### Search request example

```json
{
  "tripType": "1",
  "adultNum": 1,
  "childNum": 0,
  "infantNum": 0,
  "fromCity": "SVQ",
  "toCity": "OVD",
  "fromDate": "20251103",
  "retDate": "20250603",
  "includeMultipleFareFamily": true,
  "currency": "",
  "requestSource": "",
  "residentCode": "DSC2"
}
```

### Required passenger proof fields

Pass `residentInfo` for each eligible passenger.

| Field             | Description                                           |
| ----------------- | ----------------------------------------------------- |
| `docType`         | Document type. Supported values are `D`, `E`, and `U` |
| `docNum`          | Required when `docType` is `D` or `E`                 |
| `municipality`    | Required for `DSC1`, `DSC4`, and `DSC5`               |
| `largeFamilyCert` | Required for `DSC2`, `DSC3`, `DSC4`, and `DSC5`       |
| `community`       | Required for `DSC2`, `DSC3`, `DSC4`, and `DSC5`       |

### Booking request example

```json
{
  "cid": "******",
  "sessionId": "5475cdb2-ce22-4e52-8c2f-8ef2e81e462c",
  "passengers": [
    {
      "name": "TEST/ONE",
      "passengerType": 0,
      "birthday": "19900101",
      "gender": "M",
      "cardNum": "00000000",
      "cardType": "PP",
      "cardIssuePlace": "SG",
      "cardExpired": "20301231",
      "nationality": "SG",
      "ancillaries": [],
      "residentInfo": {
        "docType": "D",
        "docNum": "99999999Z",
        "municipality": "",
        "largeFamilyCert": "06-9999-99",
        "community": "502973"
      }
    }
  ],
  "contact": {
    "name": "TEST/TEST",
    "address": null,
    "postcode": null,
    "email": "test@test.com",
    "mobile": "0086-13928109091"
  },
  "requestSource": ""
}
```

### Field requirements by discount code

| Resident code | `docType` | `docNum`                              | `municipality` | `largeFamilyCert` | `community`  |
| ------------- | --------- | ------------------------------------- | -------------- | ----------------- | ------------ |
| `DSC2`        | required  | required when `docType` is `D` or `E` | not required   | required          | required     |
| `DSC3`        | required  | required when `docType` is `D` or `E` | not required   | required          | required     |
| `DSC1`        | required  | required when `docType` is `D` or `E` | required       | not required      | not required |
| `DSC4`        | required  | required when `docType` is `D` or `E` | required       | required          | required     |
| `DSC5`        | required  | required when `docType` is `D` or `E` | required       | required          | required     |

### Reference files for coded fields

Use the files below to map names to coded values.

#### Municipality codes

The municipality code is a 6-digit value built from `CPOR + CMUN + DC`.

{% file src="../../../.gitbook/assets/25codmun (1).xlsx" %}

#### Community codes

{% file src="../../../.gitbook/assets/community (1).xlsx" %}

### Final verification behavior

Atlas passes resident fare details to the airline during fulfillment.

The airline verifies eligibility after ticketing.\
If verification fails:

* the booking is not automatically canceled
* the traveler may be asked to present proof at the airport

Make sure travelers are prepared with the required original documents.

### Related pages

* [Search](../../booking/booking-step-guides/search.md)
* [Create Order](../../booking/booking-step-guides/create-order.md)
* [Payment & Ticketing](../../booking/booking-step-guides/payment-and-ticketing/)
* [Special Integrations](./)
