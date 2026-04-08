# Operating Model

## Purpose

Keep user support content simple and fast, while enforcing quality and consistency through admin governance.

## Two Lanes

1. User lane
- Inputs: exact error text, platform, migration request.
- Outputs: fix and verify, missing prerequisite guidance, migration steps.
- Sources: [../indexes](../indexes), [../knowledge](../knowledge).

2. Admin lane
- Inputs: new issue patterns, recurring failures, content quality gaps.
- Outputs: reviewed artifacts, updated standards, release approvals.
- Sources: this directory.

## Workflow

1. User issue arrives.
2. Search existing user-facing indexes.
3. If missing or low confidence, maintainer creates or updates artifact.
4. Reviewer applies [02-review-checklist.md](02-review-checklist.md).
5. Release approver validates [05-release-gate.md](05-release-gate.md).
6. Merge.

## Future State

When ready, move this entire directory to a private governance repository with the same file names.
