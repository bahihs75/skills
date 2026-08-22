---
name: quincadz
description: Build a production-grade multi-tenant Next.js marketplace or store-management system with Supabase SSR, role-aware routes, tenant-isolated data, Algeria location support, media uploads, catalogue and order workflows, platform governance, analytics, and responsive dashboards. Use when customers, merchants and platform administrators require distinct trusted experiences.
---

# Quincadz — Multi-Tenant Marketplace and Store Operations

This skill builds a marketplace/store platform with real tenancy boundaries. It prevents customer, merchant and platform-admin interfaces from becoming cosmetic variations of one unprotected data layer. Read [`../STANDARDS.md`](../STANDARDS.md) first.

## 1. Tenancy and role architecture

Define `visitor`, `customer`, `merchant_member`, `store_admin`, `platform_support` and `platform_admin` roles based on real membership records. Every store-scoped resource carries `storeId`; every privileged operation verifies membership/role and tenant ownership on the server and through Row Level Security. Use separate public, customer, merchant and platform route groups with server-side access checks before rendering data.

| Surface | Primary jobs | Security boundary |
| --- | --- | --- |
| Public | discover stores/products, search, product detail, policies | Visible/public records only. |
| Customer | cart, checkout/order request, address/location preferences, order history | Own records only. |
| Merchant | onboarding, store settings, catalogue, stock, orders, team membership | Membership + store scope. |
| Platform | merchant approval, category governance, moderation, support, aggregate health | Platform role and audit trail. |

## 2. Supabase/Postgres data model

Use `profiles`, `stores`, `store_memberships`, `categories`, `products`, `variants`, `inventory_movements`, `media_assets`, `carts`, `cart_lines`, `orders`, `order_lines`, `delivery_locations`, `store_delivery_rules`, `notifications`, `analytics_events` and `audit_events`. Choose UUID public identifiers, typed status enums, integer minor-unit money, UTC time and immutable order snapshots.

Indexes should serve public store/product discovery, merchant catalogue/order queues, customer order history, platform approval queue and idempotency lookup. Use constraints for unique slug per store, SKU per store, membership uniqueness, order idempotency and valid foreign keys. RLS policies must express tenant boundary directly; do not rely on hidden UI filters.

## 3. API and server action design

Use typed Next.js server actions or versioned APIs with input schemas, resource authorization, consistent errors and pagination. Mutation endpoints include explicit idempotency for orders, invite acceptance and any external side effect. Resolve price, stock, delivery and merchant/store context on the server. Use provider environment variables, explicit third-party timeouts and structured logs with request IDs.

For location UX, offer Algeria wilaya/commune selectors or maps as convenience, but persist canonical location IDs and validate scope server-side. Do not trust geocoder text alone for delivery eligibility.

## 4. UI/UX and design system

Use one product-wide token system, with a clear distinction between customer shopping surfaces and information-dense merchant/platform workflows. Public pages can be editorial and image-led; merchant pages need tables, filters, summaries and accessible states; platform screens use utilitarian hierarchy and audit visibility. Do not force a permanent left sidebar: choose navigation based on task density and mobile behavior.

Design mobile customer flows deliberately: browse → filter → detail → bag → checkout → confirmation. For merchants, collapse tables into summary rows/detail sheets, preserve filters, provide large touch targets and retain clear destructive-action confirmation. Use loading skeletons, empty states, inline errors, keyboard focus and no fake dashboard data.

## 5. Media, analytics and operations

Use Supabase Storage with scoped paths and signed upload/download rules. Store object keys, alt text, dimensions, role, approval and store ownership. Track privacy-aware events across public discovery, customer conversion, merchant catalogue/order work and platform governance. Segment aggregates by store only where permissions permit; never give one merchant cross-tenant data.

Test RLS as a first-class suite: unauthenticated denial, customer ownership, merchant store isolation, platform-admin scoped allowance, media upload paths, order idempotency, stock race protection, map/location fallback, invitation expiration, pagination, responsive admin layout, migration rollback and production build.
