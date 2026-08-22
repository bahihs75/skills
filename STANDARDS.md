# Shared Professional Standards

Every package in this library must apply the following standards in addition to its domain-specific instructions. The standards are deliberately explicit: a skill is an implementation playbook, not a high-level idea list.

## 1. Discovery and decision record

Begin every implementation with a concise decision record. State the user journey, roles, data sensitivity, chosen deployment/data providers, required integrations, performance constraints, and explicit non-goals. Record material choices such as framework, identity provider, tenancy model, order flow, payment method, delivery model, and media strategy. Prefer the smallest architecture that satisfies the stated requirements, but never omit authorization, validation, data integrity, or observability to keep a project small.

## 2. Domain model and data contracts

Define entities, ownership, state transitions, relationships, identifiers, timestamps, lifecycle rules, and retention policy before rendering screens. Use stable opaque IDs or UUIDs for public APIs, normalized tables/documents for operational records, immutable snapshots for orders/financial-like records, and structured JSON only for bounded flexible fields.

| Concern | Required standard |
| --- | --- |
| Money | Persist integer minor units or exact decimals; never derive totals from display strings or browser values. |
| Lifecycle | Use an explicit enum/state machine with valid transitions and actor authorization. |
| Time | Store UTC timestamps; format only at the interface boundary with locale and timezone awareness. |
| Identity | Separate user, role, membership, tenant/store, and session responsibilities. |
| Referential integrity | Use foreign keys or validated document references; choose delete behavior deliberately. |
| Query design | List expected read paths, then create only the indexes required for those paths. |
| Events/activity | Capture actor, action, target, prior state, next state, request ID, timestamp, and reason where applicable. |
| Media | Store durable object references plus metadata; never keep production binary files inside relational records. |

Select data structures to match access patterns. Use dictionaries/maps for keyed lookup, sets for membership and deduplication, queues for FIFO workflows, heaps for top-k/priority work, arrays/lists for ordered presentation, and database indexes for durable query acceleration. Document non-obvious complexity, avoid repeated linear scans inside loops, paginate unbounded collections, and profile before optimizing.

## 3. Architecture and module boundaries

Use clear boundaries: domain models and pure rules; input/output schemas; application services; repositories/integration adapters; delivery layer (HTTP, worker, bot, UI); configuration; and tests. Entry points wire dependencies but do not contain business logic. Abstract external services behind interfaces where test isolation or provider replacement matters. Put credentials in provider-managed environment configuration and never in browser bundles, source control, examples, logs, or generated pages.

For a full-stack product, organize the system so that public UI, privileged UI, server actions/API routes, business services, persistence, media storage and asynchronous jobs can evolve independently. Keep a dependency direction from interfaces into domain services—not from domain logic into framework or database APIs.

## 4. API, security and resilience

Design versioned resource-oriented APIs. Validate every request at the boundary; return consistent typed success and error envelopes; use precise HTTP semantics; paginate lists; filter/sort from allow-lists; and expose no stack traces, schema internals, secrets, or unscoped customer data.

| Area | Minimum implementation rule |
| --- | --- |
| Authentication | Use a proven provider or library; do not invent a home-grown session protocol. |
| Authorization | Check the caller against the specific resource/tenant/role for every protected operation. |
| Create operations | Use idempotency keys whenever duplicate submission could create an order, request, payment-like record, message, or fulfillment. |
| External calls | Apply explicit connect/read timeouts, bounded retry with jitter only for safe retryable failures, and a defined fallback. |
| Uploads | Validate MIME type, size, dimensions where relevant, storage path ownership and signed access. |
| Abuse controls | Rate-limit public forms and mutation endpoints; record security-relevant failures. |
| Privacy | Collect only necessary data, restrict reads by ownership, and define deletion/export behavior before launch. |

## 5. Web UI/UX design system

