---
id: DG-0001
type: doc-gap
title: ArgoCD target namespace not pre-provisioned
domain: argocd
platforms: [argocd+aks]
severity: sev-2
status: published
owner: platform-devops
gap_type: missing-from-docs
created: 2026-04-08
updated: 2026-04-08
tags: [namespace, first-deployment, cross-team, argocd]
related_ids: [INC-0001]
error_signatures: ["namespaces \".*\" not found"]
---

# Doc Gap: ArgoCD Target Namespace Not Pre-Provisioned

## What This Is

This is a **cross-team prerequisite gap**. The namespace that ArgoCD syncs resources into must exist in Kubernetes before the first sync. App dev teams do not create namespaces — the platform/DevOps team does. If no one coordinated this step, the sync fails.

## Error You Will See

```
namespaces "pad-dev" not found
```

or

```
namespace "<your-namespace>" not found
```

## Quick Self-Check

**Before reading the rest of this, check your onboarding/deployment guide:**

Search for these keywords in your guide:
- `kubectl create namespace`
- `create namespace`
- `namespace creation`
- `Kubernetes namespace`

If found: The step was documented but skipped → DG answer is "A1 — Documented but I skipped it"  
If NOT found: True gap → DG answer is "A2 — Never documented"

## What Is Missing

The Kubernetes namespace for your application has not been created in the target cluster. ArgoCD cannot sync resources if the destination namespace does not exist.

## Is This Step In Your Onboarding Documentation?

**Check your onboarding / deployment guide first.**

### If yes — the step was documented, you missed it

Namespace creation is documented as an onboarding step but was not done. You need to request it now — namespace lifecycle is owned by the platform/DevOps team, not app dev.

Send this request to DevOps:
> "Please create namespace `<your-namespace>` in cluster `<cluster-name>`. It is needed for ArgoCD app `<app-name>` to sync. This was listed in the onboarding guide and was missed during setup."

DevOps runs:
```bash
kubectl create namespace <your-namespace>
kubectl label namespace <your-namespace> team=<your-team> env=<env>
```

### If no — this step was never documented

True gap. Two actions needed:

1. Send this request to DevOps:
   > "Please create namespace `<your-namespace>` in cluster `<cluster-name>`. It is needed for ArgoCD app `<app-name>` to sync."

2. Ask the doc owner to add a namespace creation step to the onboarding guide so the next team doesn't hit this.

DevOps runs:
```bash
kubectl create namespace <your-namespace>
kubectl label namespace <your-namespace> team=<your-team> env=<env>
```

## How To Verify It Is Done

Once DevOps confirms, run:
```bash
kubectl get ns <your-namespace>
argocd app sync <app-name>
argocd app get <app-name> | grep Status
```

Expected: namespace shows `Active`, sync status shows `Synced`.

## Related

- Incident: [INC-0001](../incidents/incident-inc-0001-namespace-missing.md)
- Runbook: [RBK-0004](../runbooks/runbook-rbk-0004-platform-onboarding-quick-steps.md)
