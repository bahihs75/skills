---
name: tiddis-tapis
description: Build an original luxury rug storefront and Firebase-backed private administration system with editorial hero storytelling, search, category and attribute filtering, product variants, structured media, secure order or quote workflows, analytics, and responsive product detail. Use when premium catalog discovery and detailed owner control are both required.
---

# Tiddis Tapis — Luxury Rug Commerce and Firebase Operations

This skill creates a high-end rug/catalogue experience where imagery, material data and private operations receive equal engineering attention. It is not a request to copy any luxury design. Read [`../STANDARDS.md`](../STANDARDS.md) first.

## 1. Customer journey

Build a route map for home, collections, search results, filters, product detail, gallery/lightbox, bag or quote sheet, delivery/checkout, confirmation, account/order history where supported, contact and policies. Deep-link product pages by stable slug/ID. Preserve search/filter state in a shareable URL query where applicable. Return a branded accessible not-found state for withdrawn or private products.

Product discovery must offer meaningful filters—collection, color, material, dimensions, price state and availability—not decorative chips. Use debounced search, server/index-backed filtering for large catalogues, pagination or cursor loading, empty results with clear reset and no client-side scan of an unbounded collection.

## 2. Firestore and storage model

| Collection/document | Key fields | Security/query considerations |
| --- | --- | --- |
| products | id, slug, title, visibility, description, categoryIds, mediaIds, displayOrder | Public read only when visible; index visibility/order/category. |
| variants | id, productId, SKU, dimensions, color, material, price, stockState | Owner write; server validates availability/totals. |
| collections | id, slug, title, hero, productIds or query definition, visibility | Public visible query; avoid unbounded product arrays. |
| media | id, storagePath, role, alt, dimensions, crop, approval | Storage rule tied to owner/store; generate URLs safely. |
| content | surface, locale, payload, revision, visibility, publisher | Typed payload and revision history. |
| orders/quotes | id, customer/delivery snapshot, product/price snapshot, state, idempotency key | Public creation via trusted function; owner read/update only. |
| activities | id, actor, action, target, before/after, requestId, createdAt | Owner-only append/event access. |

Use Firebase Auth for identity, Firestore Security Rules for read/write boundary, Storage rules for media, and Cloud Functions/Workers/server actions for stock, totals, notification, imports and privileged updates. Do not expose service credentials in the client.

## 3. Luxury UI system

Choose one controlled atmosphere: quiet premium neutral, archive/dossier, or editorial material study. Define named warm/cool-neutral tokens, one accent, expressive modern display type, readable body sans, mono metadata, photographic color treatment, crop ratios and motion. Avoid generic beige-serif luxury, centered hero clichés, stock testimonials, fake scarcity, purple-blue glows and flat template cards.

Use a distinctive hero, an editorial collection cadence, product cards with factual states, rich gallery and a product detail hierarchy: title, price/quote state, variant selectors, material/specifications, availability, delivery lead time, gallery, action and policy context. Do not make a visual swatch imply stock or an image imply included options without data.

## 4. Owner administration

Implement direct private access and real owner role enforcement. Provide Overview, Product Catalogue, Variants, Collections, Content/Hero, Media, Orders/Quotes, Delivery, Store Settings, Activity, Export/Backup. Use a responsive admin information architecture: data tables/list rows on desktop and detail sheets/stacked summaries on mobile. Show real records and meaningful empty states, not invented KPIs.

## 5. API, events and test plan

Use trusted functions/routes for create-order/quote, owner mutations, upload sign/approval, stock changes and notifications. Enforce request schema, ownership, idempotency, rate limits, request IDs and structured errors. Track consent-aware events for search, filters, detail, gallery, bag/quote start, submit and authorized owner changes.

Test Firestore/Storage rules, visible/private product isolation, deep links, filter combinations, price/stock tampering, unauthorized owner mutations, gallery keyboard focus, upload validation, product snapshot history, content revision rollback, mobile layout and production build.
