---
name: msq-afakdeco
description: Build an Arabic-first, bilingual contract-carpet showroom for mosques and institutional projects with sector discovery, price-band/specification presentation, 58-wilaya/commune quote capture, Firebase content operations, and protected owner workflows. Use when project quotation—not simple cart checkout—is the main conversion.
---

# MSQ Afakdeco — Arabic Project-Quotation Showroom

This skill builds an original B2B/B2P carpet showroom for mosque, hospitality, education and institutional projects. It treats Arabic as a first-class language, models project qualification carefully and keeps owner content operations secure. Read [`../STANDARDS.md`](../STANDARDS.md) first.

## 1. Information architecture and UX

Create a bilingual public route model: home, sectors, mosque/mihraab options, institutional surfaces, quality groups, colors, product details, project gallery, specifications, quote request, contact and policies. Persist language in URL, profile or stable local setting; set `lang` and `dir` correctly; reverse layout/icons only where semantic direction requires it. Verify Arabic line height, form alignment, numeric price direction and screen-reader labels.

Use a factual visual language: strong material imagery, clear price-band labels, structured specifications, calm contact actions and sector-specific paths. Do not add fake certifications, client logos, claims, results or testimonials.

## 2. Domain model

| Entity | Fields | Rules |
| --- | --- | --- |
| Sector | id, locale title, slug, hero media, sortOrder, visibility | Shapes discovery and quote qualification. |
| ProductFamily | id, sectorId, qualityGroup, material, width/roll data, color options, priceBand, visibility | Price band is an informative range unless live quoting is supported. |
| ProductMedia | id, familyId, assetId, role, alt per locale, crop | Store original and derivatives separately. |
| Specification | id, familyId, key, value, unit, locale | Structured fields remain filterable/exportable. |
| Wilaya/Commune | canonical code/name/parent relation | Version seed data and validate server-side. |
| QuoteRequest | id, contact snapshot, sector/product snapshot, location, dimensions, notes, status, ownerId | Minimize PII and retain immutable context. |
| ContentRevision | id, surface, locale, payload, revision, publisherId | Supports rollback and editorial audit. |

Index public product/sector visibility, locale/slugs, quote status/date and owner queue. Use a map keyed by wilaya to resolve commune lists; use a set for active facets.

## 3. Quote lifecycle and pricing integrity

Collect name, normalized phone, sector, product context if known, wilaya, commune, dimensions, notes and consent only where needed. Estimate labels must be clearly differentiated from a final quotation. Server code sets initial status such as `new`, validates location hierarchy, sanitizes notes, applies public rate limits, snapshots relevant product data and sends notifications from trusted infrastructure.

Use transitions such as `new → qualified → quoted → won | lost | archived`. Record status reason, actor and timestamp. Never expose quote records publicly and never send unvalidated browser data directly to a spreadsheet, messaging API or mail service.

## 4. Firebase architecture

Use Firestore collections/documents for public content and private requests, Firebase Auth for owner identity, Storage for media, and rules as the authoritative read/write boundary. Keep privileged publishing, notifications, bulk imports and price calculation in Cloud Functions/Workers/server actions. Merge published content with typed defaults to protect a readable public fallback, but do not use a fallback to bypass required authorization.

## 5. Owner workflow and quality

Owner tools manage sectors, product families, specifications, colors, price bands, hero/content blocks, gallery, quote queue, request status, media, legal/brand settings, audit/history and export. Provide list pagination, search, filters, clear empty states and destructive-action confirmation. Test RTL/LTR rendering, anonymous rule denial, owner content update, quote validation, linked location behavior, safe media URL handling, offline/degraded reading and mobile forms.
