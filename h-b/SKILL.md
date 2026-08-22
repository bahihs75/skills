---
name: h-b
description: Build a COD-first Algerian commerce workflow with 58 wilayas, dependent baladiyas, server-calculated totals, and a bespoke hidden owner console. Use when a store needs practical cash-on-delivery operations without exposing admin controls to customers.
---

# H.B Reference Skill

Build original COD commerce that is operationally ready for Algeria. Pair a minimal checkout with a deeper private owner workspace: customers submit only confirmation data, while the owner manages order status, delivery, catalogue and activity.

## Checkout contract

Collect full name, phone, wilaya, delivery type, and baladiya only for domicile. Support Stop Desk and domicile. Persist COD server-side. Reject unknown wilayas, mismatched baladiyas, invalid phones, empty bags, unavailable variants and tampered prices.

## Delivery and operations

Maintain all 58 wilayas as stable records. Model Stop Desk/domicile fees, availability, optional free-delivery rules and linked communes. Give the owner an order ledger, status transitions, notes, delivery matrix, bulk delivery updates, low-stock indicators and activity history.

## Security baseline

Calculate line totals, delivery fee, stock allocation and final total on the server. Keep the owner route direct but unadvertised in public UI and protect it with production identity or a securely configured owner secret. Do not create synthetic orders or customer data.

## Verification

Test valid Stop Desk and domicile orders, invalid baladiya rejection, protected owner APIs, status transitions, migration, public/admin separation and mobile checkout behavior.
