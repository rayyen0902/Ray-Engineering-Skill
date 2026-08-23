---
name: ray-engineering-skill
description: Guide a human and AI coding agent through the lifecycle of a software project, from idea and requirements through architecture, implementation, testing, release, and maintenance. Use when initializing a project, establishing its engineering documentation system, or determining what should happen next in an AI-first development workflow.
---

# Ray Engineering Skill

## Purpose

Turn proven software-engineering practice into an executable workflow that an AI coding agent can guide step by step.

This skill is not a coding style guide and is not a replacement for project documentation. It creates and maintains the project's documentation, decisions, state, tasks, and verification loop.

Core principle:

> Do not optimize for writing code quickly. Optimize for reducing ambiguity before code is written, then make completion objectively verifiable.

## How to use this skill

This file is the routing and policy layer. It defines principles, gates, phase order, and conflicts. It is not the step-by-step procedure source.

- Execution procedures live in `workflows/`.
- Pass/fail gate criteria live in `checklists/`.
- Artifact skeletons live in `templates/`.

Internal conflict rule:

- For principles and approval gates, this file wins.
- For procedure order, the routed workflow wins.
- For artifact format, the routed template wins.
- For gate pass criteria, the routed checklist wins.

If a detail file contradicts a principle or gate in this file, stop before consequential changes and report the conflict.

## Lifecycle

The project lifecycle has 13 phases. Phases may move backward when later work exposes an earlier gap; when moving backward, update `PROJECT_STATE.md` and record the trigger.

- Phase 0 — Initialize
- Phase 1 — Clarify
- Phase 2 — Requirements
- Phase 3 — Scope
- Phase 4 — Architecture
- Phase 5 — Decisions
- Phase 6 — Agent rules
- Phase 7 — Plan
- Phase 8 — Implement
- Phase 9 — Verify
- Phase 10 — Review
- Phase 11 — Release
- Phase 12 — Maintain and evolve

The agent must know which phase the project is in and must not silently skip a phase when skipping would create material risk. Material risk means the skipped decision affects a Material or Critical item in the change classification below.

## Required project knowledge

A mature project should maintain these artifacts, using either a single file or a directory as complexity justifies:

- `README.md` — what the project is
- `AGENTS.md` — how agents must work in this repository
- `PROJECT_STATE.md` — current project state
- `SPEC.md` or `spec/` — what the product/system must do
- `ARCHITECTURE.md` or `docs/architecture/` — how the system is designed
- `ADR.md` or `docs/decisions/` — why important decisions were made
- `tasks/`, an issue tracker, or `templates/TASK.md` entries — current executable work
- `tests/` — objective verification
- `CHANGELOG.md` — user-visible evolution

Do not create all artifacts blindly. Create only what the project complexity justifies, but always establish an explicit source of truth for requirements, architecture, state, tasks, and verification.

## Source-of-truth rules

When project sources conflict:

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

## Phase routing

### Phase 0 — Initialize

Goal: establish the problem, users, constraints, repository state, and minimum project-management structure before substantial coding.

Route: procedure `workflows/project-init.md`; artifacts `templates/README.md`, `templates/SPEC.md`, `templates/PROJECT_STATE.md`, `templates/AGENTS.md`.

### Phase 1 — Clarify

Goal: ask only questions that materially reduce ambiguity, and classify unknowns as Critical, Important, or Optional.

Route: use `workflows/project-init.md` for critical unknowns, then `workflows/requirements.md`; record unresolved questions in `templates/SPEC.md`.

### Phase 2 — Requirements

Goal: convert the problem into testable requirements with explicit non-goals, assumptions, and acceptance criteria.

Route: procedure `workflows/requirements.md`; gate `checklists/requirements.md`; artifact `templates/SPEC.md`.

### Phase 3 — Scope

Goal: separate Must/Should/Could/Out of scope and choose the smallest vertical slice for the first implementation target.

Route: use `workflows/requirements.md`; artifact `templates/SPEC.md`; first slice tasks use `templates/TASK.md`; gate remains `checklists/requirements.md`.

### Phase 4 — Architecture

Goal: define only as much architecture as necessary to implement safely.

Route: procedure `workflows/architecture.md`; gate `checklists/architecture.md`; artifacts `templates/ARCHITECTURE.md`, `templates/ADR.md`.

### Phase 5 — Decisions

Goal: record decisions that are difficult to reverse, architecturally significant, security-relevant, operationally significant, likely to be questioned later, or chosen after serious alternatives.

Route: decision trigger inside `workflows/architecture.md`; artifact `templates/ADR.md`; gate item lives in `checklists/architecture.md`.

### Phase 6 — Agent rules

Goal: create or update repository-specific operating rules for agents.

Route: artifact `templates/AGENTS.md`; setup procedure `workflows/project-init.md`; downstream enforcement happens in `workflows/implementation.md` and `workflows/testing.md`.

### Phase 7 — Plan

Goal: convert approved requirements into small executable tasks with objective, scope, dependencies, acceptance criteria, and verification method.

Route: artifact `templates/TASK.md`; inputs from `templates/SPEC.md`, `templates/ARCHITECTURE.md`, and `templates/ADR.md`; sanity-check against `checklists/requirements.md` and `checklists/architecture.md` before implementation.

### Phase 8 — Implement

Goal: make the smallest coherent change that satisfies an approved task while preserving architecture invariants.

Route: procedure `workflows/implementation.md`; task format `templates/TASK.md`; report format `templates/COMPLETION_REPORT.md`.

### Phase 9 — Verify

Goal: prove completion with evidence, starting with the narrowest relevant checks and broadening only as risk warrants.

Route: procedure `workflows/testing.md`; gates `checklists/testing.md` and `checklists/security.md`; evidence format `templates/COMPLETION_REPORT.md`.

### Phase 10 — Review

Goal: review correctness, requirements coverage, regressions, security, maintainability, unnecessary complexity, documentation consistency, and test adequacy.

Route: use the after-coding steps in `workflows/implementation.md` plus the failure protocol in `workflows/testing.md`; gates `checklists/testing.md` and `checklists/security.md`; report format `templates/COMPLETION_REPORT.md`.

### Phase 11 — Release

Goal: declare release-ready only when release criteria, security disposition, migration/configuration checks, changelog, and state updates are complete.

Route: procedure `workflows/release.md`; gate `checklists/release.md`; security disposition from `checklists/security.md`; artifacts `templates/CHANGELOG.md`, `templates/PROJECT_STATE.md`, `templates/COMPLETION_REPORT.md`.

### Phase 12 — Maintain and evolve

Goal: keep current state, tasks, decisions, affected documentation, known limitations, and next priority accurate after meaningful work.

Route: procedure `workflows/maintenance.md`; artifacts `templates/PROJECT_STATE.md`, `templates/CHANGELOG.md`, `templates/ADR.md`, `templates/COMPLETION_REPORT.md`.

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

At the end of a meaningful task, report using `templates/COMPLETION_REPORT.md`:

1. What changed
2. Why it changed
3. What was verified, including commands and evidence location
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
