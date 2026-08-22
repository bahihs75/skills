---
name: meal-poll-bot-skill
description: Build a scheduled Telegram meal-poll, attendance, or group-voting bot with signed callback payloads, durable relational storage, timezone-safe deadlines, idempotent result delivery, administrator controls, and resilient scheduled jobs. Use when a group needs reliable recurring polls.
---

# Meal Poll Bot — Signed, Scheduled Group Voting

This skill creates a dependable group-poll system rather than a loose message with buttons. It supports recurring meal/attendance choices, clear deadlines, correction before closure, auditable results and resilient restart behavior. Read [`../STANDARDS.md`](../STANDARDS.md) first.

## 1. Domain model and lifecycle

Use `users`, `groups`, `group_memberships`, `poll_templates`, `polls`, `poll_options`, `votes`, `scheduled_jobs`, `delivery_attempts`, `admin_actions` and `audit_events`. Store deadline UTC plus configured group timezone. Define states `draft`, `scheduled`, `open`, `closing`, `closed`, `delivery_failed`, `cancelled` with one authoritative service controlling state transitions.

Use a unique `(pollId, voterId)` constraint so a revision upserts one vote rather than creating duplicates. Use an index on `poll status + deadline` for closure jobs, `group + open state` for active poll discovery, and notification delivery idempotency keys. Use maps for option lookup and sets for recipient deduplication.

## 2. Callback design and integrity

Callback payloads include an opaque poll ID, option ID, intended user/group context and short HMAC signature. Verify HMAC with server secret, match Telegram actor to intended eligibility, check poll is open and deadline has not passed, then write vote in a transaction. Reject forwarded/stale/tampered callbacks with a direct explanation. Never place all poll data, role status or secrets in callback data.

## 3. Scheduler and notifications

Use a durable scheduler/queue or provider-native scheduled function. The scheduler must tolerate restarts, use explicit lease/locking for a closing job, and invoke idempotent close/deliver operations. On closure, freeze votes, calculate totals from the database, persist result snapshot and send results once per intended destination. Retry send failures with bounded backoff/jitter; persist attempts and surface administrative remediation.

## 4. Admin and participant UX

Participant flow is concise: invitation, vote choice, confirmation/current selection, optional change before deadline, closed result. Admin flow includes create ad-hoc poll, schedule recurring template, set label/options/deadline/timezone, inspect active poll, manually close/cancel according to policy and view export-safe aggregate results. Use clear text and icon support, keyboard-accessible fallback where a web console exists, and localized timezone formatting.

## 5. Privacy, analytics and verification

Collect only Telegram identity/group data required for membership and votes. Define retention/deletion policy for personal participation records. Track poll created/opened, vote submitted/revised/rejected, close executed, notification delivered/failed and job latency without publishing individual vote detail where privacy policy prohibits it.

Test signature rejection, wrong-user/wrong-group callback, deadline passage, duplicate/revised vote, concurrent close/vote, job restart, delivery retry, timezone/DST conversion, admin authorization, export scoping and health check.
