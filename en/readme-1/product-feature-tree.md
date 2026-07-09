---
description: Complete Atlas API capability map showing all 26 endpoints and their dependencies
---

# Atlas API Capability Map

{% include "../.gitbook/includes/eva-help-hint.md" %}

Use this page to understand the full Atlas API landscape: three search entry points, five core business stages, and 26 API endpoints covering search, booking, payment, refunds, rebooking, and ancillary services.

---

## Overview

Atlas API is organized around three search entry points that feed into a common booking pipeline with five core stages.

<div style="display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 16px; margin: 24px 0;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; padding: 20px; text-align: center;">
    <div style="font-size: 28px; font-weight: 800; color: #1E40AF; line-height: 1.1;">3</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">Search entry points</div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; padding: 20px; text-align: center;">
    <div style="font-size: 28px; font-weight: 800; color: #1E40AF; line-height: 1.1;">5</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">Core stages</div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; padding: 20px; text-align: center;">
    <div style="font-size: 28px; font-weight: 800; color: #1E40AF; line-height: 1.1;">26</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">API endpoints</div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; padding: 20px; text-align: center;">
    <div style="font-size: 28px; font-weight: 800; color: #1E40AF; line-height: 1.1;">8</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">Integration paths</div>
  </div>
</div>

---

## Search Entry Points

Choose the right search endpoint for your use case:

<div style="display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 16px; margin: 24px 0;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #1E40AF;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Standard Search</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /search.do</div>
      <div style="font-size: 13px; color: #0F172A; line-height: 1.5;">Most common use case: one-way/return journeys, airline filtering, flight number targeting, multiple fare classes</div>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #3B82F6;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Direct Offer</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /getOffers.do</div>
      <div style="font-size: 13px; color: #0F172A; line-height: 1.5;">Skip search when you already know the exact flight and class you want to book; improves L2B conversion</div>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #F97316;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Smart Search</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /smartSearch.do</div>
      <div style="font-size: 13px; color: #0F172A; line-height: 1.5;">TMC-only; covers routes and time slots not available via standard Search</div>
    </div>
  </div>
</div>

---

## Standard Booking Flow

This is the complete standard booking journey.

{% tabs %}
{% tab title="Flow Diagram" %}

```mermaid
flowchart LR
    A[1. Search\n/search.do] --> B[2. Verify\n/verify.do]
    B --> C{Optional\nAncillaries}
    C --> D[3. Create Order\n/createOrder.do]
    D --> E[4. Pay\n/pay.do]
    E --> F[5. Retrieve Order\n/retrieveOrder.do]
    
    C -.-> L[Luggage\n/getLuggage.do]
    C -.-> S[Seat Selection\n/seatAvailability.do]
```

{% endtab %}
{% tab title="Step by Step" %}

### Step 1: Search flights

**Endpoint:** `POST /search.do`

Returns available flight options with a `routingIdentifier` used in subsequent calls.

Capabilities:
* Trip type (one-way / return)
* Passenger counts (adult / child / infant)
* Origin / destination city or airport IATA codes
* Departure / return dates (yyyyMMdd format)
* Airline / flight number filtering (optional)
* Multiple fare classes and currency options

---

### Step 2: Verify price

**Endpoint:** `POST /verify.do`

**Requires:** `routingIdentifier` from search

Validates the current price and returns:
* `sessionId` for booking
* `bookingRequirement` details
* Fare rules and cancellation policies
* Baggage allowance information

---

### Step 3 (Optional): Ancillary selection

Before creating the order, you can retrieve available ancillary options:

| Service | Endpoint | Returns |
|---------|----------|---------|
| Luggage options | `POST /getLuggage.do` | Available baggage tiers and prices |
| Seat selection | `POST /seatAvailability.do` | Seat maps with pricing per category |

Both endpoints require the `sessionId` from verify.

---

### Step 4: Create order

**Endpoint:** `POST /createOrder.do`

**Requires:** `sessionId` from verify

Creates the booking record and accepts:
* Passenger information (names, DOB, documents)
* Contact information (email, phone)
* Internal order reference (for reconciliation)
* Insurance and ancillary selections

Returns an `orderNumber` for payment and subsequent operations.

---

### Step 5: Payment

**Endpoint:** `POST /pay.do`

**Requires:** `orderNumber` from createOrder

Supported payment methods:
* Deposit (prepaid balance)
* VCC (virtual credit card)
* MoR (Merchant of Record) billing
* Credit cards: Visa / MC / AE / Discover

---

### Step 6: Retrieve order

**Endpoint:** `POST /retrieveOrder.do`

**Requires:** `orderNumber`

After successful payment, retrieve order details:
* Booking status and ticketing status
* Ticket numbers
* PNR information
* Passenger details
* Ancillary service status

{% endtab %}
{% endtabs %}

---

## Booking Flow API Cards

