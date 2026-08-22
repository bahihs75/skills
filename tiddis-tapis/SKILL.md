---
name: tiddis-tapis
description: Build a luxury rug storefront and custom Firebase-backed administration system with hero storytelling, product search and filters, structured product data, protected operations, and a refined glass-forward visual direction. Use when premium catalog experience and detailed owner control are both required.
---

# Tiddis Tapis Reference Skill

Create an original luxury-rug commerce system with a deliberate public narrative and disciplined product operations. Use a public storefront, focused product detail, search/filtering and order/quote workflow paired with a private admin surface; do not copy reference design or assets.

## Public experience

Build a responsive header, hero sequence, search, category/attribute filters, product grid, product detail, material/size/specification information, focused purchase or quote action, contact and policy views. Keep loading, empty and unavailable-product states explicit.

## Data model

Model products, galleries, variants, categories/hierarchy, attributes, settings, orders, hero content, media and audit events separately. Use stable IDs, visibility, ordering, image alt text, price treatment and stock/availability. Keep product snapshots on orders.

## Firebase pattern

Use Auth for owner identity, Firestore for documents, Storage or approved media hosting for files, and strict rules for public versus owner access. Move sensitive totals, inventory changes and privileged mutations to trusted server functions when possible.

## Verification

Check search/filter composition, product deep linking, modal focus management, Firestore-rule denial paths, mobile behavior, image loading, customer-data boundaries and an admin audit trail.
