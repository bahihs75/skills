---
name: make-ur-kdb
description: Build an original premium KDB-style commerce website and bespoke owner-admin system. Use when a user wants a complete storefront with catalog, delivery, checkout, operations, and an internal admin panel while choosing only brand name, palette, font, currency, hosting platform, and data platform.
---

# Make ur KDB

Create a premium, original commerce system with a public storefront and a separate, protected owner console. Preserve the functional rigor of KDB: editorial product discovery, server-authoritative commerce, COD-ready delivery, content governance, catalogue operations, and no public discovery of the admin route.

## Collect exactly six inputs

Ask for the following values in one compact form. Do not add discovery questions after receiving valid answers.

| Input | Required handling |
| --- | --- |
| Brand name | Apply to product copy, metadata, navigation, owner console, and documentation. |
| Color palette | Accept HEX values, names, an image palette, or a description; verify readable contrast. |
| Preferred font | Use it if supplied; otherwise use `DM Serif Display` for display and `Manrope` for interface/body. |
| Currency | Use the requested symbol/code in pricing, totals, reports, and exports. |
| Hosting platform | Use the chosen provider, such as Render, Cloudflare, Vercel or Firebase Hosting. |
| Data platform | Use the chosen store, such as Neon, Firebase, Supabase, Cloudflare D1 or PostgreSQL. |

If one required value is missing, request only that value. Do not request logos, testimonials, personal credentials, or extra marketing inputs before scaffolding.

## Delivery workflow

1. Translate palette and typography into a compact token system before composing UI.
2. Select a framework that fits the chosen hosting/data pair; define products, variants, stock, categories, collections, media, delivery rules, orders, activity and roles before screens.
3. Build public home, discovery, category/collection browsing, product detail, bag, checkout, confirmation, account/order history where supported, contact, policy and responsive navigation.
4. Build a protected owner console for overview, orders, delivery, catalogue, collections, content, hero/media, insights, settings, activity and recovery. Never expose an admin link in public UI.
5. Implement the selected payment/delivery contract. For Algeria-focused KDB work, default to COD, all 58 wilayas, Stop Desk or domicile, and baladiya only for domicile.
6. Calculate prices, stock, delivery and status transitions on the server. Treat browser values as untrusted.
7. Test checkout, protected operations, invalid inputs, desktop/mobile layouts, and the selected deployment configuration. Document secrets without committing them.

## Owner-console baseline

Include operational overview, order lifecycle/notes, delivery matrix, products/variants, collections/categories, content/hero management, media, analytics/low-stock signals, store controls, activity audit and export/backup safeguards unless the selected platform makes one inapplicable.

Use an original brand-specific visual language. Do not copy an external administration product or a reference brand’s UI.

## Safety and trust rules

- Never fabricate customer reviews, ratings, testimonials, completed orders, inventory, financial results, or identities.
- Keep owner access private and protected by the production identity system or securely configured secret.
- Validate API inputs, escape rendered content, restrict URLs/uploads, enforce authorization server-side, and protect customer data from public reads.
- Preserve sensitive operational changes in an activity record where the selected data platform supports it.

## Platform decisions

Read `references/platform-recipes.md` after the user selects the hosting/data pair. Use it as an integration guide, never as a reason to override the user’s selected services.

## Completion standard

Deliver an original responsive, tested system with deployment documentation in the user’s requested language. Report selected stack, public/owner capabilities, security controls, tests, and any required credentials.
