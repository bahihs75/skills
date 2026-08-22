---
name: product-media-library
description: Curate a raw product-image repository into a commerce-ready media system with inventory, selection, metadata, accessibility, rights tracking, responsive derivatives, structured storage, safe publishing, and quality control. Use when product media begins as unstructured image files.
---

# Product Media Library — Raw Images to Governed Commerce Assets

This skill turns an unstructured image folder into a reliable media library. It preserves originals, creates approved derivatives, binds assets to truthful product records and prevents unreviewed imagery from becoming production content. Read [`../STANDARDS.md`](../STANDARDS.md) first.

## 1. Inventory and curation workflow

Inventory each file with original filename, checksum, dimensions, aspect ratio, byte size, format, potential product, visible packaging/label, image quality, duplicate group, rights/provenance state and review status. Do not infer ingredients, legal claims, product availability, price, brand ownership or customer consent from pixels alone.

Select explicit roles: `primary_card`, `gallery`, `detail_crop`, `ingredient_or_texture`, `social_share`, `hero`, `archive`. Keep selected and rejected reason metadata. Never overwrite originals; create derivatives from a documented source asset/version.

## 2. Data model and storage

| Record | Key fields | Rule |
| --- | --- | --- |
| Asset | id, original key, checksum, original filename, width/height, MIME, provenance, rights state | Immutable source reference. |
| Derivative | id, sourceAssetId, role, format, width/height, crop, object key, generatedAt | Rebuildable and approval-aware. |
| ProductMediaLink | productId, asset/derivative ID, role, sortOrder, alt, locale, approved | Makes media assignment explicit. |
| Review | id, assetId, reviewer, status, reason, timestamp | Required before production publishing. |
| Collection | id, name, product/media relation, visibility | Supports campaign/season curation. |

Use object storage/CDN for bytes and a database/document store for metadata. Use stable IDs and signed access for private originals. Generate responsive formats according to actual interface breakpoints; avoid publishing local paths or oversized source files to mobile cards.

## 3. Accessibility and visual QA

Write factual alt text that identifies product, packaging, color/material, viewpoint and meaningful visible detail. Do not repeat nearby heading or use “image of.” Mark decorative texture only when it adds no information. Review crop safety, label legibility, contrast on interface surface, hidden personal information, accidental faces, duplicate frames, compression, mobile focal point and loading fallback.

## 4. Publishing and performance

Use a review gate: ingest → metadata → derivatives → product link → visual/accessibility review → approved → published. Serve modern responsive formats with explicit width/height to avoid layout shifts, lazy load below-fold imagery, preload only the actual hero/primary image, and retain a fallback when a CDN object fails. Never create a public asset URL before rights/approval policy allows it.

## 5. Analytics, tests and handover

Track asset usage, broken-media error, primary-image click-through and conversion association only with privacy-safe aggregate analytics. Test duplicate checksum detection, missing alt, invalid MIME, destructive crop prevention, expired signed URL, failed derivative, product-link authorization, responsive `srcset` selection and restore from originals. Deliver asset manifest, naming convention, storage lifecycle, rights policy and review/export procedure.
