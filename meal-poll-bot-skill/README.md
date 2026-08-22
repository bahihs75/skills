# meal-poll-bot-skill

This package builds reliable Telegram polls for meal planning, attendance and recurring group decisions. It replaces fragile button messages with durable polls, signed callbacks, scheduling, audit records and idempotent result publication.

## Included requirements

The skill covers relational records/indexes, HMAC callback validation, timezone-safe deadlines, scheduler behavior, participant/admin UX, privacy, analytics, testing, health and recovery operations.

## Implementation path

Read `SKILL.md` with [`../STANDARDS.md`](../STANDARDS.md). Choose a deployment provider with durable database and scheduling support; never use only in-memory timers for production deadlines.
