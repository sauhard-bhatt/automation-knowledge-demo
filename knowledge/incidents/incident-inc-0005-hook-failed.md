---
id: INC-0005
type: incident
title: Sync hook job failed
domain: argocd
platform: aks
severity: sev-1
status: published
created: 2026-04-06
updated: 2026-04-06
tags: [hook-job-failed, argocd]
error_signatures: ["Sync failed: hook / Job"]
---

# Sync Hook Job Failed

## Error
```
Sync failed: hook / Job "db-migrate" failed
```

## Fix
```bash
# Check job logs
kubectl logs -n <namespace> job/<job-name>

# Fix missing secret/dependency, then retry sync
argocd app sync <app-name> --force
```

## Verify
```bash
kubectl get job -n <namespace> <job-name> -o wide
argocd app get <app-name> | grep Status
```
