# Engineering Documentation & AI Skills Hub

A centralized, evolving knowledge base for **software engineering standards, development workflows, code-quality practices, and reusable AI-agent skills**.

This repository exists to give developers and AI coding agents a consistent starting point across projects. Instead of rediscovering the same engineering decisions, workflows, prompts, quality rules, and product-definition practices in every codebase, the reusable guidance lives here.

> **Start here for engineering work:** [`AGENTS.md`](./AGENTS.md)  
> **Browse reusable AI capabilities:** [`ai-skils/`](./ai-skils)  
> **Git/GitHub workflow:** [`gitHub-workflow/WORKFLOW.md`](./gitHub-workflow/WORKFLOW.md)

---

## Why This Repository Exists

Modern software projects need more than source code. They also need shared rules for how work is discovered, planned, implemented, reviewed, tested, documented, and maintained.

This repository acts as a reusable engineering layer across projects by collecting:

- engineering principles and architecture guidance
- AI-agent operating rules
- frontend and backend development standards
- clean-code and code-quality conventions
- Git and GitHub collaboration workflows
- local quality gates and commit tooling
- repository-navigation and knowledge-graph setup
- reusable AI skills for specialized workflows
- product and requirements-definition skills such as BRD/PRD discovery

The goal is **not** to force one architecture or toolchain onto every project. These documents provide strong defaults that should always be adapted to the target project's actual business requirements, architecture, runtime, security constraints, team practices, and existing conventions.

---

## Repository at a Glance

| Area | Purpose | Use it when... |
| --- | --- | --- |
| [`AGENTS.md`](./AGENTS.md) | Main engineering constitution and AI-agent rules | Starting technical work, architecture, implementation, debugging, refactoring, or review |
| [`ai-skils/`](./ai-skils) | Library of reusable AI skills | A task needs a specialized repeatable workflow, domain process, or agent capability |
| [`GRAPHIFY_AGENT_SETUP.md`](./GRAPHIFY_AGENT_SETUP.md) | Graphify setup and usage | A large repository needs faster structural understanding and agent navigation |
| [`clean-code/`](./clean-code) | Clean-code rules and tooling examples | Configuring ESLint, Prettier, naming, code organization, or frontend conventions |
| [`gitHub-workflow/`](./gitHub-workflow) | GitHub delivery workflow | Creating issues, branches, commits, pull requests, reviews, and merges |
| [`husky/`](./husky) | Local Git quality gates | Setting up Husky, lint-staged, Commitlint, pre-commit, or commit-msg hooks |

---

## Repository Structure

```text
documentations/
├── README.md
├── AGENTS.md
├── GRAPHIFY_AGENT_SETUP.md
│
├── ai-skils/
│   ├── <skill-name>/
│   │   ├── SKILL.md
│   │   ├── references/        # optional supporting knowledge/templates
│   │   ├── tests/             # optional skill validation assets
│   │   └── SOURCES.md         # optional research/source register
│   └── ...                    # reusable skills across many domains
│
├── clean-code/
│   ├── README.md
│   ├── ESLINT_PRETTIER.md
│   ├── GLOBAL.md
│   ├── NEXTRULES.md
│   ├── eslint.config.mjs
│   ├── .prettierrc
│   ├── .vscode/
│   ├── src/
│   ├── package.json
│   └── steps.txt
│
├── gitHub-workflow/
│   └── WORKFLOW.md
│
└── husky/
    ├── README.md
    └── Mind Map.png
```

> The `ai-skils` directory is intentionally shown at a high level because it is a growing skill library. Individual skill packages may contain different supporting files depending on what the skill needs.

---


# Install AI Skills Locally

The `ai-skils/` directory is the source library for reusable AI-agent skills in this repository.  
To make those skills available to local coding agents, install or link them into a shared local skills directory.

> **Recommended local skills directory**
>
> - **Windows:** `%USERPROFILE%\.agents\skills`
> - **macOS / Linux:** `~/.agents/skills`

The exact discovery mechanism still depends on the AI tool you use. Some agents can discover this directory directly, while others may require an explicit configuration entry. Always check the documentation for your agent before assuming automatic discovery.

## Option A — Copy or Sync Skills Locally

This is the safest default for most developers because it keeps the repository and the local agent-skill directory separate.

### Windows PowerShell

From the cloned repository root:

