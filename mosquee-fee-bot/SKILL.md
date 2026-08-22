---
name: mosquee-fee-bot
description: Build a secure Telegram reimbursement and approval system with registration, role-aware review, cashier settlement, document metadata, durable PostgreSQL data, idempotent notifications, exports, and immutable audit history. Use when money-adjacent requests require traceable multi-party authorization.
---

# Mosquee Fee Bot — Auditable Telegram Approval System

This skill implements a finance-adjacent operating system, not merely a chat flow. It protects request integrity, authorization, auditability and notification reliability while keeping the chat interaction understandable for requesters, reviewers and cashiers. Read [`../STANDARDS.md`](../STANDARDS.md) first.

## 1. Roles and state machine

Define roles explicitly: requester, group administrator/reviewer, cashier, auditor and system operator. Assign role/membership from trusted storage or Telegram group facts; never trust an incoming label or button text.

| State | Permitted actor | Allowed next state | Required evidence |
| --- | --- | --- | --- |
| draft | requester | submitted, cancelled | complete category, amount, description. |
| submitted | requester/admin | admin_review, cancelled | immutable submission version. |
| admin_review | reviewer | revision_requested, approved, rejected | reviewer identity and reason on adverse decision. |
| revision_requested | requester | submitted, cancelled | new version linked to original request. |
| approved | cashier | cashier_review, payment_rejected | approval record. |
| cashier_review | cashier | paid_confirmed, payment_rejected | settlement reference/reason. |
| paid_confirmed | system | closed | payment confirmation metadata. |
| rejected/payment_rejected | reviewer/cashier | closed, revision_requested where policy permits | explicit reason. |

Enforce transitions in a domain service, not a handler branch alone. Record each transition as an append-only event with request ID, actor ID, source message ID, prior/next state, reason and timestamp.

## 2. PostgreSQL data model

Use `users`, `group_memberships`, `roles`, `expense_requests`, `request_versions`, `request_attachments`, `approval_events`, `cashier_actions`, `notifications`, `idempotency_keys` and `audit_events`. Store monetary amounts in integer minor units or exact decimal. Keep attachment bytes in object storage or Telegram file references; persist only metadata and access control data.

Index request status/created time for queues, requester/status for self-service history, reviewer group/status, cashier queue/status, notification delivery state and unique event/idempotency keys. Use foreign keys with deliberate restrict/archive behavior. Use transaction isolation that prevents two reviewers from finalizing incompatible outcomes concurrently.

## 3. Telegram interaction design

Use a finite intake wizard: category → amount → explanation → optional attachment → review → submit. Each prompt must include cancel/back behavior, field validation and the current draft summary. Use compact callback data containing opaque IDs and HMAC signature; verify signature, user ID, state and deadline before mutation. Do not include amounts, roles, secrets or unrestricted JSON in callback payloads.

Use role-specific messages: requester status summary, reviewer decision sheet, cashier settlement control and auditor export entry. Make messages accessible in plain language and avoid emoji-only meaning. If images/documents are allowed, show filename/type/size rather than assuming their contents are valid.

## 4. API, notification and security boundaries

Run a signed Telegram webhook through a public HTTPS endpoint with secret verification. Authenticate operator web tools separately. Use explicit timeouts, retry only safe notification sends with exponential backoff/jitter, and persist delivery attempts so a crash does not duplicate messages. Redact personal/financial data from logs; use request/trace IDs. Never expose bot tokens, database URLs, service-account keys or webhook secrets.

## 5. Reporting, analytics and compliance

Provide date/status/category/group exports with permission checks and generated-at timestamp. Track operational counts such as submitted/reviewed/paid/failed and processing-time percentiles without fabricating financial data or disclosing records to unauthorized actors. Define retention, export/delete policy and local legal/accounting obligations with the organization before launch.

## 6. Tests and release

Test every allowed and forbidden transition, stale/fake callback, cross-user button attempt, concurrent review, duplicate webhook update, revision lineage, attachment authorization, export scoping, notification retry, scheduler recovery, database rollback and cash settlement evidence. Ship migrations, environment-variable table, webhook setup, health check, backup/restore and incident response steps.
