---
name: emballage-bot-live
description: Build a secure Telegram-driven product-page automation system that gathers structured product data and approved media, validates a finite intake flow, publishes branded pages through an approved deployment pipeline, and routes orders through trusted server endpoints. Use when operators need rapid product-page creation from chat.
---

# Emballage Bot Live — Telegram Product Publishing Operations

This skill turns an authorized Telegram conversation into a reliable product-publishing workflow. The bot is an intake interface; publication, storage, authentication, order creation and notification remain trusted backend responsibilities. Read [`../STANDARDS.md`](../STANDARDS.md) first.

## 1. Operator roles and intake state machine

Authorize operators by immutable user ID and explicit role. Model an intake draft with `draft`, `awaiting_media`, `awaiting_name`, `awaiting_price`, `awaiting_description`, `review`, `publishing`, `published`, `failed`, `cancelled` states. Store draft state durably with expiration; do not rely on process memory when the runtime can restart.

| Input | Validation | Storage rule |
| --- | --- | --- |
| Media | MIME, byte size, dimensions, checksum, operator ownership | Upload once to approved object storage; store object key and metadata. |
| Name | trimmed, bounded, unique/slug-safe check | Generate a canonical slug server-side. |
| Price | integer minor units or exact decimal + selected currency | Never parse display punctuation ambiguously. |
| Description | bounded, sanitized plain/approved rich text | Escape before template render. |
| SKU/availability | unique constraints, enum/state | Server confirms before publish. |
| Publication choice | authorized operator confirmation | Use idempotency key and audit event. |

Every prompt shows current draft summary, validation error, back/cancel affordance and expiry behavior. Avoid emoji-only controls and opaque unexplained states.

## 2. Product, page and media model

Create `operators`, `product_drafts`, `products`, `variants`, `media_assets`, `publish_jobs`, `pages`, `orders`, `notifications` and `activity_events`. A product page derives from structured data and a versioned template; never concatenate unescaped user input into an HTML string. Preserve published page version, product snapshot and media association to support rollback.

## 3. Publishing architecture

The bot writes a validated publish job. A trusted worker/server uses provider credentials to build/render the page, upload assets, deploy through the approved provider API, verify the resulting URL/status and record success/failure. Apply explicit timeouts, retry only safe idempotent steps, and expose a human-readable failure reason to the operator without leaking deployment tokens.

If static generation is used, publish to a separate staging location before promotion. If a database-backed storefront is used, make publication a transactional visibility change after media and data validation. Never let a browser or Telegram client receive deployment credentials.

## 4. Customer order boundary

Published pages send order requests to a server endpoint with typed schema, bot-safe rate limit and validation. The server resolves current product/variant/price/availability, creates an idempotent order/request, stores minimal customer information and triggers notification from the server. Do not let client code call the Telegram Bot API or create an order from hidden DOM price fields.

## 5. Design, analytics and tests

Use a compact product-page system: factual hero/product image, price/availability, description, specification, action, delivery/policy context and accessible contact/order form. Make responsive image loading, 44px targets, focus, errors, unavailable state and confirmation explicit.

Track draft started, draft validation failed, review reached, publish succeeded/failed, page viewed and order requested without analytics secrets/PII. Test interrupted chats, expired drafts, invalid media, duplicate SKU, escaped content, unauthorized operator, deployment failure/retry, order validation, notification retry, page rollback and mobile rendering.
