# Project Documentation Protocol Design

> **Status:** Approved architecture, pending implementation review
>
> **Date:** 2026-09-10
>
> **Purpose:** Define a reusable AI-agent protocol for discovering a software project and creating or maintaining authoritative `PROJECT.md` and `DESIGN.md` files without inventing project truth.

---

## 1. Goal

Create a reusable documentation workflow that can be copied into any software project and used by AI coding agents to understand the project deeply before implementation work.

The workflow must produce two authoritative root-level project files:

- `PROJECT.md` — stable product and business truth, including explicit BRD and PRD sections.
- `DESIGN.md` — the current approved system design, architecture rationale, UI/UX design system, and important technical decisions.

The existing root-level `AGENTS.md` remains the engineering constitution and behavioral baseline for coding agents.

This system is intended to work for frontend, backend, full-stack, mobile, dashboards, APIs, SaaS, e-commerce, internal tools, and other software projects. It should be especially complete for full-stack web projects without forcing irrelevant sections onto other project types.

---

## 2. Final Documentation Architecture

```text
project-root/
├── AGENTS.md
├── PROJECT.md                 # generated/maintained authoritative product + business truth
├── DESIGN.md                  # generated/maintained authoritative system + UX/UI design truth
│
└── docs/
    ├── README.md              # master onboarding and execution protocol
    ├── PROJECT_GUIDE.md       # discovery + interview + generation/update rules for PROJECT.md
    └── DESIGN_GUIDE.md        # discovery + interview + generation/update rules for DESIGN.md
```

The reusable instruction files and the generated authoritative project files must use different names so an AI agent cannot confuse instructions with output.

There must not be a reusable `docs/PROJECT.md` or `docs/DESIGN.md` template that can be mistaken for the actual root-level project truth.

---

## 3. Responsibility of Each File

### 3.1 `AGENTS.md`

`AGENTS.md` is the engineering constitution.

It defines coding-agent behavior, engineering rules, architecture principles, security expectations, testing discipline, implementation workflow, framework guidance, and project-specific override behavior.

It does not replace `PROJECT.md` or `DESIGN.md`.

### 3.2 `docs/README.md`

`docs/README.md` is the mandatory project-documentation entry point.

It must tell the agent:

1. what files to read and in what order
2. how to inspect the repository before asking questions
3. how to separate verified facts from unknown information
4. when the agent must ask the user instead of inferring
5. how approval gates work
6. when to invoke `PROJECT_GUIDE.md`
7. when to invoke `DESIGN_GUIDE.md`
8. how to handle existing `PROJECT.md` and `DESIGN.md`
9. how to validate the generated documents
10. which information must never be placed in these files

### 3.3 `docs/PROJECT_GUIDE.md`

`PROJECT_GUIDE.md` owns the protocol for creating and maintaining `/PROJECT.md`.

It must guide the agent through product and business discovery, BRD discovery, PRD discovery, requirements clarification, user/business-rule clarification, scope confirmation, and approval before write.

### 3.4 `docs/DESIGN_GUIDE.md`

`DESIGN_GUIDE.md` owns the protocol for creating and maintaining `/DESIGN.md`.

It must guide the agent through system-design discovery, architecture reasoning, data/API/security/infrastructure discovery, UI/UX discovery, visual-design-system discovery, technical decision clarification, and approval before write.

### 3.5 `/PROJECT.md`

`PROJECT.md` is authoritative stable product and business truth.

It must not be used as a progress tracker, task tracker, sprint log, roadmap-status board, or implementation-history document.

### 3.6 `/DESIGN.md`

`DESIGN.md` is authoritative current system and design truth.

It describes the approved technical and experience design of the product and the reasoning behind important design decisions.

---

## 4. Core Safety Rule: No Assumptions in Authoritative Files

The agent MUST NOT invent, infer, guess, interpolate, or silently complete missing product, business, design, or architectural facts in `PROJECT.md` or `DESIGN.md`.

A fact may enter an authoritative file only when it is supported by at least one of these sources:

1. direct repository evidence
2. an existing authoritative project document
3. explicit user confirmation

If information is unclear, contradictory, missing, or only probable, the agent must ask the user before including it.

The agent may propose options during the discussion, but a proposal is not project truth until the user approves it.

The final root files must not contain speculative assumptions disguised as facts.

---

## 5. Approval Model

Creating or editing `PROJECT.md` or `DESIGN.md` always requires explicit user approval.

This applies even when the proposed information appears obvious from the repository.

