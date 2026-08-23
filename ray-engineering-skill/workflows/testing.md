# Verification Workflow

## Principle

A task is complete only when its acceptance criteria have evidence.

## Levels

1. Static checks
2. Unit tests
3. Integration tests
4. End-to-end tests
5. Build/package verification
6. Security checks where applicable

Run the smallest relevant set first, then broaden when risk warrants it.

## Failure protocol

When a check fails:

1. Preserve the failure evidence.
2. Diagnose root cause.
3. Fix the cause rather than weakening the test.
4. Re-run the relevant checks.
5. Update documentation if the failure revealed a design issue.
