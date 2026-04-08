# Incidents By Platform

Find your platform. Copy fix command. Done.

---

## ArgoCD + AKS

| Error | Incident | Fix |
|---|---|---|
| `namespaces ".*" not found` | INC-0001 | kubectl create namespace &lt;name&gt; |
| `open values.*: no such file` | INC-0002 | [Verify path](../knowledge/incidents/incident-inc-0002-values-file-missing.md) |
| `cluster ".*" not found` | INC-0003 | argocd cluster list / add |
| `forbidden: User.*cannot create` | INC-0004 | [Grant RBAC](../knowledge/incidents/incident-inc-0004-rbac-denied.md) |
| `Sync failed: hook / Job` | INC-0005 | kubectl logs job/&lt;name&gt; |

**Details: [INC-0001](../knowledge/incidents/incident-inc-0001-namespace-missing.md) | [INC-0002](../knowledge/incidents/incident-inc-0002-values-file-missing.md) | [INC-0003](../knowledge/incidents/incident-inc-0003-destination-mismatch.md) | [INC-0004](../knowledge/incidents/incident-inc-0004-rbac-denied.md) | [INC-0005](../knowledge/incidents/incident-inc-0005-hook-failed.md)**

---

## Azure App Service

| Error | Incident | Fix |
|---|---|---|
| TargetInvocationException | INC-0010 | [Azure CLI query logs](../knowledge/incidents/incident-inc-0010-appservice-targetinvocation.md) |
| 401 Unauthorized | INC-0011 | [Check auth and identity](../knowledge/incidents/incident-inc-0011-appservice-401-unauthorized.md) |
| 503 Service Unavailable | INC-0012 | [Restart and check health](../knowledge/incidents/incident-inc-0012-appservice-503-unavailable.md) |

---

## Azure Container Apps (ACA)

| Error | Incident | Fix |
|---|---|---|
| Container failed to start | INC-0020 | [Check logs](../knowledge/incidents/incident-inc-0020-aca-container-failed.md) |
| Environment variable not found | INC-0021 | [Set missing env var](../knowledge/incidents/incident-inc-0021-aca-env-var-not-found.md) |
| Port already in use | INC-0022 | [Update ingress target port](../knowledge/incidents/incident-inc-0022-aca-port-already-in-use.md) |

---

## App Service on Podman

| Error | Incident | Fix |
|---|---|---|
| Image pull failed | INC-0030 | [podman pull](../knowledge/incidents/incident-inc-0030-podman-image-pull.md) |
| Container runtime error | INC-0031 | [Inspect runtime and recreate](../knowledge/incidents/incident-inc-0031-podman-runtime-error.md) |
| Volume mount denied | INC-0032 | [Fix mount permissions](../knowledge/incidents/incident-inc-0032-podman-volume-mount-denied.md) |

---

## WebLogic

| Error | Incident | Fix |
|---|---|---|
| ClassNotFoundException | INC-0040 | [Check classpath](../knowledge/incidents/incident-inc-0040-weblogic-classnotfound.md) |
| Connection refused | INC-0041 | [Check listener and server status](../knowledge/incidents/incident-inc-0041-weblogic-connection-refused.md) |
| OutOfMemoryError | INC-0042 | [Increase JVM heap and restart](../knowledge/incidents/incident-inc-0042-weblogic-outofmemory.md) |

---

**Quick search: [error-signatures-by-platform.md](error-signatures-by-platform.md)**