<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); gap: 16px; margin: 24px 0;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #1E40AF;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Search</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /search.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">Entry point (no dependency)</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">One-way / return trips</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Passenger counts (ADT/CHD/INF)</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Origin/destination IATA codes</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Departure/return dates</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Airline/flight number filters</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Multiple fare classes, currencies</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #3B82F6;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Verify</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /verify.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">Requires: search.do routingIdentifier</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Real-time price validation</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Returns sessionId for booking</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Returns bookingRequirement</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Fare rules/cancellation policy</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Baggage allowance details</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #059669;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Create Order</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /createOrder.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">Requires: verify.do sessionId</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Passenger info (names, DOB, docs)</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Contact info (email, phone)</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Internal order reference</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Insurance + ancillary selection</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Returns orderNumber</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #059669;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Pay</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /pay.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">Requires: createOrder.do orderNumber</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Deposit (prepaid balance)</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">VCC (virtual credit card)</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">MoR (Merchant of Record)</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Credit cards: Visa/MC/AE/Discover</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #059669;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Retrieve Order</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /retrieveOrder.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">Requires: pay.do success</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Booking & ticketing status</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Ticket numbers</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">PNR information</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Passenger details</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Ancillary service status</li>
      </ul>
    </div>
  </div>
</div>

---

## Direct Offer Flow (GetOffer)

Use the GetOffer flow when you already know the exact flight and fare class. This skips the search step and improves conversion.

<div style="display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 16px; margin: 24px 0;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #3B82F6;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Get Offer</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /getOffers.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">No dependency (2nd entry point)</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Airline, flight number, class</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Date, origin/destination</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Returns offerId + sessionId</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #3B82F6;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Get Offer Price</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /getOfferPrice.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">Requires: getOffers.do offerId</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Real-time exact pricing</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">For display and comparison</li>
      </ul>
    </div>
  </div>
</div>

{% hint style="success" %}
**Pro tip:** Use GetOffer when rebooking or when users select from cached search results. This reduces API calls and speeds up the booking process.
{% endhint %}

---

## Smart Search Flow (TMC only)

Smart Search is for TMC partners needing extended coverage.

<div style="display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 16px; margin: 24px 0;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #F97316;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Smart Search</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /smartSearch.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">Requires: TMC account permissions</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Extended route coverage</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Extended time slot coverage</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Returns routingIdentifier</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #F97316;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Price Compare Search</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /priceCompareSearch.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">Optional - comparison only</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Multi-flight comparison</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Flexible date comparison</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Price calendar view</li>
      </ul>
    </div>
  </div>
</div>

{% hint style="info" %}
SmartSearch covers routes and time slots not available via the standard Search endpoint. Contact your account manager to enable TMC-specific features.
{% endhint %}

---

## Post-ticketing Operations

After ticketing, these operations are available:

<div style="display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 16px; margin: 24px 0;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #DC2626;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Refund</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /refund.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">Requires: ticketed order</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Partial or full refunds</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Voluntary or involuntary</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Refund amount calculation</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Status tracking</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #DC2626;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Regenerate Order</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /regenerateOrder.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">Requires: ticketed order</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Order regeneration</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Rebook scenario support</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Preserves original order info</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #DC2626;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Stop Ticketing</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /stopTicketIssuance.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">Requires: paid, not ticketed</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Emergency stop before ticketing</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Post-payment rapid response</li>
      </ul>
    </div>
  </div>
</div>

---

## Ancillary Services

Additional services that can be added pre or post booking:

<div style="display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 16px; margin: 24px 0;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #059669;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Luggage</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /getLuggage.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">Timing: After verify, before createOrder</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Baggage tier options</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Per-category pricing</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #059669;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Seat Selection</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /seatAvailability.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">Timing: After verify, before createOrder</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Interactive seat maps</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Category-based pricing</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #059669;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Post-ticketing Ancillaries</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /bookAncillary.do</div>
      <div style="font-size: 11px; color: #F97316; font-style: italic; margin-bottom: 6px;">Timing: After ticketing</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Add luggage post-ticketing</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Select seats post-ticketing</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Separate ancillary payment</li>
      </ul>
    </div>
  </div>
</div>

---

## Webhook Notifications

Atlas can push event notifications to your system via webhooks.

### Event Types

