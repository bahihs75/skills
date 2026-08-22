---
name: mosquee-fee-bot
description: Build a Telegram reimbursement or approval bot with user registration, group-admin review, cashier settlement, immutable audit history, document attachments, exports, and a PostgreSQL-backed lifecycle. Use when money-adjacent requests need traceable multi-party approval.
---

# Mosquee Fee Bot Reference Skill

Implement a role-aware Telegram workflow for reimbursements or operational expense requests. Treat financial state transitions as safety-critical: validate data, authorize every action from server-side membership/roles, require reasons for adverse actions, and preserve history.

## Lifecycle

Use a bounded state machine such as `draft → submitted → admin_review → revision_requested | approved → cashier_review → paid_confirmed | payment_rejected → closed`. Permit only role-appropriate transitions. Preserve revisions as linked versions rather than overwriting the original.

## Required controls

Record actor ID, action, timestamp, prior state, next state and mandatory reason where relevant. Support attachment metadata, group-admin review, configurable cashier routing, user-visible status, settled-request export and resilient notification retries.

## Deployment and data

Use PostgreSQL for durable records and object storage or Telegram references for attachments. Use a webhook with a secret token on managed hosting; retain polling only for local development. Never expose credentials or accept payment confirmation from a client-side action.

## Test cases

Test authorization boundaries, forbidden transitions, concurrent reviews, revision history, partial-payment policy if enabled, export filtering, webhook validation and notification failures.
