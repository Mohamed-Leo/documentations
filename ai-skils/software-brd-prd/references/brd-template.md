# BRD Template — Business Requirements Document

The BRD answers: **Why does this initiative exist, what business change is needed, who is affected, what outcomes define success, and what boundaries/constraints govern it?**

Do not turn the BRD into a feature specification or architecture document.

# Business Requirements Document

## 1. Document Control
- Product / initiative name
- Version
- Status: Draft / In Review / Approved
- Owner
- Reviewers / approvers
- Last updated

## 2. Executive Summary
A concise explanation of the initiative, business need, intended users/customers, expected value, and desired outcome.

## 3. Business Context
- Current state
- Problem / opportunity statement
- Why now
- Strategic alignment
- Existing alternatives/processes

## 4. Business Goals and Objectives
Use stable IDs.

| ID | Objective | Measure / KPI | Target | Priority |
|---|---|---|---|---|
| BO-001 | ... | ... | ... | ... |

Objectives should be outcomes, not features.

## 5. Stakeholders
| Stakeholder / Group | Role / Interest | Needs / Impact | Decision authority |
|---|---|---|---|

Include sponsor, business owner, customers, users, operations, support, legal/compliance, finance, partners, and other relevant groups.

## 6. Customer / User Context
High-level segments/personas, jobs/goals, pain points, and relevant current behavior. Keep detailed UX/persona research linked rather than bloating the BRD.

## 7. Scope and Boundaries
### In scope
Business capabilities/outcomes included.

### Out of scope
Explicit exclusions for this initiative/release.

### Future considerations
Valuable ideas intentionally deferred.

## 8. Business Requirements
High-level outcomes/capabilities needed by the business.

| ID | Business requirement | Rationale | Source / Stakeholder | Priority | Success evidence |
|---|---|---|---|---|---|
| BR-001 | ... | ... | ... | Must | ... |

Requirements should not prescribe implementation unless the implementation is itself a binding business/contractual constraint.

## 9. Business Rules and Policies
Document decision rules, eligibility, pricing, limits, approvals, ownership, moderation, compliance rules, or other policy-level behavior that shapes the product.

## 10. Business Process / Current-to-Future Change
Where relevant:
- Current workflow summary
- Desired future workflow summary
- Manual vs automated boundaries
- Process owners

## 11. Assumptions
Only explicit assumptions. Each important assumption should have an owner or validation path when possible.

## 12. Constraints
Examples: budget/resource envelope, deadlines, contractual commitments, mandatory platforms, geography, regulatory obligations, legacy dependencies.

## 13. Dependencies
External business, vendor, partner, organizational, or platform dependencies.

## 14. Risks
| Risk | Impact | Likelihood | Mitigation / Response | Owner |
|---|---|---|---|---|

## 15. Cost / Benefit / Value Model
Use only the level of detail appropriate to the project:
- Expected revenue/value/cost savings/risk reduction
- Major cost drivers
- Business case or ROI assumptions

Do not invent figures.

## 16. Success Metrics
Define measurable business outcomes, leading indicators, guardrail metrics, and—when known—baseline and target.

## 17. Transition Requirements
Use `TR-###` for temporary capabilities needed to reach the future state: migration, training, rollout, coexistence, communications, business continuity, etc.

## 18. Open Questions and Decisions
| ID | Question / decision | Impact | Owner | Status |
|---|---|---|---|---|

## 19. Approval / Acceptance
Record who must approve the business baseline and what approval means.
