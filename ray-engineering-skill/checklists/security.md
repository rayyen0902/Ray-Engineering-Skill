# Security Review

Rules: items marked **(blocking)** must pass or be explicitly waived by the human. Mark non-applicable items as `N/A: <reason>`; never silently skip a line. Mark automatable items with `(automatable)` and link the script/CI check when one exists; manual checklist review is the fallback, not the preferred mechanism.

- [ ] **(blocking)** Authentication considered
- [ ] **(blocking)** Authorization considered
- [ ] **(blocking)** Secrets handling reviewed `(automatable)`
- [ ] Sensitive data identified
- [ ] Input validation considered
- [ ] Dependency risks considered `(automatable)`
- [ ] Logging does not expose sensitive data `(automatable)`
- [ ] **(blocking)** Dangerous/destructive operations require appropriate authorization
- [ ] Deployment security considered
