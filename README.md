# Skills Library

This repository is a curated library of **agent-facing skill packages**. It contains one reusable commerce-and-admin builder, `make-ur-kdb`, and one original reference skill for every GitHub repository linked to this workspace. The source repositories were audited as **read-only references**; only this repository has been changed.

## Using the library

Each folder contains a `SKILL.md` with YAML trigger metadata and focused operational instructions. Start with `make-ur-kdb` when you need a complete premium commerce website and bespoke owner console. It asks only for the brand name, color palette, preferred font (or uses the KDB default), currency, hosting platform, and data platform.

The repository-specific skills are focused guides. Use them separately for their domain, or combine them with `make-ur-kdb` when building a larger system. They teach patterns, checks, schemas, workflows, and quality boundaries; they do not copy code, customer data, imagery, secrets, brands, or proprietary content from the source repositories.

## Packages

| Folder | Derived from | Primary use |
| --- | --- | --- |
| [`make-ur-kdb`](./make-ur-kdb/) | KDB/H.B operational model | Premium storefront plus hidden bespoke owner admin, selected hosting/data pair, and COD-ready operations. |
| [`carpet`](./carpet/) | [`Carpet`](https://github.com/bahihs75/Carpet) | Editorial carpet, materials, interior or portfolio storefront design. |
| [`h-b`](./h-b/) | [`H.B`](https://github.com/bahihs75/H.B) | COD-first Algeria checkout, 58 wilayas, baladiya rules and private owner operations. |
| [`msq-afakdeco`](./msq-afakdeco/) | [`MSQ-afakdeco`](https://github.com/bahihs75/MSQ-afakdeco) | Arabic-first contract-carpet quotation showroom. |
| [`mosquee-fee-bot`](./mosquee-fee-bot/) | [`Mosquee_fee_BOT`](https://github.com/bahihs75/Mosquee_fee_BOT) | Auditable Telegram reimbursement and approval workflows. |
| [`tiddis-tapis`](./tiddis-tapis/) | [`Tiddis-tapis`](https://github.com/bahihs75/Tiddis-tapis) | Luxury rug commerce, Firebase content data and protected operations. |
| [`afak-carpet-skill`](./afak-carpet-skill/) | [`afak-carpet`](https://github.com/bahihs75/afak-carpet) | Arabic/English sector showroom, quote requests and Firebase CMS. |
| [`baakbook`](./baakbook/) | [`baakbook`](https://github.com/bahihs75/baakbook) | Safe small-commerce migration and managed-platform cutover. |
| [`emballage-bot-live`](./emballage-bot-live/) | [`emballage-bot-live`](https://github.com/bahihs75/emballage-bot-live) | Secure Telegram product-page automation. |
| [`meal-poll-bot-skill`](./meal-poll-bot-skill/) | [`meal-poll-bot`](https://github.com/bahihs75/meal-poll-bot) | Scheduled signed-callback Telegram polling. |
| [`product-media-library`](./product-media-library/) | [`product`](https://github.com/bahihs75/product) | Raw product-image curation and media governance. |
| [`quincadz`](./quincadz/) | [`quincadz`](https://github.com/bahihs75/quincadz) | Multi-tenant Next.js marketplace, location UX and Supabase controls. |
| [`space-wear`](./space-wear/) | [`space-wear`](https://github.com/bahihs75/space-wear) | Industrial-editorial fashion commerce and deep operational control room. |

## Quality contract

Every package is initialized and validated with the skill-package validator. Skills use lowercase hyphenated directory identifiers so that their metadata remains portable, even when the source repository uses a different capitalization or punctuation.

> The skills require original implementation work. They must never copy reference code, live customer information, credentials, image rights, or brand identity. They also prohibit fabricated customer reviews, ratings, testimonials, financial metrics, stock or order data.

See [`LIBRARY_DESIGN.md`](./LIBRARY_DESIGN.md) for the package taxonomy and `make-ur-kdb` input contract. See [`AUDIT.md`](./AUDIT.md) for a concise record of the read-only reference analysis.