### Required write sequence

1. inspect the project
2. collect verified facts
3. identify missing or conflicting information
4. ask the user focused questions
5. prepare the proposed document or proposed changes
6. show the user what will be written or changed
7. receive explicit approval
8. write the file
9. verify the written result

The agent MUST NOT jump directly from repository inspection to editing either authoritative file.

---

## 6. Project Discovery Workflow

### Phase 1 — Load instructions

Before discovery, the agent must read:

1. root `AGENTS.md`
2. `docs/README.md`
3. the relevant specialist guide
4. any existing root `PROJECT.md`
5. any existing root `DESIGN.md`
6. existing product, architecture, ADR, API, database, UI, and deployment documentation that may contain authoritative information

### Phase 2 — Repository reconnaissance

The agent must inspect the repository before questioning the user.

Relevant evidence may include:

- repository structure
- manifests and lockfiles
- framework/runtime versions
- source modules and feature boundaries
- routes and screens
- configuration files
- environment-variable names without exposing secret values
- database schemas and migrations
- API contracts
- authentication and authorization logic
- integrations
- queues and background jobs
- tests
- deployment configuration
- infrastructure configuration
- design tokens
- component libraries
- CSS/theme configuration
- fonts, icons, assets, and motion libraries
- localization and RTL configuration
- accessibility patterns
- existing README and project documentation

The agent must reuse repository evidence rather than asking the user questions that can be answered confidently by inspection.

### Phase 3 — Fact inventory

Internally, the agent should classify discovered information into three buckets:

- **Verified repository fact** — directly supported by the codebase or an authoritative existing document.
- **User-confirmed fact** — explicitly confirmed by the user.
- **Unresolved** — missing, conflicting, ambiguous, outdated, or dependent on intent.

Only the first two categories may enter the final authoritative files.

### Phase 4 — User interview

The agent must ask only questions that materially improve project truth.

Question rules:

- Ask one focused question at a time by default.
- Tightly coupled factual fields may be grouped when separating them would be artificial.
- Do not ask the user for technical facts already proven by the repository.
- Do not infer business intent from technical implementation.
- When an architectural or design choice is undecided, present realistic options and trade-offs, then ask the user to choose or approve one.
- Resolve contradictions explicitly instead of silently selecting one source.
- Continue until there are no material unknowns required for the requested document.

### Phase 5 — Draft review

Before writing, the agent must present the proposed content or a clear proposed delta when updating an existing file.

The draft must clearly reflect only verified and user-confirmed information.

### Phase 6 — Approval

The agent must receive explicit approval from the user before writing.

Silence, lack of objection, or prior approval of a different document does not count as approval.

### Phase 7 — Write and verify

After approval, the agent writes the root file and verifies:

- the intended sections exist
- no unsupported claims were added
- no approved information was lost
- `PROJECT.md` and `DESIGN.md` do not contradict each other
- relative links and references are valid where practical
- the final file remains focused on durable project truth

---

## 7. `PROJECT.md` Content Model

`PROJECT.md` must focus on stable product and business truth.

Its standard structure should include, when applicable:

### Document control

- project name
- document purpose
- authoritative status
- last materially reviewed date
- ownership or stakeholder authority when known

### Project definition

- executive overview
- product vision
- problem statement
- value proposition
- product goals
- non-goals
- project scope
- out-of-scope boundaries
- key constraints
- project terminology and glossary

### Users and stakeholders

- target users
- user groups/personas when confirmed
- stakeholders
- customer/business actors
- user needs and pain points

### Business Requirements Document — BRD

The BRD section should cover, when applicable:

- business context
- business objectives
- expected business outcomes
- business capabilities
- business stakeholders
- business processes
- business rules
- policies
- compliance or regulatory constraints
- commercial/model constraints when confirmed
- operational constraints
- external business dependencies
- business-level success criteria

### Product Requirements Document — PRD

The PRD section should cover, when applicable:

- product objectives
- target use cases
- product capabilities
- major features
- user journeys
- functional requirements
- non-functional product requirements
- roles and permissions from a product perspective
- data requirements from a product perspective
- validation/business behavior
- notifications and communication requirements
- integrations from a product/business perspective
- localization requirements
- accessibility requirements when product-level
- compatibility/platform requirements
- edge cases and failure expectations that are part of product behavior
- acceptance criteria

### Product domain truth

When useful, include confirmed conceptual entities and relationships such as customer, order, subscription, organization, invoice, product, shipment, or account.

