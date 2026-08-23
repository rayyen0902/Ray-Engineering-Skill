---
name: project-engineering
description: Guide a human and AI coding agent through the lifecycle of a new software project, from idea and requirements through architecture, implementation, testing, release, and maintenance. Use when initializing a project, establishing its engineering documentation system, or determining what should happen next in an AI-first development workflow.
---

# Project Engineering Skill

## Purpose

Turn proven software-engineering practice into an executable workflow that an AI coding agent can guide step by step.

This skill is not a coding style guide and is not a replacement for project documentation. It creates and maintains the project's documentation, decisions, state, tasks, and verification loop.

Core principle:

> Do not optimize for writing code quickly. Optimize for reducing ambiguity before code is written, then make completion objectively verifiable.

## Operating model

The project lifecycle is:

1. Initiate
2. Clarify the problem
3. Define requirements
4. Define scope and acceptance criteria
5. Design architecture
6. Record important decisions
7. Establish implementation rules
8. Plan work
9. Implement
10. Verify
11. Review
12. Release
13. Maintain and evolve

The agent must know which phase the project is in and must not silently skip a phase when skipping would create material risk.

## Required project knowledge

A mature project should maintain these artifacts:

- `README.md` — what the project is
- `AGENTS.md` — how agents must work in this repository
- `PROJECT_STATE.md` — current project state
- `SPEC.md` or a `spec/` directory — what the product/system must do
- `docs/architecture/` — how the system is designed
- `docs/decisions/` — why important decisions were made
- `tasks/` or issue tracker — current executable work
- `tests/` — objective verification
- `CHANGELOG.md` — user-visible evolution

Do not create all artifacts blindly. Create only what the project complexity justifies, but always establish an explicit source of truth for requirements, architecture, state, and verification.

## Source-of-truth rules

When sources conflict:

1. Explicit current user instruction
2. Approved current specification
3. Approved architecture and ADRs
4. Current project state
5. Existing implementation
6. Historical notes

Never treat existing code as automatically authoritative when it contradicts an approved specification or architecture decision.

If a conflict is discovered, stop before making a consequential change and explain the conflict.

## Human approval gates

The agent may draft and analyze freely, but material decisions require human confirmation.

Minimum gates:

- Requirements gate: scope and success criteria confirmed
- Architecture gate: architecture accepted before major implementation
- Change gate: material architecture/scope changes recorded before implementation continues
- Release gate: release criteria satisfied before declaring release-ready

The agent may bypass a gate only when the user explicitly instructs it to do so.

## Phase workflow

### Phase 0 — Initialize

Determine:

- project name
- problem being solved
- intended users
- product/system type
- constraints
- repository state
- existing technology, if any
- desired outcome

Create the minimum project-management structure.

Do not start substantial coding merely because the user described an idea.

### Phase 1 — Clarify

Ask only questions that materially reduce ambiguity.

Classify unknowns as:

- Critical — must resolve before the next gate
- Important — can be resolved during design
- Optional — defer unless needed

Do not interrogate the user unnecessarily.

### Phase 2 — Requirements

Establish:

- goals
- users/actors
- primary use cases
- functional requirements
- non-functional requirements
- constraints
- explicit non-goals
- assumptions
- acceptance criteria

Requirements must be testable where practical.

### Phase 3 — Scope

Separate:

- Must have
- Should have
- Could have
- Out of scope

Break the first implementation target into a small vertical slice whenever possible.

### Phase 4 — Architecture

Define only as much architecture as necessary.

Consider:

- system boundaries
- modules/services
- data model
- interfaces/APIs
- state and data flow
- external dependencies
- security boundaries
- deployment model
- observability
- failure modes
- scaling assumptions

Avoid speculative complexity.

### Phase 5 — Decisions

Create an ADR for decisions that are:

- difficult to reverse
- architecturally significant
- security-relevant
- operationally significant
- likely to be questioned later
- alternatives were seriously considered

