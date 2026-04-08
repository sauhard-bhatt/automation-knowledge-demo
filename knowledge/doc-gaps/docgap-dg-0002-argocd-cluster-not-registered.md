---
id: DG-0002
type: doc-gap
title: ArgoCD destination cluster not registered
domain: argocd
platforms: [argocd+aks]
severity: sev-2
status: published
owner: platform-devops
gap_type: missing-from-docs
created: 2026-04-08
updated: 2026-04-08
tags: [cluster-registration, first-deployment, cross-team, argocd, destination]
related_ids: [INC-0003]
error_signatures: ["cluster \".*\" not found"]
---

# Doc Gap: ArgoCD Destination Cluster Not Registered

## What This Is

This is a **cross-team prerequisite gap**. Before an ArgoCD Application can deploy to a cluster, that cluster must be registered in ArgoCD by the DevOps team. App dev teams reference the cluster by name in their Application spec — but if DevOps never registered it, the reference fails.

## Error You Will See

```
cluster "Customer-Service-prod" not found
```

or

```
cluster "<your-cluster-name>" not found
```

## Quick Self-Check

**Before reading the rest of this, check your onboarding/deployment guide:**

Search for these keywords in your guide:
- `argocd cluster add`
- `cluster registration`
- `register cluster`
- `Add the cluster to ArgoCD`

If found: The step was documented but skipped → DG answer is "A1 — Documented but I skipped it"  
If NOT found: True gap → DG answer is "A2 — Never documented"

## What Is Missing

The target cluster is not registered in ArgoCD. ArgoCD only knows about clusters that have been explicitly added. The name in your Application `spec.destination.name` must exactly match a registered cluster name.

## Is This Step In Your Onboarding Documentation?

**Check your onboarding / deployment guide first.**

### If yes — the step was documented, you missed it

Cluster registration is listed in the onboarding guide but was not done before deployment. This step requires DevOps access — you cannot self-serve it.

Send this request to DevOps:
> "Please register cluster `<cluster-name>` in ArgoCD so that Application `<app-name>` can sync to it. The kubeconfig context is `<kube-context>`. This was listed in our onboarding guide and was missed."

DevOps runs:
```bash
argocd cluster add <kube-context> --name <cluster-name>
argocd cluster list
```

### If no — this step was never documented

True gap. Two actions needed:

1. Send this request to DevOps:
   > "Please register cluster `<cluster-name>` in ArgoCD so that Application `<app-name>` can sync to it. The kubeconfig context is `<kube-context>`."

2. Ask the doc owner to add cluster registration as an explicit prerequisite in the onboarding guide.

DevOps runs:
```bash
argocd cluster add <kube-context> --name <cluster-name>
argocd cluster list
```

## How To Verify It Is Done

Once DevOps confirms, run:
```bash
argocd cluster list | grep <cluster-name>
argocd app sync <app-name>
argocd app get <app-name> | grep Destination
```

Expected: cluster listed, sync status `Synced`, Destination shows correct cluster name.

## Related

- Incident: [INC-0003](../incidents/incident-inc-0003-destination-mismatch.md)
- Runbook: [RBK-0004](../runbooks/runbook-rbk-0004-platform-onboarding-quick-steps.md)