This section must describe business meaning, not database implementation.

### Stable constraints and decisions

Record durable product/business decisions whose rationale materially helps future readers understand the project.

### Exclusions

`PROJECT.md` must not contain:

- sprint status
- implementation percentage
- current tickets
- current branch
- completed-task lists
- temporary debugging state
- day-to-day roadmap execution status
- commit history
- Graphify project-state output

Graphify and project-management tooling should own changing implementation state.

---

## 8. `DESIGN.md` Content Model

`DESIGN.md` must describe the current approved system design and UI/UX design system.

Its standard structure should include, when applicable:

### Design overview

- design purpose
- system context
- design goals
- technical constraints
- quality attributes
- approved architecture summary

### Architecture

- architecture style and rationale
- system boundaries
- major modules/services
- dependency direction
- responsibilities and ownership boundaries
- important runtime flows
- synchronous/asynchronous boundaries
- external systems
- Mermaid diagrams when they genuinely improve understanding

### Architecture decisions

For major decisions, record:

- decision
- context/problem
- considered alternatives where known
- chosen approach
- rationale
- trade-offs
- consequences/constraints

The file should explain both **what** was chosen and **why**.

### Frontend design

When applicable:

- frontend architecture
- route/page structure
- rendering strategy
- feature boundaries
- component architecture
- state ownership
- server-state/data-fetching strategy
- forms and validation architecture
- error/loading/empty states
- localization/RTL approach
- frontend performance principles

### Backend design

When applicable:

- backend architecture
- module/domain boundaries
- transport layer
- application/service layer
- domain/business-rule placement
- persistence layer
- validation boundaries
- error model
- concurrency/transaction behavior
- background work

### API and contracts

When applicable:

- API style
- endpoint/resource organization
- request/response conventions
- validation strategy
- versioning strategy
- pagination/filter/sort conventions
- idempotency rules
- webhook/event contracts
- error-response contract

### Data design

When applicable:

- database technology and rationale
- conceptual and logical data model
- important entities/collections/tables
- relationships
- ownership boundaries
- indexes and performance-sensitive access patterns
- transaction requirements
- migration strategy
- retention or lifecycle constraints
- caching strategy

### Authentication and authorization

When applicable:

- identity model
- authentication mechanism
- session/token model
- authorization model
- roles and permissions
- ownership rules
- trust boundaries
- sensitive operations

### Security and privacy design

When applicable:

- trust boundaries
- input validation
- secrets handling
- sensitive-data handling
- encryption requirements
- abuse/rate-limit protections
- file/upload security
- security headers
- privacy/compliance design constraints

### Integrations

When applicable:

- third-party services
- integration ownership
- failure/retry behavior
- webhook handling
- timeout/idempotency behavior
- external data contracts

### Infrastructure and deployment

When applicable:

- environments
- deployment topology
- hosting/provider architecture
- runtime configuration
- CI/CD design
- storage
- CDN
- queues/workers
- observability
- logging
- monitoring
- backup/recovery
- scaling strategy
- resilience/failure handling

### Testing and quality architecture

When applicable:

- unit boundaries
- integration-test boundaries
- component tests
- end-to-end flows
- contract tests
- security tests
- quality gates

### UI/UX and visual design system

For projects with a user interface, include confirmed design truth such as:

- UX principles
- information architecture
- navigation model
- major user flows
- screen/page relationships
- responsive strategy and breakpoints
- accessibility standards
- visual direction
- typography
- color system
- spacing system
- grid/layout principles
- radius/border/elevation rules
- design tokens
- component system
- form patterns
- table/list patterns
- feedback/status patterns
- empty/loading/error states
- iconography
- imagery/illustration direction
- motion and animation principles
- interaction patterns
- focus/hover/pressed/disabled states
- dark/light theme behavior if applicable
- localization/RTL visual behavior
- content hierarchy and tone where relevant

Major UI/UX decisions should include rationale and trade-offs when that context matters.

### Deliberate trade-offs and constraints

Document important accepted limitations and architectural compromises that future agents must understand before suggesting redesigns.

---

## 9. Universal Adaptation Rules

The guides must adapt to the actual project type.

Examples:

- Backend-only API: omit irrelevant visual-design sections.
- Frontend-only application: do not invent backend/database architecture.
- Mobile application: adapt navigation, platform, lifecycle, offline, and device concerns.
- Full-stack web application: use the complete relevant model.
- Internal dashboard: emphasize roles, workflows, tables, permissions, data operations, and UX states.
- Library/package: focus on purpose, consumers, public API, compatibility, design decisions, and quality requirements.