Create a project-specific design system before composing pages. Specify purpose-named color tokens, type roles, spacing scale, radius logic, shadows, focus treatment, z-index layers, icon style, imagery rules, motion duration and easing. One accent color should carry active/CTA/focus meaning; maintain a consistent neutral temperature; avoid pure black, generic neon glows, AI-purple gradients, decorative emojis, fake testimonials, fake metrics, arbitrary placeholders, and copied reference identities.

Public websites should use semantic HTML, skip links, descriptive alt text, keyboard-visible focus, readable 65-character text measures, strong contrast, clear current navigation and truthful product/service status. Use asymmetry only when it improves hierarchy. Prefer grid over fragile percentage math, cap layouts around 1200–1440px, use `min-height: 100dvh` rather than `100vh`, and collapse multi-column layouts to a deliberate single-column mobile composition below 768px.

Choose an intentional visual archetype. For premium editorial commerce, use controlled contrast, material imagery, asymmetric composition and broad whitespace. For industrial/admin experiences, use a Swiss-print or tactical-telemetry mode consistently: rigid grids, monospaced operational metadata, clear dividers, objective labels and data density without decorative card clutter. Do not blend unrelated visual languages within one surface.

## 6. Mobile design and responsive behavior

Treat mobile as a designed workflow rather than a reduced desktop. Define the navigation model, safe areas, thumb reach, 44px minimum interactive targets, form keyboard behavior, image crops, text scaling via `clamp()`, loading states and no-horizontal-overflow policy. Preserve the same design system across mobile screens while changing density and composition for the device.

When generating mobile visual references, establish a design bible first: platform mode, type scale, palette, spacing, radius, icon weight, component family, navigation and device framing. Generate one readable screen per step of a flow; do not compress multiple screens into an unreadable collage. Ensure a real sequence such as browse → detail → bag → checkout → confirmation or dashboard → activity → detail.

## 7. States, motion and accessibility

Every interactive unit requires default, hover, focus-visible, active, disabled, loading, empty, success and error considerations. Use skeletons that match final layout rather than generic spinners. Place form labels above inputs, helper text near the field, and specific error text below it. Support `prefers-reduced-motion`; animate only `transform` and `opacity`; use intentional non-linear motion below 300ms for routine interactions; and never animate layout dimensions or bind continuous scroll work directly to scroll events.

## 8. Analytics and experimentation

Define measurement before adding analytics code. Specify event name, actor/anonymous context, object ID, source, timestamp, privacy classification and success/failure outcome. Track meaningful funnel steps—view, search, filter, product/detail view, add-to-bag, begin checkout, validation failure, order/request created, owner status change—without recording raw secrets, full addresses, payment data, or unnecessary personal details. Use a documented consent model where required.

Measure service quality with latency, error rate, queue depth, conversion by funnel stage, order/request state distribution, inventory/data-quality indicators and owner action history. Do not fabricate dashboards, traffic numbers, rankings, testimonials or performance claims. When external traffic intelligence is explicitly requested, save retrieved data immediately, record date range/source, distinguish estimates from first-party data, and state coverage limitations.

## 9. Testing, release and operations

Use a test pyramid: deterministic unit tests for pure rules and state transitions; integration tests for persistence/API/authorization; minimal end-to-end critical paths. Test unhappy paths, retries/idempotency, ownership, concurrent mutations, migrations, mobile layout and accessibility. Run type checks, lint/format checks, build validation and dependency/security checks appropriate to the stack.

Release with reversible migrations, backups before destructive operations, documented environment variables, health/readiness checks, structured logs, request IDs, alert thresholds and rollback instructions. Use feature flags only for genuine staged rollout needs, and remove stale flags after adoption.

## 10. Complete-output standard

For every requested deliverable, create the complete file and every named section. Never leave TODOs, ellipses, placeholder implementation steps, “similar to above” text, fake content, or hidden omissions. Cross-check the original request against the actual file list before delivery and clearly identify any genuine integration credential the user must provide.
