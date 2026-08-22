# baakbook

`baakbook` is the migration skill for turning a small or JSON-backed commerce application into a managed, secure and observable product. It is appropriate when a local Flask/Node application or static data file has outgrown single-instance deployment.

## Focus

The guide covers inventory, data classification, target schema, extraction/transformation/import boundaries, reconciliation, media migration, cutover, rollback, UI continuity, security, testing and operational handover.

## Start here

Read `SKILL.md` and [`../STANDARDS.md`](../STANDARDS.md). Do not begin a destructive migration without a verified backup, dry-run evidence, record-count reconciliation and documented rollback owner.

## Data integrity statement

Migration tooling must preserve source provenance and report invalid data. It must not silently drop records, invent missing customer/order fields, or move secrets into repository files.
