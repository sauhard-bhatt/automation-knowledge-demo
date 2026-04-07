# Taxonomy

Controlled vocabulary improves Copilot retrieval and enables deterministic automation routing.

## Domains

- `argocd`
- `kubernetes`
- `helm`
- `aks`
- `rbac`
- `ci-cd`

## Platforms

- `aks`
- `argocd`
- `github-actions`
- `rundeck`

## Severity

- `sev-1`: production outage or major customer impact
- `sev-2`: degraded service with workaround
- `sev-3`: localized impact
- `sev-4`: minor issue or documentation-only

## Status

- `draft`
- `published`
- `deprecated`

## Tag Families

- Failure phase: `preflight`, `manifest-generation`, `apply`, `post-sync`
- Failure class: `namespace-missing`, `rbac-denied`, `values-file-missing`, `destination-mismatch`, `hook-job-failed`
- Action type: `triage`, `runbook`, `prevention`, `automation`

## Error Signature Guidance

- Capture exact text from logs/events.
- Keep one signature per list entry.
- Prefer literal phrases over paraphrasing.
- Add top-level mapping in `indexes/error-signatures-index.md`.
