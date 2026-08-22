# h-b

`h-b` is the operational COD skill for Algerian commerce. It is used when the payment method is cash on delivery and location selection must follow the 58 wilayas and their dependent baladiyas.

## Scope

The package covers the minimal customer data contract, canonical delivery lookups, server-side totals and stock, idempotent order creation, custom owner operations, privacy, analytics, testing and deployment controls. It intentionally keeps the owner route private from normal visitors.

## Use with

Read `SKILL.md` with [`../STANDARDS.md`](../STANDARDS.md). Combine it with `make-ur-kdb` when the user needs the full brand/storefront/admin implementation, or use it independently to retrofit trusted COD logic into an existing store.

## Source boundary

This is a functional pattern. It does not include customer records, order data, passwords, visual identity, code or assets from any source project.
