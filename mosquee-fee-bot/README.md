# mosquee-fee-bot

This package guides the implementation of a secure Telegram reimbursement or approval workflow. It is for organizations that need requester intake, reviewer approval, cashier settlement, durable records and an audit trail rather than informal chat-only decisions.

## Included standards

The skill specifies a state machine, roles, PostgreSQL records/indexes, signed callback behavior, webhook security, notification resilience, attachment metadata, exports, analytics, testing and release operations. It treats expense-like data as sensitive and does not use mock financial results.

## Recommended reading order

Read `SKILL.md`, then [`../STANDARDS.md`](../STANDARDS.md). Select deployment and secrets management appropriate to the organization’s approved infrastructure before configuring Telegram.

## Safety boundary

Do not place bot tokens, payment information, request contents or identity data in repositories, browser code, logs or sample responses. A chatbot button does not replace resource-scoped authorization.