<div style="display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 12px; margin: 20px 0;">
  <div style="background: #FFFFFF; border-radius: 8px; border: 1px solid #CBD5E1; padding: 14px; border-left: 3px solid #3B82F6;">
    <div style="font-family: monospace; font-size: 12px; font-weight: 600; color: #3B82F6;">TICKETING_COMPLETE</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">Ticketing completed successfully</div>
  </div>
  <div style="background: #FFFFFF; border-radius: 8px; border: 1px solid #CBD5E1; padding: 14px; border-left: 3px solid #DC2626;">
    <div style="font-family: monospace; font-size: 12px; font-weight: 600; color: #DC2626;">VOID_NOTIFICATION</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">Order voided</div>
  </div>
  <div style="background: #FFFFFF; border-radius: 8px; border: 1px solid #CBD5E1; padding: 14px; border-left: 3px solid #F97316;">
    <div style="font-family: monospace; font-size: 12px; font-weight: 600; color: #F97316;">SCHEDULE_CHANGE</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">Flight schedule changed</div>
  </div>
  <div style="background: #FFFFFF; border-radius: 8px; border: 1px solid #CBD5E1; padding: 14px; border-left: 3px solid #059669;">
    <div style="font-family: monospace; font-size: 12px; font-weight: 600; color: #059669;">AIRLINE_STATUS_UPDATE</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">Airline status update</div>
  </div>
  <div style="background: #FFFFFF; border-radius: 8px; border: 1px solid #CBD5E1; padding: 14px; border-left: 3px solid #8B5CF6;">
    <div style="font-family: monospace; font-size: 12px; font-weight: 600; color: #8B5CF6;">EMAIL_NOTIFICATION</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">Email notification sent</div>
  </div>
  <div style="background: #FFFFFF; border-radius: 8px; border: 1px solid #CBD5E1; padding: 14px; border-left: 3px solid #0891B2;">
    <div style="font-family: monospace; font-size: 12px; font-weight: 600; color: #0891B2;">INCIDENT_NOTIFICATION</div>
    <div style="font-size: 12px; color: #64748B; margin-top: 4px;">Incident event</div>
  </div>
</div>

### Registration & Query

```mermaid
sequenceDiagram
    participant Client
    participant Atlas
    participant Webhook

    Client->>Atlas: Register webhook
    Atlas->>Client: signingKey
    Note over Client,Atlas: Book normally
    Client->>Atlas: search → verify → order → pay
    
    Note over Atlas,Webhook: Events trigger push
    Atlas->>Webhook: Ticketing complete
    Webhook->>Client: TICKETING_COMPLETE event
    Note right of Client: Validate signature with signingKey
    Client->>Webhook: 200 OK
```

---

## Order Management & PNR

<div style="display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 16px; margin: 24px 0;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #0891B2;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Order List</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /orderList.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Filter by date range</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Filter by status</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Pagination support</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #0891B2;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Extract PNR</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /extractPnr.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Raw PNR content</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">E-ticket information</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #0891B2;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">PNR Claim</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /pnrClaim.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Claim PNR ownership</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Bind to order reference</li>
      </ul>
    </div>
  </div>
</div>

---

## Utility Endpoints

<div style="display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 16px; margin: 24px 0;">
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #6366F1;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Balance</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /balance.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Account balance check</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Multi-currency support</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #6366F1;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Flight Data Feed</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /flightDataFeed.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Full route data export</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Incremental sync</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #6366F1;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">Email Query</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /emailQuery.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Email content lookup</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Attachment downloads</li>
      </ul>
    </div>
  </div>
  <div style="background: #FFFFFF; border-radius: 10px; border: 1px solid #CBD5E1; overflow: hidden;">
    <div style="height: 4px; background: #6366F1;"></div>
    <div style="padding: 16px;">
      <div style="font-size: 15px; font-weight: 700; color: #1E40AF; margin-bottom: 4px;">aTrip Token</div>
      <div style="font-family: monospace; font-size: 11px; color: #3B82F6; margin-bottom: 8px;">POST /atripToken.do</div>
      <ul style="padding-left: 16px; margin-top: 6px;">
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Obtain access tokens</li>
        <li style="font-size: 12px; color: #0F172A; line-height: 1.6;">Token refresh mechanism</li>
      </ul>
    </div>
  </div>
</div>

---

## API Dependency Reference

This table shows the key parameter flows between endpoints:

| API | Depends on | Key parameters passed |
|-----|-----------|----------------------|
| `search.do` | - | `routingIdentifier` → Verify |
| `verify.do` | `search.do` | `sessionId` → CreateOrder / rules / baggage |
| `createOrder.do` | `verify.do` / `getOffers.do` | `sessionId`, `bookingRequirement` |
| `getOffers.do` | - | `offerId`, `sessionId` |
| `pay.do` | `createOrder.do` | `orderNumber` |
| `refund.do` | `retrieveOrder.do` | `orderNumber`, `ticketNumber` |
| `getLuggage.do` | `verify.do` | `sessionId` |
| `seatAvailability.do` | `verify.do` | `sessionId` |
| `bookAncillary.do` | `retrieveOrder.do` | `orderNumber` |
| `regenerateOrder.do` | `retrieveOrder.do` | `orderNumber` |

---

### Key Takeaways

* **Entry points:** `search.do`, `getOffers.do`, `smartSearch.do`
* **Mandatory flow:** Search/GetOffer → Verify → CreateOrder → Pay → RetrieveOrder
* **Optional steps:** Luggage / Seat / Ancillary
* **Post-ticketing:** Refund / Regenerate / BookAncillary / OrderList
* **Notifications:** Webhook registration + event consumption

### Related Sections

* [Booking Overview](../product-guides/booking/booking-overview/) - Choose the right booking flow
* [API Reference](../api-reference/) - Complete endpoint specifications
* [Webhook Overview](../product-guides/extensions-and-integrations/webhook-overview/) - Notification setup and handling
