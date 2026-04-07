# Incidents Index

**Sorted by ID. Filter by platform using [BY-PLATFORM.md](../BY-PLATFORM.md) or [error-signatures-by-platform.md](error-signatures-by-platform.md).**

## ArgoCD + AKS (5 incidents)

| ID | Title | Status | Platforms | Error Signature | Link |
|---|---|---|---|---|---|
| INC-0001 | Namespace missing | published | argocd+aks | namespaces ".*" not found | [Go](../knowledge/incidents/incident-inc-0001-namespace-missing.md) |
| INC-0002 | Helm values file missing | published | argocd+aks | open values.*: no such file | [Go](../knowledge/incidents/incident-inc-0002-values-file-missing.md) |
| INC-0003 | Destination cluster mismatch | published | argocd+aks | cluster ".*" not found | [Go](../knowledge/incidents/incident-inc-0003-destination-mismatch.md) |
| INC-0004 | RBAC permission denied | published | argocd+aks | forbidden: User.*cannot create resource | [Go](../knowledge/incidents/incident-inc-0004-rbac-denied.md) |
| INC-0005 | Sync hook job failed | published | argocd+aks | Sync failed: hook / Job | [Go](../knowledge/incidents/incident-inc-0005-hook-failed.md) |

## Azure App Service (3 incidents)

| ID | Title | Status | Platforms | Error Signature | Link |
|---|---|---|---|---|---|
| INC-0010 | TargetInvocationException | published | appservice | TargetInvocationException | [Go](../knowledge/incidents/incident-inc-0010-appservice-targetinvocation.md) |
| INC-0011 | 401 Unauthorized | published | appservice | 401 Unauthorized | [Go](../knowledge/incidents/incident-inc-0011-appservice-401-unauthorized.md) |
| INC-0012 | 503 Service Unavailable | published | appservice | 503 Service Unavailable | [Go](../knowledge/incidents/incident-inc-0012-appservice-503-unavailable.md) |

## Azure Container Apps (ACA) (3 incidents)

| ID | Title | Status | Platforms | Error Signature | Link |
|---|---|---|---|---|---|
| INC-0020 | Container failed to start | published | aca | Container exited with code / Failed to provision | [Go](../knowledge/incidents/incident-inc-0020-aca-container-failed.md) |
| INC-0021 | Environment variable not found | published | aca | Environment variable not found | [Go](../knowledge/incidents/incident-inc-0021-aca-env-var-not-found.md) |
| INC-0022 | Port already in use | published | aca | Port already in use | [Go](../knowledge/incidents/incident-inc-0022-aca-port-already-in-use.md) |

## App Service on Podman (3 incidents)

| ID | Title | Status | Platforms | Error Signature | Link |
|---|---|---|---|---|---|
| INC-0030 | Image pull failed | published | podman | Failed to pull image / image not found | [Go](../knowledge/incidents/incident-inc-0030-podman-image-pull.md) |
| INC-0031 | Container runtime error | published | podman | Container runtime error | [Go](../knowledge/incidents/incident-inc-0031-podman-runtime-error.md) |
| INC-0032 | Volume mount denied | published | podman | Volume mount denied | [Go](../knowledge/incidents/incident-inc-0032-podman-volume-mount-denied.md) |

## WebLogic (3 incidents)

| ID | Title | Status | Platforms | Error Signature | Link |
|---|---|---|---|---|---|
| INC-0040 | ClassNotFoundException | published | weblogic | java.lang.ClassNotFoundException | [Go](../knowledge/incidents/incident-inc-0040-weblogic-classnotfound.md) |
| INC-0041 | Connection refused | published | weblogic | Connection refused | [Go](../knowledge/incidents/incident-inc-0041-weblogic-connection-refused.md) |
| INC-0042 | OutOfMemoryError | published | weblogic | java.lang.OutOfMemoryError | [Go](../knowledge/incidents/incident-inc-0042-weblogic-outofmemory.md) |

---

**Total: 17 published incidents across 5 platforms**
