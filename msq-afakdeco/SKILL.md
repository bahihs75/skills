---
name: msq-afakdeco
description: Build an Arabic-first contract-carpet quotation showroom for mosques and institutional spaces with Firebase content management, sector browsing, price bands, 58-wilaya location data, and safe quote operations. Use when the sales motion is project quotation rather than cart checkout.
---

# MSQ Afakdeco Reference Skill

Use this skill for made-to-measure carpet, mosque, hotel, school or large-space projects. Build a factual Arabic-first showroom that guides visitors from sector to specification to quote request, with an editable Firebase content model.

## Public model

Separate mosque/mihraab and institutional-surface discovery. Support quality groups, color taxonomy, price-per-square-metre bands, specifications, galleries and WhatsApp/contact actions. Use Arabic names and formatting as first-class data; make RTL intentional.

## Quote workflow

Collect name, normalized phone, project sector, product context where present, wilaya, commune, dimensions/project notes and only the information needed for a meaningful quote. Store a bounded schema with a server-controlled initial status. Make spreadsheet/webhook forwarding secondary and non-blocking.

## Firebase content pattern

Keep managed site content in a versioned document with defaults/merge behavior and offline read fallback. Store quote requests separately. Use Firebase Authentication and rules as the authorization boundary.

## Completion standard

Verify RTL/LTR reading order, price labels, linked wilaya/commune data, offline states, authenticated content updates, request status workflow and image URL safety.
