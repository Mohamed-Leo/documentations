# BRD / PRD Quality Gates

Run these checks before calling a BRD/PRD ready or final.

## Gate 1 — Business clarity
Pass only if:
- The problem/opportunity is explicit.
- Business objectives are outcomes, not disguised features.
- Success has measurable evidence or is explicitly marked TBD.
- Stakeholders and affected users are identified.
- Scope and out-of-scope boundaries are clear.
- Major business rules, constraints, dependencies, assumptions, and risks are visible.

## Gate 2 — BRD / PRD separation
- BRD explains why, business outcomes, business boundaries, and high-level required capabilities.
- PRD explains product users, behavior, functions, quality attributes, and acceptance.
- Architecture/framework/database/API implementation choices are not mixed in unless they are binding constraints.
- Sprint status, tickets, and temporary progress notes are absent.

## Gate 3 — Requirement quality
For every material requirement ask:
1. **Necessary** — What higher-level objective/need requires this?
2. **Singular** — Is it exactly one requirement rather than multiple joined behaviors?
3. **Clear** — Could two reasonable readers interpret it differently?
4. **Unambiguous** — Are undefined pronouns, vague qualifiers, or overloaded terms present?
5. **Measurable / verifiable** — Can test, demonstration, analysis, or inspection prove it?
6. **Feasible** — Is there a known reason it cannot realistically be met? If feasibility is unknown, flag it rather than guessing.
7. **Traceable** — Is its source/parent need known?
8. **Implementation-neutral** — Does it say what is required rather than how to build it, unless the “how” is a true constraint?
9. **Consistent** — Does it conflict with another requirement, rule, scope statement, or assumption?
10. **Bounded** — Where ranges/limits matter, are they defined?

## Gate 4 — Vague-language scan
Rewrite or quantify terms such as:
- fast / quickly
- scalable
- secure
- user-friendly / easy / intuitive
- robust
- flexible
- reliable
- seamless
- high-performance
- real-time
- large / small
- sufficient / adequate
- as needed / where appropriate

If the user cannot yet define a measurable target, keep the requirement but mark the target `TBD` and record the decision required.

## Gate 5 — Coverage
Check relevant categories; do not force irrelevant ones:
- Functional behavior
- Roles/permissions
- Data lifecycle
- Integrations/interfaces
- Security/privacy
- Performance/scale
- Availability/recovery
- Accessibility
- Localization
- Compatibility
- Error/edge/adverse behavior
- Analytics/telemetry
- Domain/compliance rules
- Migration/training/transition
- Support/operations

## Gate 6 — Traceability
For medium/large products:
- Every Must-have product requirement traces upward.
- Every primary business objective has product coverage or an explicit reason it does not.
- Orphan requirements are challenged.
- Conflicting requirements are resolved or listed as open decisions.

## Gate 7 — MVP integrity
- MVP is a coherent usable outcome, not merely a random subset of features.
- Must-haves are genuinely required for the defined launch outcome.
- Deferred features are explicit.
- Out-of-scope items are explicit enough to prevent scope creep.

## Gate 8 — Assumption hygiene
- Assumptions are not presented as confirmed facts.
- High-risk assumptions have a validation path where possible.
- Unknowns are not silently filled by the agent.

## Gate 9 — Acceptance readiness
- Critical functional requirements have observable acceptance/verification.
- Critical NFRs have targets or explicit TBD decisions.
- Launch/readiness criteria are defined at the product level.

## Readiness result
Use one of:
- **Ready for approval** — no high-impact gaps.
- **Conditionally ready** — only low/medium-impact TBDs remain and are explicitly owned.
- **Not ready** — unresolved high-impact decisions could materially change scope, product behavior, compliance, or success criteria.
