# Release Gate

A change is release-ready only if all gates pass.

## Gate A: Content Integrity

- [ ] Artifact content is correct for target platform.
- [ ] Steps are reproducible.
- [ ] Verify commands confirm expected state.

## Gate B: Discoverability

- [ ] Artifact is reachable from at least one entry index.
- [ ] Existing paths are not broken.

## Gate C: Governance Compliance

- [ ] Review checklist is fully passed.
- [ ] Ownership of artifact is assigned.
- [ ] Status field reflects actual maturity.

## Gate D: Risk and Safety

- [ ] No secrets in content.
- [ ] Risky operations include context/warnings.
- [ ] Rollback path exists when applicable.

## Approval Rule

Minimum approvals:
1. One technical reviewer.
2. One governance or release approver.
