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

## Azure App Service (1 incident)

| ID | Title | Status | Platforms | Error Signature | Link |
|---|---|---|---|---|---|
| INC-0010 | TargetInvocationException | published | appservice | TargetInvocationException | [Go](../knowledge/incidents/incident-inc-0010-appservice-targetinvocation.md) |

## Azure Container Apps (ACA) (1 incident)

| ID | Title | Status | Platforms | Error Signature | Link |
|---|---|---|---|---|---|
| INC-0020 | Container failed to start | published | aca | Container exited with code / Failed to provision | [Go](../knowledge/incidents/incident-inc-0020-aca-container-failed.md) |

## App Service on Podman (1 incident)

| ID | Title | Status | Platforms | Error Signature | Link |
|---|---|---|---|---|---|
| INC-0030 | Image pull failed | published | podman | Failed to pull image / image not found | [Go](../knowledge/incidents/incident-inc-0030-podman-image-pull.md) |

## WebLogic (1 incident)

| ID | Title | Status | Platforms | Error Signature | Link |
|---|---|---|---|---|---|
| INC-0040 | ClassNotFoundException | published | weblogic | java.lang.ClassNotFoundException | [Go](../knowledge/incidents/incident-inc-0040-weblogic-classnotfound.md) |

---

**Total: 9 published incidents across 5 platforms**
