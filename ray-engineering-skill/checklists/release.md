# Release Gate

Rules: items marked **(blocking)** must pass or be explicitly waived by the human. Mark non-applicable items as `N/A: <reason>`; never silently skip a line. Mark automatable items with `(automatable)` and link the script/CI check when one exists; manual checklist review is the fallback, not the preferred mechanism.

- [ ] **(blocking)** Scope is complete
- [ ] **(blocking)** Critical tests pass `(automatable)`
- [ ] **(blocking)** Known critical issues resolved
- [ ] Version updated if applicable
- [ ] **(blocking)** Changelog updated
- [ ] Configuration reviewed
- [ ] Database migrations reviewed
- [ ] Rollback strategy considered
- [ ] **(blocking)** Security review completed or explicitly waived with reason
- [ ] Deployment verified
- [ ] **(blocking)** PROJECT_STATE updated
