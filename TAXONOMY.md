# Taxonomy

Controlled vocabulary improves Copilot retrieval and enables deterministic automation routing.

## Platforms

- `argocd+aks` — ArgoCD deployments on Azure Kubernetes Service
- `appservice` — Azure App Service (web apps, API apps)
- `aca` — Azure Container Apps
- `podman` — Podman container runtime
- `weblogic` — Oracle WebLogic Application Server

## Domains

- `argocd`
- `kubernetes`
- `helm`
- `aks`
- `rbac`
- `ci-cd`
- `appservice`
- `container-apps`
- `weblogic`

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
- Platform-specific: `appservice`, `aca`, `podman`, `weblogic`, `argocd`, `kubernetes`

## Error Signature Guidance

- Capture exact text from logs/events.
- Keep one signature per list entry.
- Prefer literal phrases over paraphrasing.
- Add top-level mapping in `indexes/error-signatures-by-platform.md`.
- **Platform-aware:** same error text may appear on multiple platforms with different fixes.
