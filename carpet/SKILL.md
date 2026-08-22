---
name: carpet
description: Design and implement an original premium carpet, interior, material, or portfolio storefront with an editorial visual system, accessible product discovery, truthful quote or commerce conversion, and production-ready data/API boundaries. Use when a material-led brand needs a high-end public experience.
---

# Carpet — Editorial Material Commerce System

This skill creates an original material-led web experience. It combines visual storytelling, product/context discovery, structured content, optional quote or commerce flows, responsive design and durable operational boundaries. Read [`../STANDARDS.md`](../STANDARDS.md) first.

## 1. Product strategy and route model

Define whether the site converts visitors into a purchase, quote request, appointment, sample request or project enquiry. Map routes for home, materials/collections, product catalogue, product detail, projects/interiors, journal or specification resources when required, contact, policy and confirmation. Every route needs a clear next action and a way back.

## 2. Content and data model

| Record | Required fields | Notes |
| --- | --- | --- |
| Material/Product | id, slug, title, summary, long description, type, finish, origin if verified, availability, visibility | Keep unverified claims out of copy. |
| Variant/Specification | id, productId, dimensions, material composition, color, lead time, price/quote state | Separate variant data from descriptive marketing copy. |
| Collection | id, title, slug, concept, image IDs, sort order, visibility | Supports editorial grouping without product duplication. |
| Project | id, title, sector, location only if permitted, narrative, media, featured flag | Do not expose customer/private location data without permission. |
| Media | id, object key, role, crop, alt, width, height, approval state | Preserve original and responsive derivatives separately. |
| Enquiry | id, contact snapshot, product/project context, message, status, owner, timestamps | Validate and rate-limit public submission. |

Use indexes for visible collections, public product slugs and enquiry status/date. Use sets for multi-select filters and maps keyed by ID for local detail state; do not repeatedly scan a large product array to resolve items.

## 3. Visual direction and UI/UX

Treat material and imagery as evidence, not decoration. Choose an editorial archetype such as quiet premium neutral, archive/dossier or studio precision. Build named palette tokens, a distinctive display/body pairing, image aspect-ratio rules and a deliberate spacing scale. Use asymmetric composition, image crops, captions, physical material texture and restrained motion. Avoid generic equal-card rows, stock-looking imagery, neon glows, emoji icons, arbitrary gradients and artificial luxury copy.

Use responsive grids that become one column below 768px. Product cards must communicate price/quote state, material, size/availability and clear activation. Product detail must support gallery navigation, specifications, delivery/lead-time truth, accessible accordions or disclosure, enquiry/purchase action, and unavailable state. All form labels sit above their fields; errors explain exactly what must change.

## 4. Quote and commerce boundaries

When selling, delegate order totals, price, stock, delivery and state transitions to server services. When quoting, collect minimal business-relevant inputs, assign a server-controlled status, record context snapshot, and notify the owner from trusted server code. Do not make a browser call a messaging API with a secret or trust price/product identifiers without verification.

## 5. API, privacy and analytics

Provide versioned endpoints or typed server actions for catalogue queries, enquiry creation and owner operations. Apply allow-listed filters, pagination, validation, resource-scoped owner checks and public rate limits. Track privacy-minimal signals such as collection view, product view, specification download, enquiry start and enquiry submitted. Never create artificial reviews, project claims, client logos or conversion data.

## 6. Testing and delivery

Test responsive image crops, keyboard gallery operation, route deep links, filter reset, empty catalogue, unavailable variants, enquiry validation/rate limit, owner authorization, server-side totals if commerce exists, content fallback and low-network behavior. Provide environment, media-storage, deployment, backup and rollback instructions that match the chosen stack.