An ADR should contain:

- Context
- Decision
- Alternatives
- Consequences
- Status

Do not create ADRs for trivial implementation details.

### Phase 6 — Agent rules

Create or update `AGENTS.md` with repository-specific instructions:

- architecture invariants
- coding conventions
- directory ownership
- test commands
- build commands
- forbidden operations
- generated-file rules
- dependency rules
- migration rules
- review expectations

Keep AGENTS focused on operational rules. Do not turn it into a general project essay.

### Phase 7 — Plan

Convert approved requirements into executable tasks.

Each task should have:

- objective
- scope
- dependencies
- acceptance criteria
- verification method

Prefer small tasks that can be implemented and verified independently.

### Phase 8 — Implement

Before coding:

1. Read applicable `AGENTS.md`
2. Read relevant specification
3. Read relevant architecture/ADR
4. Read `PROJECT_STATE.md`
5. Inspect existing code
6. Confirm task scope

During coding:

- make the smallest coherent change
- preserve architecture invariants
- add/update tests
- update documentation when behavior or design changes

Do not refactor unrelated areas unless required.

### Phase 9 — Verify

Completion requires evidence.

Run the narrowest relevant checks first, then broader checks as appropriate:

- formatter
- linter
- type checker
- unit tests
- integration tests
- end-to-end tests
- build
- security checks

Never claim a task is complete merely because code was written.

### Phase 10 — Review

Review for:

- correctness
- requirements coverage
- regressions
- security
- maintainability
- unnecessary complexity
- documentation consistency
- test adequacy

If the implementation contradicts an approved decision, either fix it or propose a decision change.

### Phase 11 — Release

Before release:

- verify release criteria
- update version if applicable
- update changelog
- verify migrations
- verify configuration
- verify deployment
- verify rollback strategy where relevant
- update project state

### Phase 12 — Maintain

After meaningful work:

- update `PROJECT_STATE.md`
- close or update tasks
- record important decisions
- update affected documentation
- record known limitations
- identify next priority

## Project state protocol

`PROJECT_STATE.md` should be concise and current.

It should answer:

- What phase are we in?
- What is complete?
- What is in progress?
- What is blocked?
- What decisions are pending?
- What known problems exist?
- What is the next highest-priority action?

Do not use it as a historical log. History belongs in Git, changelog, issues, or decision records.

## Change classification

Classify proposed changes:

### Trivial
Examples: typo, formatting, local refactor with no behavior change.

Proceed normally.

### Normal
Examples: feature implementation, bug fix, test changes.

Follow the current task and verification process.

### Material
Examples: API contract changes, schema changes, service-boundary changes, authentication changes, architecture changes, major dependency changes.

Require impact analysis and update relevant specification/ADR/state before or alongside implementation.

### Critical
Examples: security boundary changes, destructive migrations, production data changes, irreversible infrastructure changes.

Require explicit human confirmation before execution.

## Anti-patterns

Never:

- invent requirements
- silently change scope
- treat an old document as current without checking
- rewrite architecture merely because another design looks cleaner
- mark work complete without verification
- create excessive documentation with no operational value
- hide uncertainty
- make destructive changes without explicit authorization
- use memory or chat history as the sole source of project truth

## Completion contract

At the end of a meaningful task, report:

1. What changed
2. Why it changed
3. What was verified
4. What remains uncertain
5. Whether project documentation/state was updated
6. What should happen next

## Bootstrap behavior

When invoked on an empty or poorly documented repository:

1. Inspect the repository.
2. Determine what already exists.
3. Preserve useful existing conventions.
4. Propose the minimum documentation structure.
5. Guide the user through the first unresolved phase.
6. Create artifacts only after gathering enough information.
7. Do not generate speculative architecture or requirements just to fill files.

The goal is not maximum documentation.

The goal is a project whose intent, constraints, decisions, state, and verification are sufficiently explicit that another AI agent can continue the work safely.
