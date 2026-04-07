---
id: INC-0002
type: incident
title: Values file missing
domain: argocd
platform: aks
severity: sev-2
status: published
created: 2026-04-06
updated: 2026-04-06
tags: [values-file-missing, argocd]
error_signatures: ["open values.*: no such file or directory"]
---

# Helm Values File Missing

## Error
```
failed to generate manifest: open values/dev.yaml: no such file or directory
```

## Fix
```bash
# Verify correct path in Application spec:
kubectl get app <app-name> -n argocd -o yaml | grep -A 5 "helm:"

# Update Application helm values path or create missing file
kubectl patch app <app-name> -n argocd --type merge \
  -p '{"spec":{"source":{"helm":{"valuesFiles":["values/dev.yaml"]}}}}'

argocd app sync <app-name>
```

## Verify
```bash
argocd app get <app-name> | grep Conditions
```
