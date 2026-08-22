---
name: space-wear
description: Build an original industrial-editorial fashion commerce system with a comprehensive custom owner control room, Algeria delivery, catalogue and media governance, activity history, first-party analytics, export/backup controls, and deployable Cloudflare/Firebase/Neon runtime options. Use when a brand needs strong public identity and deep operational control.
---

# Space Wear — Industrial Editorial Commerce and Control Room

This skill creates an original fashion-commerce system with a disciplined public identity and serious operational depth. It combines industrial editorial direction, truthful catalogue behavior, region-aware delivery, private custom administration and deployment parity. Read [`../STANDARDS.md`](../STANDARDS.md) first.

## 1. Choose one visual mode

Choose either **Swiss Industrial Print** or **Tactical Telemetry** and keep it consistent. Swiss Industrial Print uses off-white substrate, dense black type, strict grids, hazard-red accent and poster-like negative space. Tactical Telemetry uses dark charcoal, high-density mono data, technical framing and one purposeful status accent. Do not mix modes, use rounded consumer-card aesthetics, generic neon glow or fake aerospace decoration without operational purpose.

Public fashion surfaces may use strong editorial macro-type, image crops, collection narratives and product detail. Owner surfaces use rigid grid/data rhythm, monospace metadata, visible structural dividers, concise labels and real queue/stock status. Never copy a reference brand’s garment imagery, logo, layout or language.

## 2. Commerce data model

| Entity | Required fields | Operational standard |
| --- | --- | --- |
| Product | id, slug, title, story, category, visibility, media, publish state | Public visibility query and content revision. |
| Variant | id, productId, SKU, size/color, price, stock state, weight/delivery attributes | Unique SKU and server-selected availability. |
| Collection | id, editorial metadata, query/product relation, order, visibility | Supports campaigns without duplicated product truth. |
| DeliveryRule | region, method, fee, threshold, availability, effective window | Evaluated server-side and audited. |
| Order | public code, customer/line/delivery snapshots, total, payment/order state | Idempotent create and immutable commercial snapshot. |
| Content/Hero | surface, asset, copy, locale, schedule, revision, publisher | Content studio with rollback. |
| Media | storage key, role, crop, alt, rights/approval, dimensions | Owner approval before public use. |
| Activity | actor, action, target, before/after, reason, request ID, time | Append-only owner/accountability feed. |

Use indexes for visible catalogue queries, collection order, order queue status/date, low-stock report, delivery rule selection and activity history. Use a set for selected filters/sizes and a keyed map for cart/variant state.

## 3. Public customer experience

Build home, campaign/hero, collection, search/filter, product detail, size/variant selection, bag, checkout, confirmation, policy/contact and account/order history where supported. Clearly show size/variant availability, delivery context, price currency and error states. A filter result must be reflected in URL/state and resettable. Product images must be accessible and responsive; no feature requires a hover-only interaction.

Use a responsive editorial system: mobile prioritizes thumb-friendly browsing and product actions; desktop can use grid tension, image bleed and type contrast. Use 44px touch targets, 65ch prose, `min-height: 100dvh`, no horizontal overflow, keyboard/focus controls, skeletons and concrete empty/error messages.

## 4. Comprehensive owner control room

Create private direct access with real role/owner checks and no public discoverability. Include Access Control, Overview, Hero Studio, Storefront Copy, Catalogue, Collections, Catalogue Behavior Toggles, 58-Wilaya Delivery, Orders, Media Library, Identity/Legal, Consent/Marketing, Reports, Activity and guarded JSON Export/Import/Recovery.

| Area | Required behavior |
| --- | --- |
| Access | Owner/member invite and role lifecycle, session management, sensitive action re-auth where provider supports it. |
| Overview | Real operational queues, low-stock/data quality notes, recent activity, no fabricated KPI cards. |
| Hero/Content | Draft/publish/schedule/revert with locale and media validation. |
| Catalogue | Product/variant lifecycle, stock state, search, visibility, collection relation and media role management. |
| Delivery | 58 wilayas, method/fee/availability, bulk edit, rule conflicts and activity history. |
| Orders | Filter, detail, note, allowed status transition, delivery snapshot, export-safe queue. |
| Media | Signed scoped upload, asset metadata, alt/crop, rights/approval and reference protection. |
| Governance | Legal copy, consent/marketing policy, report date ranges, activity audit and verified backup/restore. |

## 5. Deployment parity, API and observability

Document local development, selected production platform, environment variables, migrations/rules, object storage, scheduled work and background functions. If Cloudflare/Firebase/Neon alternatives exist, keep domain contracts and authorization semantics equivalent while documenting provider-specific wiring. Use typed versioned APIs or server actions, idempotency for create/order actions, timeouts/retries for integrations, request IDs, JSON structured logs and health/readiness checks.

Track consent-aware customer funnel and operational events: discovery, filter, product, variant, bag, checkout, order/request, owner content/catalogue/delivery changes and report generation. Do not record sensitive text/PII in analytics payloads or fabricate traffic/commerce metrics.

## 6. Test and release criteria

Test catalogue visibility, size/variant state, delivery rule selection, 58-wilaya lookup, server totals, stock concurrency, protected admin routes, owner role/tenant checks, media upload/path ownership, content revision rollback, export/import validation, activity immutability, filter deep links, mobile navigation and accessibility. Release with migration backup, provider configuration validation, smoke tests, rollback steps, observability dashboard and incident contact/runbook.