```powershell
$source = Join-Path (Get-Location) "ai-skils"
$destination = Join-Path $env:USERPROFILE ".agents\skills"

New-Item -ItemType Directory -Force -Path $destination | Out-Null
Copy-Item "$source\*" $destination -Recurse -Force
```

### macOS / Linux

From the cloned repository root:

```bash
mkdir -p ~/.agents/skills
cp -R ai-skils/. ~/.agents/skills/
```

This copies each skill package into the shared skills directory.

## Option B — Link the Repository Skills Directory

This is useful for maintainers or developers who want a `git pull` to immediately expose the newest skill definitions without running another copy step.

### Windows PowerShell — Junction

Run PowerShell with permission to create a junction:

```powershell
$repoSkills = (Resolve-Path ".\ai-skils").Path
$agentRoot = Join-Path $env:USERPROFILE ".agents"

New-Item -ItemType Directory -Force -Path $agentRoot | Out-Null
New-Item -ItemType Junction -Path (Join-Path $agentRoot "skills") -Target $repoSkills
```

If `%USERPROFILE%\.agents\skills` already exists, back it up or remove it before creating the junction.

### macOS / Linux — Symlink

```bash
mkdir -p ~/.agents
ln -s "$(pwd)/ai-skils" ~/.agents/skills
```

If `~/.agents/skills` already exists, back it up or remove it before creating the symlink.

## Expected Local Skill Structure

After installation, the local structure should look like:

```text
.agents/
└── skills/
    ├── <skill-name>/
    │   ├── SKILL.md
    │   ├── references/      # optional
    │   ├── tests/           # optional
    │   └── SOURCES.md       # optional
    └── ...
```

`SKILL.md` is the primary entry point for a skill. Supporting files are optional and depend on the workflow.

## Verify the Installation

### Windows PowerShell

```powershell
Get-ChildItem (Join-Path $env:USERPROFILE ".agents\skills")
```

To verify that individual skills contain their primary instruction file:

```powershell
Get-ChildItem (Join-Path $env:USERPROFILE ".agents\skills") -Directory |
  ForEach-Object {
    $skillFile = Join-Path $_.FullName "SKILL.md"
    [PSCustomObject]@{
      Skill = $_.Name
      HasSkillFile = Test-Path $skillFile
    }
  }
```

### macOS / Linux

```bash
find ~/.agents/skills -maxdepth 2 -name SKILL.md -print
```

A correctly installed skill should expose its own `SKILL.md`.

## Keep Skills Updated

If you used the **copy/sync** approach:

```bash
git pull
```

Then run the copy step again.

If you used the **junction/symlink** approach:

```bash
git pull
```

No additional copy is required because the agent directory points to the repository skill library.

## How AI Agents Should Use Installed Skills

Installing skills does not mean an agent should invoke every skill for every task.

A good agent workflow is:

1. Read the current task and project-local instructions first.
2. Inspect the repository before making changes.
3. Identify whether a relevant specialized skill exists.
4. Read that skill's `SKILL.md` before implementation.
5. Follow the skill's required process, checklists, and validation steps.
6. Keep project-specific rules and explicit user requirements higher priority than reusable skills.
7. Use the skill to improve judgment and execution—not to bypass repository context.
8. Verify the result using the target project's own tests, linting, type checks, builds, and runtime checks.

### Important priority rule

Reusable skills are **supporting instructions**, not the highest authority.

Use this order:

1. Explicit user/task requirements.
2. Security, privacy, legal, and data-integrity requirements.
3. Project-specific `AGENTS.md`, `README`, architecture, and business rules.
4. Version-matched official documentation.
5. Relevant local skill instructions.
6. General reusable guidance from this repository.

## Agent Compatibility

This repository intentionally keeps the skill format simple and file-based so it can be adapted to multiple AI coding tools.

Before relying on automatic skill discovery:

- confirm whether your agent supports local skills directly
- confirm the directory it scans
- confirm whether it needs a config file or plugin
- confirm whether it loads skills globally or only per project
- confirm whether skills are loaded automatically or must be explicitly invoked
- prefer documented agent behavior over assumptions

Do not copy tool-specific setup from another agent unless that tool documents compatible behavior.

---

# Core Documentation

## 1. Engineering Constitution — `AGENTS.md`

[`AGENTS.md`](./AGENTS.md) is the primary engineering reference in this repository.

It defines the default operating model for both human developers and AI coding agents, including:

- senior-engineer execution discipline
- repository reconnaissance before implementation
- architecture decision rules
- clean code and naming
- JavaScript and TypeScript
- data structures and algorithms
- frontend architecture
- React and Next.js
- forms, validation, state, and data fetching
- styling and design systems
- accessibility and performance
- frontend testing
- backend architecture
- Node.js, Express, Fastify, PHP, and Laravel
- API design
- authentication and authorization
- application security
- relational and non-relational databases
- PostgreSQL, MySQL, MongoDB, and Redis
- Prisma, Drizzle, and Eloquent
- transactions, migrations, queues, and caching
- logging, observability, configuration, and error handling
- testing strategy and CI/CD
- Git and change management
- documentation standards
- definition of done
- forbidden AI-agent behavior
- technology evaluation and maintenance rules

### How to use it

Use `AGENTS.md` as a **default engineering constitution**, not as permission to overwrite a project's existing architecture.

Before applying a rule, inspect the target repository and determine whether stronger project-specific requirements already exist.

---

## 2. AI Skills Library — `ai-skils/`

[`ai-skils/`](./ai-skils) is a reusable library of specialized instructions and workflows for AI agents.

The purpose of a skill is to make an AI agent perform a repeatable class of work with better structure, consistency, domain understanding, and quality control.

A skill can define:

- when it should be used
- what context must be inspected first
- required discovery or reasoning steps
- workflow stages
- output structure
- quality gates
- templates and references
- validation or test cases
- source material
- common failure modes

### Typical skill structure

```text
ai-skils/<skill-name>/
├── SKILL.md          # primary instructions and workflow
├── SOURCES.md        # optional sources/research
├── references/       # optional templates, checklists, guides
└── tests/            # optional skill behavior/validation tests
```

Not every skill needs every supporting folder. `SKILL.md` is the main entry point for an individual skill.

### Example: Software BRD + PRD

[`ai-skils/software-brd-prd/`](./ai-skils/software-brd-prd) provides a structured requirements workflow for software products and projects.

Its core approach is:

1. **Discover before documenting.**
2. Separate the **BRD** — business problem, value, objectives, constraints, and outcomes — from the **PRD** — users, behavior, product capabilities, requirements, quality attributes, and validation.
3. Track **Confirmed facts, Assumptions, Open decisions, and Unknowns** instead of inventing missing information.
4. Build the BRD before the PRD.
5. Keep requirements traceable using stable IDs such as `BO-###`, `BR-###`, `FR-###`, and `NFR-###`.
6. Validate requirements against explicit quality gates before calling documents final.

This is useful when starting a new software product, defining an MVP, reviewing unclear requirements, or preparing a project before design and implementation.

---

## 3. Graphify Agent Setup

[`GRAPHIFY_AGENT_SETUP.md`](./GRAPHIFY_AGENT_SETUP.md) explains how to use Graphify to create a persistent project knowledge graph that coding agents can query before repeatedly scanning large repositories.

It covers:

- global installation
- project setup
- Codex integration
- local/offline code extraction
- graph refresh after code changes
- repository queries
- dependency/path exploration
- affected-area analysis
- optional semantic extraction

Use it when repository size or complexity makes repeated manual exploration expensive.

---

## 4. Clean Code & Tooling

[`clean-code/`](./clean-code) contains focused engineering notes plus reusable configuration examples.

Important resources include:

- [`clean-code/README.md`](./clean-code/README.md) — broader clean-code and tooling documentation
- [`clean-code/ESLINT_PRETTIER.md`](./clean-code/ESLINT_PRETTIER.md) — ESLint and Prettier guidance
- [`clean-code/GLOBAL.md`](./clean-code/GLOBAL.md) — general coding standards and naming rules
- [`clean-code/NEXTRULES.md`](./clean-code/NEXTRULES.md) — React/Next.js-oriented organization and component rules
- [`clean-code/eslint.config.mjs`](./clean-code/eslint.config.mjs) — example ESLint configuration
- [`clean-code/.prettierrc`](./clean-code/.prettierrc) — example Prettier configuration

Some material in this directory predates the newer repository-wide `AGENTS.md`. When rules conflict, prefer the more current repository-level guidance unless the target project defines a stronger rule.

---

## 5. GitHub Workflow

[`gitHub-workflow/WORKFLOW.md`](./gitHub-workflow/WORKFLOW.md) defines a practical team workflow for delivering work through GitHub.

