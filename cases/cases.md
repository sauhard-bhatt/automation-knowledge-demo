# Cases (Legacy)

This folder is a legacy location for incident cases.

## Canonical Location

- New artifacts: `knowledge/incidents/`
- Canonical index: `indexes/incidents-index.md`

## Existing Legacy Cases

- [ArgoCD Sync Failure - Namespace Missing](argocd-sync-failure-namespace-missing.md)
- [ArgoCD Sync Failure - Helm values file missing](argocd-helm-values-file-missing.md)
- [ArgoCD Sync Failure - Destination cluster mismatch](argocd-destination-cluster-mismatch.md)
- [ArgoCD Sync Failure - RBAC permission denied](argocd-rbac-permission-denied.md)
- [ArgoCD Sync Failure - Sync hook job failed](argocd-sync-hook-job-failed.md)

## Migration Rule

When a legacy case is updated, migrate it to a canonical file using:

- `templates/incident-template.md`
