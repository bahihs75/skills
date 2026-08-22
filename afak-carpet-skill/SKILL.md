---
name: afak-carpet-skill
description: Build an original bilingual Arabic/English carpet showroom with sector-led discovery, product/specification content, 58-wilaya and commune quote capture, Firebase CMS, media governance, owner operations, responsive RTL/LTR design, and safe request processing. Use when an Algerian supplier sells projects through quotations.
---

# Afak Carpet — Bilingual Sector Showroom and Quote Operations

This skill builds an original Arabic/English project-sales showroom. It treats language direction, sector qualification, verified material information, quote privacy and owner content management as first-class engineering concerns. Read [`../STANDARDS.md`](../STANDARDS.md) first.

## 1. Bilingual UX and route system

Implement stable Arabic and English routes or locale state for home, sectors, category/product detail, colors/materials, project gallery, specifications, quote request, contact, policies and confirmation. Set document `lang` and `dir` per locale, reverse physical layout only when appropriate, keep numeric units/prices readable and test keyboard traversal in both directions. Do not translate product identifiers in a way that breaks canonical data linking.

Use a sector-first navigation model: mosque, hotels, schools, offices or other verified target spaces. Each sector surface should explain relevant materials/specifications and lead to product or quote action. Use an image-led but restrained design: textured material surfaces, high contrast labels, safe crop ratios, one accent, contextual iconography and factual copy.

## 2. Domain and data structure

| Entity | Required fields | Contract |
| --- | --- | --- |
| LocaleContent | locale, key, text/media payload, revision, publisher | Typed content blocks, not arbitrary executable HTML. |
| Sector | id, localized name/slug, summary, cover media, visibility/order | Drives customer discovery and qualification. |
| ProductFamily | id, sector IDs, localized title/description, materials, quality, colors, specs, visibility | Maintain structured facts separately from long copy. |
| Project | id, sector, localized narrative, approved media, consent status, featured flag | Publish only authorized names/location/media. |
| Wilaya/Commune | canonical code/name/parent relation/version | Client lookup map; server validation source. |
| QuoteRequest | id, contact snapshot, context snapshot, dimensions, location, note, lifecycle, owner | PII-minimal, private, auditable. |
| MediaAsset | id, storage key, alt per locale, crops, rights/approval, dimensions | Lifecycle managed through private CMS. |

Index public locale/visibility/slug, sector/product relationships, quote status/date and activity date. Use sets for selected sectors/facets and maps for normalized lookup—never repeated nested scans.

## 3. Quote workflow and owner CMS

Quote intake collects only relevant information: name, normalized phone, selected sector/product if present, wilaya, commune, dimensions, message and consent if required. Validate fields on client for immediate feedback and on server/functions as final authority. Create a snapshot, set `new` status server-side, attach request ID and rate limit public submission. Use lifecycle `new → qualified → quoted → won | lost | archived`, with reason and activity events.

The owner CMS manages brand settings, locale copy, hero, sectors, product families, specifications, project gallery, requests, media, visibility, policy settings, activity, export and safe restore. Use Firebase Auth, Firestore rules, Storage rules and trusted functions for privileged mutations/notifications. A hidden link is not an access-control strategy.

## 4. Analytics, tests and delivery

Track privacy-minimal locale selection, sector view, product/specification view, quote started/submitted/validation failed and authorized owner action. Do not store raw messages in analytics events. Test Arabic/English direction, localization fallback, location hierarchy, anonymous rules denial, owner writes, request rate limit, media validation, accessibility, mobile forms, offline/degraded content and export scoping.

Deliver environment configuration, Firebase rules/deploy procedure, content seed/revision plan, media storage policy, backup/rollback procedure and no-fabrication statement.
