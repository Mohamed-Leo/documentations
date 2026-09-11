# Evaluation Scenarios for `software-brd-prd`

These scenarios test behavior, not exact wording.

## Test 1 — Vague greenfield idea: gaming platform

### Prompt
> I want to build a gaming platform. Make the BRD and PRD.

### Expected behavior
- Skill triggers.
- Agent does **not** invent the platform model, target players, monetization, game types, scope, or success metrics.
- Agent begins a focused discovery interview (3–6 high-value questions).
- Questions cover business goal, target customer/player, product boundary, core value/journeys, MVP, and major constraints.
- Agent keeps BRD and PRD distinct.

### Fail conditions
- Produces a polished “final” BRD/PRD immediately from assumptions.
- Dumps 40+ generic questions at once.
- Chooses tech stack/architecture without being asked or without a binding constraint.

---

## Test 2 — Rich context already exists

### Prompt
> We already discussed the target users, the marketplace model, commission, seller onboarding, payment/refund rules, and MVP scope. Use the skill and create the BRD/PRD.

### Expected behavior
- Agent first extracts existing facts from available context.
- It does not ask the user to repeat known facts.
- It asks only for material gaps.
- It labels any unresolved assumptions/TBDs.
- Requirements trace to business/user needs.

### Fail conditions
- Restarts discovery from zero.
- Treats inferred details as confirmed.

---

## Test 3 — User requests certainty despite missing facts

### Prompt
> Just make the final PRD now. Don’t ask me anything. Decide whatever is missing.

### Expected behavior
- Agent makes a best-effort draft without fabricating facts.
- Unknowns are clearly marked `TBD` / assumptions.
- High-impact gaps prevent the “final” label.
- Document remains useful and structured.

### Fail conditions
- Invents pricing, legal requirements, SLAs, target regions, or business rules as facts.

---

## Test 4 — Technical design contamination

### Prompt
> Our stack is Next.js, Express, MongoDB and Cloudinary. Put the database collections, REST endpoints, folder structure, and deployment architecture into the PRD.

### Expected behavior
- Agent records the named stack only if it is a confirmed constraint.
- It keeps database schemas, endpoints, folder structure, and deployment architecture in technical/design documentation rather than core PRD.
- PRD states product-level capabilities, interface needs, data needs, and quality constraints.

### Fail conditions
- PRD becomes an architecture/design spec.

---

## Test 5 — Weak requirements review

### Input requirements
- “The app should be fast.”
- “The UI must be user-friendly.”
- “The system should scale to lots of users.”
- “Admins can manage users and orders.”

### Expected behavior
- Flags vague/unverifiable language.
- Splits compound requirements when needed.
- Requests/defines measurable targets where known.
- Produces separate requirement IDs and traceability.

---

## Test 6 — Regulated domain

### Prompt
> Create a BRD/PRD for a healthcare appointment and patient-record app.

### Expected behavior
- Compliance/privacy/data-access/safety questions are raised early.
- Agent asks which jurisdictions/standards actually apply instead of assuming.
- Sensitive data, access/audit, consent, retention, recovery, and human/clinical boundaries are considered.

### Fail conditions
- Assumes a specific law applies without location/context.
- Treats security/privacy as generic one-line NFRs.

---

## Test 7 — AI product

### Prompt
> I’m making an AI customer-support copilot for companies. Let’s do BRD and PRD.

### Expected behavior
- Discovery covers buyer vs end user, support workflows, data sources, permissions, human review, quality/evaluation, hallucination/fallback behavior, privacy/retention, model/provider dependency, latency/cost, analytics, and MVP.
- Architecture/model vendor choices are not invented.

---

## Test 8 — Update an existing baseline

### Prompt
> We changed the business model from subscription-only to subscription + transaction fees. Update the BRD and PRD.

### Expected behavior
- Identifies impacted business requirements, goals/metrics, pricing rules, user journeys, billing/payment requirements, analytics, acceptance, and traceability.
- Preserves unaffected stable truth.
- Does not rewrite unrelated sections gratuitously.
- Surfaces downstream decisions that need confirmation.
