---
id: RBK-0004
type: runbook
title: Platform Onboarding Quick Steps
domain: platform
platforms: [argocd+aks, appservice, aca]
severity: sev-3
status: published
owner: platform-enablement
created: 2026-04-07
updated: 2026-04-07
tags: [onboarding, quick-steps]
related_ids: [INC-0001, INC-0002, INC-0003, GAP-0001]
error_signatures: []
---

# Runbook: Platform Onboarding Quick Steps

## Summary

Minimal onboarding checklist for users who are blocked while onboarding and need direct steps.

## ArgoCD + AKS Onboarding

1. Create namespace.
2. Verify ArgoCD destination cluster exists.
3. Verify repository path and values file path.
4. Apply ArgoCD Application manifest.
5. Sync and verify health.

## Commands

```bash
kubectl create namespace <namespace>
argocd cluster list
argocd app create <app-name> --repo <repo-url> --path <path> --dest-name <cluster-name> --dest-namespace <namespace>
argocd app sync <app-name>
argocd app get <app-name>
```

## Verify

```bash
argocd app get <app-name> | grep -E "Status|Health"
```

## Related Artifacts

- Related Incident: [INC-0001](../incidents/incident-inc-0001-namespace-missing.md)
- Related Incident: [INC-0002](../incidents/incident-inc-0002-values-file-missing.md)
- Related Incident: [INC-0003](../incidents/incident-inc-0003-destination-mismatch.md)
- Related Doc Gap: [DG-0001](../doc-gaps/docgap-dg-0001-argocd-namespace-not-preprovisioned.md)
