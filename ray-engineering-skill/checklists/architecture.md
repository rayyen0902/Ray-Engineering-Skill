# Architecture Gate

Rules: items marked **(blocking)** must pass or be explicitly waived by the human. Mark non-applicable items as `N/A: <reason>`; never silently skip a line. Mark automatable items with `(automatable)` and link the script/CI check when one exists; manual checklist review is the fallback, not the preferred mechanism.

- [ ] **(blocking)** Requirements are approved
- [ ] System boundaries defined
- [ ] Major components defined
- [ ] Data ownership defined
- [ ] Interfaces identified
- [ ] Main data flows understood
- [ ] **(blocking)** Security boundaries considered
- [ ] Failure modes considered
- [ ] Operational needs considered
- [ ] **(blocking)** Significant decisions have ADRs
- [ ] **(blocking)** Architecture approval obtained
