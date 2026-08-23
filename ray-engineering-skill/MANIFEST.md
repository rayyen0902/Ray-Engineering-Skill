# Ray Engineering Skill Manifest

Start with `SKILL.md`. Load detail files only when a phase route, gate, or artifact requires them.

Internal precedence:

- Principles and approval gates: `SKILL.md`
- Procedure order: `workflows/`
- Artifact format: `templates/`
- Gate pass criteria: `checklists/`

## File map

| File | Use it when |
| --- | --- |
| `SKILL.md` | Always read first for principles, phase routing, gates, source-of-truth rules, and completion contract. |
| `workflows/project-init.md` | Phase 0/1: initializing a repository or clarifying critical unknowns. |
| `workflows/requirements.md` | Phase 2/3: turning an idea into testable requirements and scope. |
| `workflows/architecture.md` | Phase 4/5: designing proportional architecture and triggering ADRs. |
| `workflows/implementation.md` | Phase 8/10: before/during/after coding for an approved task. |
| `workflows/testing.md` | Phase 9/10: verification levels, failure protocol, and evidence expectations. |
| `workflows/release.md` | Phase 11: release preconditions and release process. |
| `workflows/maintenance.md` | Phase 12: after meaningful changes, keep docs/state/decisions current. |
| `checklists/requirements.md` | Requirements/scope gate before architecture or implementation. |
| `checklists/architecture.md` | Architecture gate before major implementation. |
| `checklists/testing.md` | Verification gate before review/release claims. |
| `checklists/security.md` | Security review for implementation, verification, and release disposition. |
| `checklists/release.md` | Release gate before declaring release-ready. |
| `templates/README.md` | Create or refresh the project README. |
| `templates/AGENTS.md` | Create or refresh repository-specific agent operating rules. |
| `templates/SPEC.md` | Create or refresh requirements, scope, assumptions, and acceptance criteria. |
| `templates/ARCHITECTURE.md` | Create or refresh proportional architecture documentation. |
| `templates/ADR.md` | Record a significant decision with context, alternatives, and consequences. |
| `templates/TASK.md` | Convert approved work into an executable task with acceptance and verification. |
| `templates/PROJECT_STATE.md` | Keep current phase, progress, blockers, pending decisions, known issues, and next priority current. |
| `templates/CHANGELOG.md` | Record user-visible evolution. |
| `templates/COMPLETION_REPORT.md` | Report meaningful task completion with evidence and uncertainty. |
