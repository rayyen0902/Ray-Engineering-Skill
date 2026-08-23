# Joining an Ongoing Project Workflow

## Goal

Enter a repository that already has documentation or code without inventing missing context and without treating stale documents as current.

## Fixed read order

1. Read `AGENTS.md` for operating rules, forbidden operations, commands, and verified facts/pitfalls.
2. Read `PROJECT_STATE.md` for phase, current objective, blockers, pending decisions, known issues, last phase transition, and next priority.
3. Read the current specification (`SPEC.md` or `spec/`) and check its `Status` / `Last verified` header.
4. Read architecture (`ARCHITECTURE.md` or `docs/architecture/`) and relevant ADRs; check freshness headers where present.
5. Read current tasks (`tasks/`, issue tracker, or `templates/TASK.md` entries).
6. Inspect tests and verification commands before changing code.
7. Inspect existing implementation only after the controlled documents are understood.

## Freshness checks

- If a controlled document lacks `Last verified`, treat it as unverified and say so.
- If `Last verified` predates the last relevant gate, release, or major implementation change, verify the document against current code and user intent before relying on it.
- If controlled documents conflict, apply the source-of-truth rules in `SKILL.md` and report the conflict before consequential changes.

## Entry report

Before making a consequential change, send a short entry report to the user:

1. Current phase judgment.
2. What appears complete, in progress, blocked, and pending.
3. Documents that are stale, missing, or conflicting.
4. Verified facts that constrain the work.
5. Proposed next action and which gate it touches.

Do not start implementation until the user confirms the entry report when the project has Material/Critical ambiguity.
