---
name: baakbook
description: Plan and execute a safe migration of a small Flask, JSON-backed, or single-instance commerce application to managed hosting, authentication, database, server functions, media storage, and observability. Use when a legacy store must modernize without data loss or an unsafe cutover.
---

# Baakbook — Safe Commerce Modernization and Migration

This skill modernizes a small commerce system without hiding migration risk behind a visual redesign. It starts with source evidence, builds a target contract, migrates through reconciliation, and releases with rollback capability. Read [`../STANDARDS.md`](../STANDARDS.md) first.

## 1. Migration discovery record

Inventory every runtime, source file, environment variable, dependency, JSON/database record, media path, scheduled task, form, payment/delivery integration, identity flow and operational manual step. Classify data as public content, operational configuration, customer PII, order history, financial-like record, media or secret. Record source counts, data quality findings, retention obligations and downtime tolerance before choosing a target platform.

## 2. Target architecture and data model

Move from a single mutable JSON file or local server state to managed services appropriate to the user’s selected provider pair. Keep public web, API/function layer, trusted business services, database, object storage, identity and background work separate. Prefer normalized entities and append-only history for orders/changes.

| Legacy concept | Target record | Migration rule |
| --- | --- | --- |
| product JSON | products, variants, collections, media references | Preserve IDs/provenance; normalize fields; quarantine invalid rows. |
| settings JSON | typed store settings/version | Merge with defaults, track revision/publisher. |
| order JSON | orders, immutable lines/delivery/customer snapshots, activity | Preserve original timestamps/status and source ID. |
| local uploads | object storage objects plus media metadata | Upload checksum-verified copies; do not use local runtime paths. |
| owner password/token | managed identity or server-side secret/config | Never migrate raw credential values into client storage. |

Design foreign keys/references, indexes for public products and operational queues, idempotency constraints, UTC times, money in minor units/decimal and reversible migrations. Document how deleted/archived legacy data is handled.

## 3. Extraction, transformation and reconciliation

Create separate read-only extraction, pure transformation and import layers. Save a source manifest with row counts and checksums. Validate shapes before transformation, normalize phone/currency/date fields explicitly, preserve a `legacySourceId`, and create an error/quarantine report rather than silently dropping bad records.

Before cutover, compare source and target counts by entity/status, compare representative field values, verify media accessibility, detect duplicates, reconcile order totals and produce a signed/dated migration report. Run dry-runs against a non-production target with anonymized customer data whenever possible.

## 4. Cutover and rollback

Use a staged path: prepare schema and permissions; dry-run; seed static/public data; verify; place legacy writes into controlled maintenance/read-only mode; run final delta import; reconcile; switch traffic; monitor; retain rollback capability. Do not destroy the source until the defined observation window has passed. A rollback plan must specify DNS/runtime switch, write freeze, data divergence handling and responsible operator.

## 5. UX and operations during modernization

Do not let the migration break customer paths. Preserve product slugs or map redirects, design clear unavailable/maintenance states, provide a branded error/not-found page and keep public forms validated/rate-limited. Give owners an admin migration dashboard only when it shows actionable state: import progress, exceptions, record counts, last backup and cutover readiness—not fabricated progress metrics.

## 6. Testing and handover

Test transformation functions, duplicate handling, schema migration upgrade/downgrade, permission boundaries, media checksums, retry/idempotency, replay of a representative order, failure mid-import, recovery after restart, performance on production-scale data and post-cutover smoke flow. Deliver architecture record, schema, import logs, reconciliation report, environment table, migration/cutover runbook, rollback procedure and monitoring plan.
