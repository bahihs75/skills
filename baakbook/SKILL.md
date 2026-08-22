---
name: baakbook
description: Plan and execute a safe migration of a small Flask or JSON-backed commerce application to managed hosting, authentication, database, functions, and media services. Use when a legacy single-instance store must modernize without losing customer or order data.
---

# Baakbook Reference Skill

Modernize a small commerce application without treating migration as a visual redesign. Start with source inventory, define a target data contract, reconcile every record, then move traffic through a deliberate cutover and observation period.

## Migration workflow

1. Inventory legacy files, database/JSON structures, customer data, order states, media references, secrets and current hosting behavior.
2. Design target schemas for products, settings, users, orders, media and audit fields before writing import code.
3. Create read-only inspection, transformation and reconciliation tooling. Require record counts and field-level difference reports before cutover.
4. Build the target runtime with managed identity, data-store authorization rules, secret configuration, and an operations dashboard.
5. Test a dry-run migration with anonymized data; do not commit live customer JSON or production credentials.
6. Perform a time-boxed production cutover, preserve a rollback path, monitor data integrity, and retire the old runtime only after a defined observation period.

## Architecture rules

Prefer a static/public frontend plus managed data/auth/functions when the system fits that model; use a server runtime where sensitive operations or integration boundaries require it. Treat a local JSON file as single-instance development storage, not a multi-instance production database.

## Acceptance criteria

Deliver source inventory, target schema, migration report, reconciliation result, role model, deployment checklist, privacy controls, rollback plan and post-cutover monitoring checklist.
