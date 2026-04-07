# Error Signatures by Platform

Match your exact error text and platform to incident.

---

## ArgoCD + AKS

| Error Pattern | Incident | Direct Fix |
|---|---|---|
| `namespaces ".*" not found` | INC-0001 | `kubectl create namespace <name>` |
| `open values.*: no such file` | INC-0002 | Update helm valuesFiles path |
| `cluster ".*" not found` | INC-0003 | `argocd cluster list` + register |
| `forbidden: User.*cannot create` | INC-0004 | Create namespace OR grant RBAC |
| `Sync failed: hook / Job` | INC-0005 | `kubectl logs job/<name>` |

---

## Azure App Service

| Error Pattern | Incident | Direct Fix |
|---|---|---|
| `TargetInvocationException` | INC-0010 | `az monitor app-insights query` + restart |
| `401 Unauthorized` | INC-0011 | Validate auth config + managed identity |
| `503 Service Unavailable` | INC-0012 | Check logs + restart + health probe |

---

## Azure Container Apps (ACA)

| Error Pattern | Incident | Direct Fix |
|---|---|---|
| `Container exited with code` | INC-0020 | `az containerapp logs show` |
| `Failed to provision container` | INC-0020 | Verify image + redeploy |
| `Environment variable not found` | INC-0021 | Set missing env var with `az containerapp update --set-env-vars` |
| `Port already in use` | INC-0022 | Correct ingress `targetPort` |

---

## App Service on Podman

| Error Pattern | Incident | Direct Fix |
|---|---|---|
| `Failed to pull image` | INC-0030 | `podman pull <registry>/<image>` |
| `image not found` | INC-0030 | `podman login` + retry pull |
| `Container runtime error` | INC-0031 | Inspect logs + recreate container |
| `Volume mount denied` | INC-0032 | Use correct mount perms/SELinux relabel |

---

## WebLogic

| Error Pattern | Incident | Direct Fix |
|---|---|---|
| `java.lang.ClassNotFoundException` | INC-0040 | Add JAR to `$DOMAIN_HOME/lib/` + restart |
| `Connection refused` | INC-0041 | Check listener port + start server |
| `OutOfMemoryError` | INC-0042 | Increase heap in startup args + restart |

---

**For details: click incident link in [by-platform.md](by-platform.md)**

**All incidents: [../knowledge/incidents/](../knowledge/incidents/)**