The agent must not create empty architecture merely to satisfy a template.

If a section is irrelevant, omit it or explicitly state that it is outside project scope only when that fact adds clarity.

---

## 10. Existing-File Update Protocol

`PROJECT.md` and `DESIGN.md` are living authoritative files, but they must not be changed casually.

When one already exists, the agent must:

1. read the complete current file
2. inspect the relevant project changes
3. identify whether a material truth actually changed
4. explain the exact proposed documentation delta
5. ask questions for anything unclear
6. receive explicit user approval
7. edit only the approved material
8. preserve unaffected truth
9. verify internal consistency after the edit

The agent must never regenerate an existing authoritative file from scratch unless the user explicitly approves a full rewrite.

---

## 11. Material Change Rules

### `PROJECT.md` should be reviewed when a material product/business truth changes, such as:

- product vision or problem definition
- target users or stakeholders
- business model or major business process
- project scope
- major feature/capability
- functional requirement
- important non-functional product requirement
- business rule
- role/permission meaning
- compliance requirement
- major user journey
- durable product constraint

### `DESIGN.md` should be reviewed when a material design truth changes, such as:

- architecture style
- major module/service boundaries
- data model or persistence strategy
- authentication/authorization design
- API contract strategy
- critical integration
- deployment/infrastructure topology
- security boundary
- caching/queue/event architecture
- frontend architecture
- UI/UX system
- visual design system
- major responsive/accessibility/motion behavior

### Changes that normally do not require updates

- typo fixes
- small isolated bug fixes
- implementation-status changes
- task completion
- branch changes
- routine refactors that preserve design
- formatting-only changes
- dependency patch updates that do not alter architecture or product behavior

---

## 12. Conflict Handling

If repository implementation, `PROJECT.md`, `DESIGN.md`, user statements, or another authoritative source conflict, the agent must stop and surface the conflict.

The agent must not silently decide which version is correct.

The user must confirm the intended truth before the authoritative project files are changed.

Where product truth and technical implementation differ because implementation is incomplete or incorrect, `PROJECT.md` remains the approved product truth and the implementation should be treated separately as an engineering discrepancy.

---

## 13. Output Quality Rules

Generated authoritative documentation must be:

- specific to the actual project
- concise where possible but complete where necessary
- structured for both humans and AI agents
- free from generic filler
- free from unsupported claims
- free from speculative future architecture
- internally consistent
- explicit about important boundaries and rules
- readable without requiring the reader to reverse-engineer the repository first

Use tables when they improve scanning and comparison.

Use Mermaid diagrams when relationships or flows are materially clearer visually.

Do not duplicate the same truth across many sections without need.

Prefer durable descriptions over implementation trivia.

---

## 14. Relationship to Graphify

Graphify may be used to help inspect repository structure, symbols, relationships, and change impact.

Graphify is not the source of stable business/product truth unless the underlying repository evidence itself proves that truth.

Changing project-state information tracked by Graphify must not be copied into `PROJECT.md` merely to make the document look current.

`PROJECT.md` and `DESIGN.md` describe durable approved truth; Graphify describes the evolving codebase and project state.

---

## 15. Intended Agent Invocation

A user should be able to give a short instruction such as:

> Read the project documentation instructions in `docs/` and initialize or review the project's authoritative documentation.

From there, the agent should know to:

1. read `AGENTS.md`
2. read `docs/README.md`
3. inspect existing `PROJECT.md` and `DESIGN.md`
4. inspect the repository
5. use `PROJECT_GUIDE.md` for product/business discovery
6. use `DESIGN_GUIDE.md` for technical/UI/UX discovery
7. ask the user for every material unknown
8. obtain approval before writing either root file
9. generate or update only the approved authoritative documents

The user should not need to repeat the full workflow in every prompt.

---

## 16. Implementation Scope After Approval

Implementation of this design will create:

- `docs/README.md`
- `docs/PROJECT_GUIDE.md`
- `docs/DESIGN_GUIDE.md`

It will also update the repository root `README.md` so the new reusable documentation workflow appears in the repository structure, documentation map, and recommended AI-agent usage.

The implementation must not create a root `PROJECT.md` or `DESIGN.md` inside the `documentations` repository solely as examples, because those names are reserved for real project-authoritative outputs when the protocol is copied into a project.

The existing root `AGENTS.md` remains independently maintained and is not replaced as part of this protocol implementation.
