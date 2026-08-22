---
name: quincadz
description: Build a multi-tenant Next.js marketplace or store-management system with Supabase SSR, authentication, role-aware routes, Algeria location selection, maps, media uploads, customer checkout, and platform administration. Use when customers, merchants, and platform operators need separate workflows.
---

# Quincadz Reference Skill

Create a production-oriented multi-tenant application with clear client, merchant/store and platform-admin boundaries. Use Next.js routing and server-side data access to prevent client roles from becoming only visual differences.

## Route and role model

Separate public/client, store/operator and platform-admin route groups. Enforce roles in server middleware and database policies. Define user, store, membership, category, product, variant, inventory, cart, order, location and upload records before pages.

## Core workflows

Build customer product discovery, cart, direct-order or checkout, order history and profile. Build merchant onboarding, store setup, product/catalogue management, order operations and settings. Build platform administration for users, stores, categories and governance.

## Supabase and maps

Use server-side Supabase clients for privileged operations, Row Level Security for tenant isolation, storage buckets for uploads, and migrations for schema changes. Treat maps/location selectors as user-experience helpers; validate and persist canonical location identifiers server-side.

## Quality baseline

Test role denials, tenant isolation, checkout totals, upload authorization, map/location fallback, loading/error states, Playwright critical journeys, observability/error reporting and responsive admin tables.
