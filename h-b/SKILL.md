---
name: h-b
description: Build a production-minded Algerian COD commerce system with all 58 wilayas, dependent baladiyas, Stop Desk/domicile rules, server-authoritative inventory and totals, a private bespoke owner console, operational activity history, and responsive checkout. Use when cash-on-delivery is the sole payment method.
---

# H.B — Algerian COD Commerce and Private Operations

This skill is an end-to-end pattern for practical COD retail. Customers complete a minimal delivery request; the server guarantees product, delivery, total and status integrity; owners operate a custom unadvertised control room. Read [`../STANDARDS.md`](../STANDARDS.md) first.

## 1. Customer checkout contract

Collect only full name, phone number, selected wilaya, delivery type and baladiya if the type is domicile. The delivery types are `stop_desk` and `domicile`. COD is persisted as the only payment preference. Do not collect email, online-payment details, free-form address or unrelated profile data unless the user explicitly adds a lawful operational reason.

| Field | Validation | Server rule |
| --- | --- | --- |
| customerName | trimmed, bounded human-readable name | Required; store order snapshot only. |
| phone | normalized local/international format | Required; never render publicly. |
| wilayaCode | member of canonical 58-wilaya dataset | Required; derive canonical wilaya name server-side. |
| deliveryType | `stop_desk` or `domicile` enum | Required; selects valid fee and location rules. |
| baladiya | canonical commune for selected wilaya | Required only for domicile; rejected for mismatched wilaya. |
| cart lines | product/variant IDs and quantities | Re-read current data; never trust submitted title/price/stock. |
| idempotencyKey | high-entropy bounded token | One successful order per key. |

## 2. Data structures and state machine

Model `Wilaya`, `Commune`, `DeliveryRule`, `Product`, `Variant`, `InventoryReservation`, `Cart`, `Order`, `OrderLineSnapshot`, `CustomerSnapshot`, `DeliverySnapshot`, `OrderNote`, and `ActivityEvent`. Store canonical wilaya and commune data as stable lookup records or a versioned seed dataset. Build a `Map<wilayaCode, Commune[]>` for client display and validate again using server lookup.

Use explicit status transitions such as `requested → confirmed → preparing → dispatched → delivered`, with allowed cancellation/failed-delivery branches based on operation rules. Record actor, reason, prior and next state. Put a unique index on idempotency key and indexes on order status/createdAt, phone hash where allowed, wilaya code and owner queue sort order.

## 3. Trusted order transaction

In one transaction or compensating workflow: validate request schema, load visible variants, lock/check stock, calculate exact line totals from persisted price, choose delivery rule, calculate fee, create immutable snapshots, reserve/decrement inventory based on policy, create order and activity event, and return a safe confirmation code. On retries return the existing order for the same idempotency key. Release expired reservations through a bounded background process when the architecture uses reservations.

## 4. Public UI/UX

Design a clear retail journey: discovery, product detail, bag, checkout, confirmation and contact. Checkout must show the selected delivery method and fee before submit, disclose that COD is the only method, use a select for all wilayas, and reveal/clear baladiya only for domicile. Preserve the value when switching options only when valid; otherwise explain why it was cleared. Provide loading, stock-error, invalid-phone, invalid-location, empty bag and successful confirmation states.

Use KDB-quality visual restraint: named palette tokens, editorial type hierarchy, high-quality icons instead of emojis, generous product imagery, 44px mobile targets, one-column collapse and no horizontal scroll. The owner console is never linked from the public header, footer, sitemap or marketing copy.

## 5. Owner console

Implement Overview, COD Orders, Delivery Matrix, Catalogue, Storefront Content, Media, Activity, Settings and Backup/Export. Orders display customer/delivery snapshots, line totals, COD state, notes and allowed transitions. Delivery Matrix manages 58 wilayas, methods, fees, availability and bulk changes. Catalogue manages product/variant visibility, stock state, media roles and collection membership. All mutations require owner authorization and emit activity events.

## 6. API, observability and testing

Create versioned APIs for public catalog/checkout and protected operations. Validate every field at the edge; rate limit checkout; set explicit timeouts for messaging/notification calls; log request IDs and failure code without leaking customer data. Track funnel events and operational state distribution without collecting unnecessary PII.

Test valid Stop Desk order, valid domicile order, missing/invalid baladiya, mismatched wilaya/commune, out-of-stock variant, tampered price, duplicate idempotency retry, forbidden admin mutation, status-transition denial, delivery bulk update, mobile selection behavior, accessibility and restore validation.
