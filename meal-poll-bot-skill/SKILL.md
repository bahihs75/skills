---
name: meal-poll-bot-skill
description: Build a scheduled Telegram meal-poll or attendance-voting bot with signed callbacks, durable vote storage, timezone-safe deadlines, administrative controls, and resilient result delivery. Use when a group needs reliable recurring polls.
---

# Meal Poll Bot Reference Skill

Build recurring or on-demand group polling with the discipline of a small transactional system. Use a database for users, polls and votes; use a durable scheduler/job store; and validate every callback against the message recipient and a signed payload.

## Poll lifecycle

Create a poll with type, label, deadline, target recipients and status. Close conflicting active polls of the same type according to explicit business rules. On closure, freeze voting, compute yes/no/unanswered counts, publish results once and retain the record.

## Callback safety

Encode only the minimum poll/user/choice data plus an HMAC signature. On receipt, validate signature, sender identity, poll status and deadline before writing a vote. Use upsert semantics so a user can revise a vote before closure without creating duplicates.

## Administration

Provide separate admin actions for poll creation, label entry, active-poll result review, deadline revision and subscriber list. Store timezone-aware deadlines in UTC and present them in the configured local timezone.

## Verification

Test forged callback rejection, cross-user button misuse, late voting, duplicate voting, deadline rescheduling, scheduler restart recovery, result idempotency and health-check availability.