It covers the lifecycle from task definition to merge, including:

- issue structure
- branch naming
- commit conventions
- pull-request preparation
- code review
- merge requirements
- post-merge maintenance
- common change types and scopes

Use this guide when creating or organizing project tickets and when coordinating work between multiple developers or AI coding agents.

---

## 6. Husky & Local Quality Gates

[`husky/README.md`](./husky/README.md) is a practical setup guide for enforcing development quality before code reaches the remote repository.

It includes:

- Husky
- lint-staged
- ESLint
- Prettier
- Commitlint
- `pre-commit` hooks
- `commit-msg` hooks

The folder also contains [`husky/Mind Map.png`](./husky/Mind%20Map.png) as a visual explanation of the workflow.

---

# How to Use This Repository

## For Developers

A recommended sequence is:

1. Read [`AGENTS.md`](./AGENTS.md) to understand the engineering baseline.
2. Inspect the target project's own README, architecture, package manifests, tests, and local instructions.
3. Use the focused documentation folder that matches the current task.
4. Use an appropriate skill from [`ai-skils/`](./ai-skils) when the task benefits from a repeatable specialized workflow.
5. Adapt reusable guidance to the project's real constraints instead of copying it blindly.
6. Validate the final result using the project's own lint, typecheck, test, build, and runtime checks.

---

## For AI Coding Agents

This repository should improve an agent's judgment, not replace project discovery.

Before making implementation changes, an agent should:

1. understand the user's requested outcome
2. inspect the target repository and its local instructions
3. identify the smallest affected surface
4. reuse existing architecture and patterns where valid
5. load or follow a relevant specialized skill when appropriate
6. preserve business behavior, security boundaries, and compatibility
7. implement the smallest correct maintainable change
8. verify the result with evidence

A reusable rule from this repository should never silently override a stronger project-specific rule.

---

# Instruction Priority

When guidance conflicts, use this practical order:

1. explicit task requirements and acceptance criteria
2. security, privacy, legal, and data-integrity requirements
3. existing business behavior and compatibility guarantees
4. project-specific instructions, architecture, and documentation
5. version-matched official documentation
6. relevant specialized skill instructions
7. this repository's general engineering defaults
8. broader community conventions

This priority keeps reusable guidance useful without allowing it to damage a real project's established behavior.

---

# Repository Philosophy

The common idea behind the documentation and skills is simple:

> **Understand first. Choose deliberately. Change the smallest correct surface. Verify with evidence.**

Good engineering is not measured by the number of abstractions, files, libraries, prompts, agents, or patterns involved.

A good result should be easier to:

- understand
- verify
- test
- secure
- review
- operate
- maintain
- extend

AI should reduce repeated work while preserving engineering judgment—not replace it.

---

# Maintaining This Repository

This is a living knowledge base. Documentation and skills should evolve as tools, frameworks, practices, and project needs change.

When updating it:

- prefer official and version-matched technical documentation
- keep examples clearly identified as examples
- keep project-specific decisions inside the project whenever possible
- update reusable rules only when they are genuinely reusable
- distinguish stable guidance from experimental guidance
- keep skill instructions focused on one recognizable class of work
- add references or tests when a skill becomes complex enough to need them
- avoid duplicated or contradictory rules
- update this root README when the repository structure or major entry points change

---

# Quick Start

Clone the repository:

```bash
git clone https://github.com/Mohamed-Leo/documentations.git
cd documentations
```

Then choose the setup that matches what you need:

1. Read `AGENTS.md` for the engineering baseline.
2. Install or link `ai-skils/` into your local agent skills directory if you want reusable AI workflows available across projects.
3. Use the target project's own instructions and architecture as the primary project context.
4. Open `gitHub-workflow/WORKFLOW.md` when working through issues, branches, pull requests, reviews, and merges.
5. Run the target project's real verification commands before considering work complete.

For general engineering work, begin with:

```text
AGENTS.md
```

For reusable AI workflows, browse:

```text
ai-skils/
```

For local AI-skill setup, see:

```text
Install AI Skills Locally
```

For GitHub collaboration rules, open:

```text
gitHub-workflow/WORKFLOW.md
```

---

## Author

Maintained by [Mohamed-Leo](https://github.com/Mohamed-Leo).

This repository is a public engineering and AI-workflow knowledge base built for reuse, learning, consistency, and continuous improvement across software projects.
