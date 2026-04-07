---
id: INC-0004
type: incident
title: RBAC permission denied
domain: argocd
platform: aks
severity: sev-1
status: published
created: 2026-04-06
updated: 2026-04-06
tags: [rbac-denied, argocd]
error_signatures: ["forbidden: User.*cannot create resource"]
---

# RBAC Permission Denied

## Error
```
forbidden: User "system:serviceaccount:argocd:argocd-application-controller" cannot create resource "namespaces"
```

## Fix
```bash
# Option A: Create namespace before sync (if allowed)
kubectl create namespace <target-namespace>
argocd app sync <app-name>

# Option B: Grant ArgoCD ClusterRole permission
kubectl create clusterrole argocd-namespaces --verb=create,get,patch --resource=namespaces
kubectl create clusterrolebinding argocd-namespaces \
  --clusterrole=argocd-namespaces \
  --serviceaccount=argocd:argocd-application-controller
argocd app sync <app-name>
```

## Verify
```bash
argocd app get <app-name> | grep Conditions
```
