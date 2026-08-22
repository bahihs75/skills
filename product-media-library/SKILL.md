---
name: product-media-library
description: Curate a raw product-photo repository into commerce-ready media with selection, metadata, accessibility, optimization, structured storage, and safe publishing. Use when a project begins with unstructured product image files rather than a catalog system.
---

# Product Media Library Reference Skill

Turn a raw image collection into a reliable product-media system. Preserve originals, create derivative assets deliberately, and treat naming, alt text, licensing and product association as first-class data.

## Curation workflow

1. Inventory images with filename, dimensions, aspect ratio, file size, visual subject, legibility, duplication risk and quality notes.
2. Group candidates by product and select a primary card image, gallery images, detail crops and social/share crops.
3. Create normalized IDs independent of original filenames; keep the original filename as provenance metadata.
4. Add factual product/packaging alt text. Do not infer ingredients, claims, prices, availability or brand permissions from an image alone.
5. Generate responsive formats and sizes, store originals separately, and publish only approved derivatives through the selected storage/CDN provider.

## Data contract

Store `assetId`, `productId`, `role`, `url`, `width`, `height`, `alt`, `sourceFilename`, `createdAt`, `rightsStatus`, `approved`, and optional tags. Validate URLs and avoid hard-coding local filesystem paths in production UI.

## Quality checks

Review sharpness, exposure, cropped labels, unintended people, sensitive information, duplicate frames, mobile card crop, contrast against page surfaces and accessibility text. Keep uncertain images in review rather than publishing them.
