---
name: make-ur-kdb
description: Create an original, premium, platform-configurable commerce website and private owner-admin system. Use when a user wants a complete brand storefront, product operations, delivery, checkout, owner controls, and deployment while supplying only brand name, palette, font preference, currency, hosting platform, and data platform.
---

# Make ur KDB — Complete Commerce and Owner-Control Playbook

This skill creates an original KDB-quality commerce system. It combines an editorial storefront, trusted transaction flow, responsive customer experience, private operational console, provider-aware architecture, and rigorous launch controls. It never copies a reference design, codebase, brand identity, image rights, customer data, reviews, ratings, orders, or operational metrics.

Read [`../STANDARDS.md`](../STANDARDS.md) before implementation. Its requirements for system boundaries, data structures, API design, security, UI/UX, mobile behavior, analytics, testing, and complete output are mandatory.

## 1. Collect exactly six inputs

Use one concise form. Once valid values are supplied, begin implementation without asking for a logo, slogan, testimonials, personal credentials, or subjective brand workshop.

| Required input | Acceptance rule | How it changes the system |
| --- | --- | --- |
| Brand name | Any non-empty name | Metadata, public copy, admin labels, email/send templates, accessibility labels, documentation. |
| Color palette | HEX list, named palette, image palette, or concise description | Semantic color tokens; one controlled accent; contrast verification. |
| Preferred font | Valid font name or “none” | Use supplied font when licensable; otherwise use `DM Serif Display` for editorial display and `Manrope` for interface/body. |
| Currency | Symbol or ISO code | Money formatting, receipts, cart, orders, reports, exports. |
| Hosting platform | Explicit provider | Runtime, CI/CD, environment variables, domain, scaling and observability design. |
| Data platform | Explicit provider | Schema/migrations, identity boundary, authorization, storage, backup and recovery strategy. |

If one value is missing, ask only for that value. Treat hosting and data choices as architecture constraints, not cosmetic preferences.

## 2. Architecture selection

Write an architecture decision record covering the selected provider pair. Use the smallest production-safe stack. A public marketing site may be static, but orders, user information, owner changes, inventory, totals, secrets, callbacks, and provider keys must never rely on untrusted client logic.

| Provider pair | Recommended architecture | Mandatory safeguards |
| --- | --- | --- |
| Render + Neon | Typed full-stack application with server APIs, PostgreSQL migrations, object storage for media. | Connection pooling, migration runbook, server-only secrets, backups and health endpoint. |
| Cloudflare + Firebase | Pages/Workers for public/API edge; Firebase Auth/Firestore/Storage for identity/data/media. | Firestore rules, privileged worker/function layer, signed uploads and deploy-time environment checks. |
| Cloudflare + D1/R2 | Worker API, D1 relational data, R2 media and queued jobs when required. | Parameterized queries, migration files, R2 scoped signing, idempotent jobs. |
| Vercel + Supabase | Next.js server routes/actions, Supabase Postgres/Auth/Storage. | RLS per tenant/resource, service-role use only on server, migration review. |
| Firebase Hosting + Firebase | Static/public client plus Auth, Firestore, Storage and Cloud Functions. | Rules as authorization authority, callable/HTTP functions for trusted totals and state changes. |

Create modules for `domain`, `schemas`, `services`, `repositories`, `adapters`, `api`, `ui`, `config`, and `tests`. Keep framework glue at the edge. Use dependency injection or small provider adapters for data, storage, notification and payment integrations.

## 3. Canonical data model

Implement the entities that the selected project needs, with stable IDs, UTC timestamps, actor fields, ownership and explicit state transitions.

| Entity | Core fields | Invariants and indexes |
| --- | --- | --- |
| User | id, identityProviderId, email/phone where supplied, role, status, createdAt | Unique provider ID; role changes audited. |
| Store | id, brandName, currency, settings, ownerId, status | One owner membership minimum; index ownerId. |
| Product | id, storeId, slug, title, description, visibility, categoryId, mediaIds | Unique `(storeId, slug)`; public query index by visibility/category. |
| Variant | id, productId, sku, attributes, priceMinor, compareAtMinor, stockState | Unique SKU; exact integer or decimal money; no browser price authority. |
| Collection/Category | id, storeId, title, slug, sortOrder, visibility | Stable slug and sortable visibility query. |
| MediaAsset | id, storeId, objectKey, URL, alt, width, height, role, approvalState | Object storage only; signed path ownership; no binary database column. |
| Cart | id, userId or anonymousToken, currency, lines, expiresAt | Validate current product/variant availability at checkout. |
| Order | id, storeId, publicCode, customer snapshot, lines snapshot, totals, delivery snapshot, payment status, order status | Immutable line/price snapshot; idempotency unique key; status/date index. |
| DeliveryRule | id, region scope, method, feeMinor, availability, conditions | Server-selected by region/method; effective date optional. |
| ContentBlock | id, storeId, surface, locale, payload, visibility, revision | Sanitized structured content, not executable markup. |
| ActivityEvent | id, storeId, actorId, action, targetType, targetId, before, after, requestId, createdAt | Append-only and indexed by store/date. |

