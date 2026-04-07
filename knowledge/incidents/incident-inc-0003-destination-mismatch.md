---
id: INC-0003
type: incident
title: Destination cluster mismatch
domain: argocd
platform: aks
severity: sev-2
status: published
created: 2026-04-06
updated: 2026-04-06
tags: [destination-mismatch, argocd]
error_signatures: ["cluster \".*\" not found"]
---

# Destination Cluster Mismatch

## Error
```
cluster "Customer-Service-prod" not found
```

## Fix
```bash
# List registered clusters
argocd cluster list

# Option A: Register missing cluster
argocd cluster add <kube-context> --name Customer-Service-prod

# Option B: Update Application destination to match registered name
kubectl patch app <app-name> -n argocd --type merge \
  -p '{"spec":{"destination":{"name":"<registered-cluster-name>"}}}'

argocd app sync <app-name>
```

## Verify
```bash
argocd app get <app-name> | grep Destination
```
