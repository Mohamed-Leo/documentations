# PRD Template — Product Requirements Document

The PRD answers: **What product must exist to satisfy the business/user needs, how should it behave, what qualities must it meet, and how will we know it is correct?**

Keep implementation architecture in technical/design documents unless a choice is a confirmed product/business constraint.

# Product Requirements Document

## 1. Document Control
- Product name
- Version
- Status: Draft / In Review / Approved
- Product owner
- Contributors/reviewers
- Last updated
- Related BRD version

## 2. Product Summary
- One-sentence product definition
- Problem solved
- Primary users/customers
- Core value proposition

## 3. Product Goals and Non-Goals
### Goals
Trace each goal to `BO-###` / `BR-###` where possible.

### Non-goals
Explicitly state what the product/release will not solve.

## 4. Users, Personas, and Roles
| Role / Persona | Primary goals | Key permissions / responsibilities | Priority |
|---|---|---|---|

Separate buyer/customer from end user when applicable.

## 5. User / Stakeholder Requirements
Use `UR-###`.

| ID | User/stakeholder need | Source | Business trace | Priority |
|---|---|---|---|---|

## 6. Product Scope and Release Definition
### MVP / v1
What is required for the first usable/releasable product.

### In scope
Capabilities included in this PRD.

### Out of scope
Explicit exclusions.

### Future / later
Deferred capabilities, not disguised as current requirements.

## 7. Core User Journeys / Use Cases
For each major journey:
- Actor
- Trigger
- Preconditions
- Main flow
- Alternate flows
- Failure/exception paths
- Completion state / outcome

Cover critical off-nominal cases, not only the happy path.

## 8. Feature / Capability Overview
Group requirements by coherent product capability or domain, not by engineering team.

For each capability include:
- Purpose / user value
- Related business/user requirement IDs
- Priority
- Dependencies

## 9. Functional Requirements
Use `FR-###`. One testable behavior per requirement.

Recommended form: **The product shall [observable behavior] [condition/context] [measurable outcome if applicable].**

| ID | Functional requirement | Trace | Priority | Acceptance / verification |
|---|---|---|---|---|

Avoid UI micro-design or technical implementation unless it is required product behavior.

## 10. Business Rules
Restate only rules that product behavior must enforce. Reference the BRD source where possible.

## 11. Roles and Permissions
Define authorization behavior by role, resource, and action. Include ownership, administrative override, delegation, and audit requirements where relevant.

## 12. Data Requirements
Use `DR-###` when material.
- Core entities and relationships at product/domain level
- Data ownership/source of truth
- Required fields or invariants where product-critical
- Import/export
- Retention/deletion
- Audit history
- Sensitive-data classification

Do not replace this with database schema design.

## 13. Integration Requirements
Use `IR-###`.
For each integration define:
- Business/product purpose
- Information/capability exchanged
- Direction
- Dependency criticality
- User-visible failure/fallback behavior
- Required constraints (contract/platform/compliance)

Do not prescribe API internals unless externally contractual.

## 14. Non-Functional Requirements
Use `NFR-###` and measurable targets where possible.

### Performance and scale
Latency, throughput, concurrency, volume, load assumptions.

### Availability and reliability
Availability/SLO, graceful degradation, recovery expectations, RPO/RTO where relevant.

### Security
Authentication, authorization, sensitive actions, session behavior, auditability, abuse controls.

### Privacy
Consent, minimization, retention, deletion, export, residency, third-party handling where applicable.

### Accessibility
Applicable accessibility target/standard and critical assistive-use expectations.

### Compatibility
Platforms, browsers, devices, versions, screen classes, networks.

### Localization
Languages, currencies, dates/numbers, time zones, RTL/LTR, region-specific rules.

### Usability and supportability
Onboarding, errors, recovery, help/support, operator/admin needs.

### Observability
Product-critical logging, audit events, monitoring, alerts, diagnostics.

### Cost constraints
Only when material: per-user/request/session ceilings or budget guardrails.

## 15. States, Edge Cases, and Error Behavior
Capture lifecycle states and exceptional behavior:
- Invalid input
- Duplicate/replayed action
- Partial completion
- Cancellation
- Dependency outage
- Permission loss
- Conflict/concurrency
- Expiration/timeouts
- Recovery/retry
- Fraud/abuse/adversarial use when relevant

## 16. Notifications and Communications
Trigger, audience, channel, required content/purpose, preferences/opt-out, failure behavior.

## 17. Analytics and Telemetry
Define product/business events and metrics needed to evaluate objectives. Avoid implementation-level analytics schema unless required.

## 18. Acceptance Criteria / Product Acceptance
Define launch/readiness conditions and key acceptance criteria. Critical requirements must have an observable verification method.

## 19. Prioritization
Use a clear system such as Must / Should / Could / Won't for this release. Priority does not replace scope.

## 20. Dependencies, Assumptions, Risks
Product-level dependencies and assumptions not already resolved in the BRD.

## 21. Open Questions / TBDs
Never hide unresolved product decisions in prose.

## 22. Traceability Matrix
Recommended for medium/large projects.

| Product requirement | User need | Business requirement / objective | Verification |
|---|---|---|---|
| FR-001 | UR-001 | BR-002 / BO-001 | Test / Demo / Analysis / Inspection |

## 23. Related Artifacts
Link, do not duplicate:
- BRD
- UX research / flows / prototypes
- Design system
- Technical architecture / `DESIGN.md`
- ADRs
- API contracts
- Data model
- Security/threat model
- Delivery roadmap / backlog
