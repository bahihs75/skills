# Skill Library Design

## Purpose

The library contains one reusable commerce builder and one original reference skill per linked repository. Each package is self-contained, procedural, and designed for an agent rather than a human reader. The reference repositories remain read-only; their implementation is translated into reusable patterns rather than copied.

## Package map

| Folder | Package purpose |
| --- | --- |
| `make-ur-KDB/` | Build a premium commerce website and bespoke owner-admin system from a brand brief and a hosting/data-platform choice. |
| `Carpet/` | Create an editorial carpet or portfolio storefront with robust responsive foundations. |
| `H.B/` | Build a COD-first Algerian commerce flow and bespoke owner control room. |
| `MSQ-afakdeco/` | Build a contract-carpet quote showroom for mosque and institutional spaces. |
| `Mosquee_fee_BOT/` | Build a role-aware Telegram reimbursement and approval workflow. |
| `Tiddis-tapis/` | Build a luxury rug commerce system with Firebase product data and custom operations. |
| `afak-carpet/` | Build a bilingual Arabic/English sector showroom with quote management. |
| `baakbook/` | Design a safe migration path from a small-commerce runtime to managed web/data services. |
| `emballage-bot-live/` | Build a secure Telegram-driven product-page automation workflow. |
| `meal-poll-bot/` | Build a scheduled, signed-callback Telegram voting workflow. |
| `product/` | Curate a raw product-image library into secure commerce-ready media. |
| `quincadz/` | Build a multi-tenant Next.js marketplace with Supabase, location and operational controls. |
| `space-wear/` | Build an industrial-editorial fashion commerce system and deep custom admin. |

## make-ur-KDB input contract

Ask the user only for the following six inputs, and do not add discovery questions unless one input is genuinely invalid or missing:

| Input | Required behavior |
| --- | --- |
| Brand name | Use in navigation, metadata, owner workspace, transactional copy, and documentation. |
| Color palette | Accept HEX values, named colors, image palette, or a descriptive palette. Confirm readable contrast. |
| Font preference | Apply the stated font; otherwise use the KDB default pairing: `DM Serif Display` for display and `Manrope` for interface/body. |
| Currency | Use the requested currency symbol/code in product, order and operational displays. |
| Hosting platform | Accept a user-selected host such as Render, Cloudflare, Vercel, Firebase Hosting, or another named platform. |
| Data platform | Accept a user-selected store such as Neon, Firebase, Supabase, Cloudflare D1, PostgreSQL, or another named platform. |

Default product behavior is a premium original storefront and a separate internal owner console. For Algeria, use COD-only checkout, 58 wilayas and dependent baladiyas; for another market, ask the user to provide or approve the delivery geography before launch.

## Shared quality baseline

Every generated commerce implementation must use original design, no fabricated customer reviews or ratings, server-authoritative totals and inventory, role-protected administration, safe data schemas, accessible keyboard flows, responsive verification, automated tests, and deployment documentation appropriate to the selected platform.

## Documentation plan

The repository root will carry `README.md` in English and `README.ar.md` in Arabic. Each skill itself remains concise and agent-facing: a `SKILL.md` with frontmatter and a focused `references/` directory only where extra detail is needed.
