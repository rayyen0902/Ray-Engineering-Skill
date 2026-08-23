# Release Gate

Rules: items marked **(blocking)** must pass or be explicitly waived by the human. Mark non-applicable items as `N/A: <reason>`; never silently skip a line. Prefer automated or recorded evidence where practical.

- [ ] **(blocking)** Scope is complete
- [ ] **(blocking)** Critical tests pass
- [ ] **(blocking)** Known critical issues resolved
- [ ] Version updated if applicable
- [ ] **(blocking)** Changelog updated
- [ ] Configuration reviewed
- [ ] Database migrations reviewed
- [ ] Rollback strategy considered
- [ ] **(blocking)** Security review completed or explicitly waived with reason
- [ ] Deployment verified
- [ ] **(blocking)** PROJECT_STATE updated