Use maps/dictionaries for keyed UI state and set membership for selected filters or deduplication. Paginate catalogue, media, order and activity lists. Do not load unbounded data into a dashboard or use quadratic list scans for cart/product lookups.

## 4. Public storefront and customer experience

Build the public information architecture intentionally: home, collection/category discovery, search/filter results, product detail, bag, checkout, confirmation, account/orders where the identity model supports it, contact/policies, and helpful not-found/error pages. Use semantic navigation and a skip link. Do not include a public link or marketing reference to the owner console.

Create an editorial visual system from the user’s palette: named color tokens, display/body/mono typography roles, spacing scale, images, component radii, focus state, motion duration, and z-index layers. Use composition variety rather than repetitive equal cards. Public pages should feel spacious and image-led; operational screens should favor calm information density and scannable data.

Every customer surface needs loading, empty, unavailable, validation-error, success and offline/degraded states. Conditional checkout fields must use controlled state: changing a wilaya, delivery type, locale, delivery rule or other dynamic choice must preserve the valid name, phone, selected lines and compatible values already entered. Clear only now-invalid dependent choices, such as a baladiya after its wilaya changes, with a concise explanation. Use visible focus, 44px touch targets, mobile single-column collapse, semantic labels, accurate alt text, `min-height: 100dvh` for view-height sections, and no horizontal overflow.

## 5. Checkout, delivery and trusted totals

First model the order flow as a server-side state machine. On checkout, re-read variants and delivery rules, validate stock and visibility, calculate line totals, discounts, tax if configured, delivery fee and grand total on the server, then write an immutable order snapshot inside a transaction. Use an idempotency key so retries cannot create duplicate orders. After success, clear only the completed cart/draft and render a dedicated confirmation screen or durable route carrying the safe public order code and verified delivery label; do not hide success feedback behind an empty-cart branch.

For Algeria-focused builds, use COD by default unless the user selects another method: full name, phone, all 58 wilayas, Stop Desk or domicile, and a dependent baladiya selector only for domicile. Validate the wilaya/baladiya relationship on the server. Never request unneeded email, free-form address, payment data or user data.

## 6. Private owner control room

Build an unadvertised direct route with real authorization. The owner console must cover Overview, Orders, Delivery, Catalogue, Collections, Content, Hero/Media, Insights, Settings, Activity and Backup/Export. Bind order-status selects and other dynamic admin controls directly after the owner surface renders, or cover the actual delegated event path with an end-to-end test; API unit tests alone do not prove that a rendered control causes its protected mutation. Use a custom brand-specific design, never an imitation of Shopify or a public-template dashboard.

| Console area | Required operations |
| --- | --- |
| Overview | actionable order/status/low-stock/data-quality cues; never fabricated KPIs. |
| Orders | filters, detail, notes, status transition guard, customer and delivery snapshot, export-safe views. |
| Delivery | regions, methods, availability, fees, conditional rules and bulk edits with audit event. |
| Catalogue | product/variant/media/category lifecycle, visibility, stock state, search and pagination. |
| Content | hero, pages, localized blocks, section visibility and revision-aware publishing. |
| Media | upload validation, crop/alt/role metadata, approval, referenced-asset protection. |
| Insights | first-party funnel/operational events, date filters, privacy-safe aggregates. |
| Settings | brand, legal, policies, notification preferences, integrations and store state. |
| Activity/Recovery | append-only changes, scoped export, import validation, backup and rollback procedure. |

## 7. APIs, security, analytics and testing

Version APIs from the first route. Use nouns, typed request/response schemas, resource-scoped authorization, list pagination, allow-listed filtering/sorting, structured errors, rate limits and explicit external-call timeouts. State security rules in the API specification.

Capture privacy-minimal funnel events: view, search, filter, detail view, add-to-bag, begin checkout, validation failure, order created and authorized owner change. Record request IDs and failure categories, not raw secrets, payment data or unnecessary personal data. Define consent behavior before launching analytics.

Test pure totals/state transitions, input validation, data migration, resource ownership, idempotency, stock concurrency, delivery rules, owner actions, mobile checkout, keyboard navigation, upload denial, empty/error states and production build. Deliver exact setup, migration, test, preview, deployment and rollback commands.

## 8. Completion checklist

Before delivery, verify all six inputs are visibly applied; no public admin discovery exists; no secrets or TODO placeholders remain; every domain entity has ownership and lifecycle rules; every API mutation is validated and authorized; conditional forms preserve valid input across re-renders; successful checkout reaches a visible confirmation state; rendered owner controls—not only their endpoints—complete protected mutations; current static client assets are loaded after deploy; desktop and mobile flows are tested; first-party analytics is documented; and deployment/backup/rollback instructions match the selected platforms.
