# Error Signatures Index

Map exact error text to incident IDs for deterministic lookup.

| Signature | Incident ID | First Action | Primary Runbook |
|---|---|---|---|
| namespaces \"pad-dev\" not found | INC-0001 | Create namespace and re-sync | RBK-0001 |
| open values/dev.yaml: no such file or directory | INC-0002 | Validate values path in source config | RBK-0001 |
| cluster \"Customer-Service-prod\" not found | INC-0003 | Validate destination cluster registration | RBK-0001 |
| forbidden: User \"system:serviceaccount:argocd:argocd-application-controller\" cannot create resource \"namespaces\" | INC-0004 | Validate ArgoCD controller RBAC | RBK-0001 |
| Sync failed: hook / Job \"db-migrate\" failed | INC-0005 | Inspect job logs and dependencies | RBK-0001 |
