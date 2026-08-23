# Architecture

- Status: Draft
- Last verified: YYYY-MM-DD

Writing rule: document only decisions that constrain implementation, verification, security, deployment, or future change. If a section is not needed at current complexity, write `N/A: <reason>` instead of inventing detail.

## 1. Architectural goals

What must this architecture make easy, safe, or cheap?

## 2. System boundaries

What is inside the system, what is outside, and what must never cross without an explicit interface?

Example: "Billing provider is outside; only the Billing Adapter may call it."

## 3. Components

| Component | Owns | Must not own | Notes |
| --- | --- | --- | --- |
|  |  |  |  |

## 4. Data model

Entities, ownership, retention, and invariants.

## 5. Interfaces / APIs

Contracts that other components or external systems depend on. Link ADRs for hard-to-reverse choices.

## 6. Data flow

Trace the primary write path and read path. Include where validation, authorization, and errors happen.

## 7. Security boundaries

Trust boundaries, secrets location, sensitive data classes, and destructive-operation controls.

## 8. Deployment

Runtime topology, environments, configuration sources, and migration entry points.

## 9. Failure modes

What breaks, how it is detected, and what the safe degradation is.

## 10. Observability

Logs, metrics, traces, alerts, and audit records needed to operate the system.

## 11. Scaling assumptions

Expected load now, next credible step, and what is intentionally not designed for yet.
