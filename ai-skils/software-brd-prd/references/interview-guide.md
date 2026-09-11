# Discovery Interview Guide

Use this as a question bank, not a script. Ask only what is relevant and unanswered. Prefer 3–6 questions per turn, then summarize what changed.

## Stage 0 — Existing context
Before asking anything:
- Read the current conversation, project docs, repository context, research, and prior decisions available to you.
- Extract known facts and contradictions.
- Do not ask the user to repeat known information.

## Stage 1 — Business foundation
Establish why the product should exist.
- What problem/opportunity is being addressed?
- Who owns/sponsors the initiative?
- What happens today without the product? What pain, cost, risk, or lost opportunity exists?
- What business outcomes should change?
- How will success be measured? Which metrics/KPIs matter and what targets are expected?
- Is this a commercial product, internal system, client project, platform, or experiment?
- What deadlines, budget/resource constraints, contracts, or strategic commitments are real?

## Stage 2 — Market, customer, and users
- Who is the buyer/customer? Who are the actual end users? Are they different?
- Which primary user segments/personas matter first?
- What jobs, goals, frustrations, and current alternatives do they have?
- What regions/languages/device contexts matter?
- What competitors or substitute workflows exist, and what must be meaningfully better/different?

## Stage 3 — Scope and product boundary
- What is the product in one sentence?
- What absolutely must exist in v1/MVP?
- What is explicitly out of scope?
- What may belong to later releases?
- What external systems, teams, or manual processes remain outside the product boundary?
- Is this greenfield, replacement, migration, extension, or modernization?

## Stage 4 — Actors, roles, and core journeys
- Which roles/actors exist (guest, user, admin, operator, vendor, moderator, etc.)?
- What are the top end-to-end journeys for each primary actor?
- What starts and completes each journey?
- What approvals, states, lifecycle transitions, notifications, or exceptions exist?
- What should happen when something fails, is invalid, unavailable, duplicated, cancelled, or disputed?

## Stage 5 — Business rules and monetization
Ask when relevant:
- Pricing/subscription/commission/transaction model?
- Eligibility, limits, quotas, scoring, ranking, rewards, refunds, fees, promotions, ownership, moderation, or dispute rules?
- Which rules are policy/business decisions versus implementation details?
- Which rules vary by region, tenant, plan, or user type?

## Stage 6 — Data and content
- What core entities/data does the product manage?
- Who creates, owns, edits, views, exports, deletes, or retains that data?
- What data is sensitive/personal/regulated?
- What import/export, migration, audit history, retention, deletion, backup, or recovery needs exist?
- What content/media types are supported?

## Stage 7 — Integrations and ecosystem
- Which third-party services or internal systems must integrate?
- Is the product itself exposing APIs/webhooks/SDKs?
- What happens if dependencies are degraded or unavailable?
- Which identity, payments, messaging, maps, storage, analytics, game services, AI models, or other providers are mandatory constraints versus replaceable options?

## Stage 8 — Quality attributes / NFR discovery
Turn adjectives into measurable targets where possible.
- Performance/latency/throughput/concurrency/scale
- Availability/reliability/recovery/backup
- Security/authentication/authorization/auditability
- Privacy/data residency/retention
- Accessibility
- Browser/device/platform compatibility
- Localization/time zones/currencies
- Usability/onboarding/supportability
- Observability/logging/monitoring
- Offline/poor-network behavior when relevant
- Cost/usage ceilings when operational cost is material

## Stage 9 — Compliance, safety, and domain rules
Ask early for regulated or high-risk products.
- Which laws, regulations, standards, contractual requirements, app-store/platform policies, age rules, content rules, financial/health/privacy obligations, or regional restrictions apply?
- Is human review required anywhere?
- What abuse, fraud, safety, moderation, or trust risks must the product control?

## Stage 10 — Analytics and acceptance
- What product events/metrics must be observable?
- What defines activation, engagement, conversion, retention, completion, or success?
- What business/product conditions make v1 acceptable for launch?
- Which requirements are Must/Should/Could/Won't for the current release?

## Stage 11 — Transition and operations
For replacements/internal/enterprise products:
- Is data migration required?
- Is user/admin training required?
- Does rollout need pilot, phased migration, coexistence, or rollback?
- What support/operations ownership is required after launch?

# Domain lenses

Apply only the relevant lens.

## SaaS / multi-tenant
Tenancy boundaries, organizations/workspaces, roles, plans/entitlements, billing, quotas, admin controls, data isolation, onboarding/offboarding, auditability.

## Marketplace / commerce
Buyer/seller roles, catalog/inventory, search/discovery, checkout, payment, fees, fulfillment, returns/refunds, disputes, ratings/reviews, fraud, tax, moderation.

## Gaming platform
Player identity/profile, matchmaking/lobbies, game/session lifecycle, progression/rewards, inventory/economy, social/community, leaderboards, anti-cheat/abuse, moderation, parental/age controls where applicable, platform/device support, latency/availability, monetization, live-ops, telemetry.

## AI product
Model/provider dependency, input/output boundaries, grounding/data sources, quality metrics, latency/cost, fallback behavior, human review, safety/abuse, prompt/data privacy, retention, evaluations, explainability where required.

## Fintech / payments
Money movement lifecycle, authorization/capture/refund, ledger/source of truth, reconciliation, fraud/risk, limits, KYC/AML where applicable, audit trail, failure/idempotency, regulatory and security constraints.

## Healthcare
Clinical vs administrative use, sensitive data boundaries, consent, access/audit, safety, data retention, interoperability, regulatory requirements, human oversight.

## Internal business system
Current workflow, process owners, approvals, exception handling, permissions, reporting, import/export, legacy migration, audit, training, operational continuity.

## Mobile / offline-first
Supported OS/device range, permissions, offline behavior, sync/conflict rules, push notifications, background work, connectivity degradation, battery/storage constraints, app-store requirements.
