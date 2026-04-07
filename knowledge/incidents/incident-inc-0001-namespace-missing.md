---
id: INC-0001
type: incident
title: Namespace missing
domain: argocd
platforms: [argocd+aks]
severity: sev-2
status: published
created: 2026-04-06
updated: 2026-04-06
tags: [namespace-missing, argocd]
error_signatures: ["namespaces \".*\" not found"]
---

# Namespace Missing

## Error
```
namespaces "pad-dev" not found
```

## Fix
```bash
kubectl create namespace pad-dev
argocd app sync <app-name>
```

## Verify
```bash
kubectl get ns pad-dev
argocd app get <app-name> | grep Status
```
