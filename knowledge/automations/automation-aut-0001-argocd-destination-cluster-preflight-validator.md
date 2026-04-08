---
id: AUT-0001
type: automation
title: ArgoCD destination cluster preflight validator
domain: argocd
platforms: [argocd+aks]
severity: sev-3
status: draft
owner: platform-devops
created: 2026-04-06
updated: 2026-04-08
tags: [automation, preflight, argocd, destination-validation]
related_ids: [INC-0003, DG-0002]
error_signatures: ["cluster \".*\" not found"]
---

# Automation: ArgoCD Destination Cluster Preflight Validator

## Summary

Fail fast in CI/CD if an ArgoCD application points to a destination cluster name that is not registered in ArgoCD.

## Trigger Condition

Pipeline detects ArgoCD Application manifest changes, or deployment job starts for an ArgoCD-managed service.

## Required Inputs

- ArgoCD server URL
- ArgoCD auth token with read access to clusters
- Application manifest path
- `spec.destination.name` value from manifest

## Safe Checks

1. Parse Application manifest and extract destination name.
2. Query registered clusters from ArgoCD.
3. Compare names with exact match.
4. If no match, stop pipeline with actionable error.

## Action Steps

```bash
APP_DEST_NAME=$(yq '.spec.destination.name' <app-manifest.yaml>)
argocd cluster list -o name | grep -Fx "$APP_DEST_NAME"
```

If `grep` does not match:
- Exit non-zero
- Print remediation:
  - Register cluster: `argocd cluster add <kube-context> --name <cluster-name>`
  - Or update app destination name to a registered cluster

## Expected Output

- Success: pipeline continues
- Failure: clear preflight message with required fix and verify command

## Rollback

Disable validator stage for emergency deployment and track exception ticket for follow-up.

## Related Artifacts

- Related Incident: [INC-0003](../incidents/incident-inc-0003-destination-mismatch.md)
- Related Doc Gap: [DG-0002](../doc-gaps/docgap-dg-0002-argocd-cluster-not-registered.md)
- Related Runbook: [RBK-0004](../runbooks/runbook-rbk-0004-platform-onboarding-quick-steps.md)
