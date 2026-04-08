# Doc Gaps Index

These are **cross-team prerequisite gaps** — steps that DevOps/platform team must complete before app dev can deploy successfully. Use this index when you are deploying for the first time and hit an error that suggests something was never set up.

**Copilot prompt pattern for this index:**
> `I am deploying [service] to [platform] for the first time. I get [paste exact error]. What prerequisite step am I missing and who needs to do it?`

---

## ArgoCD + AKS

| ID | Title | Error Signature | Gap Type | Who Does It | Status | Link |
|---|---|---|---|---|---|---|
| DG-0001 | ArgoCD target namespace not pre-provisioned | `namespaces "..." not found` | missing-from-docs | platform-devops | published | [docgap-dg-0001](../knowledge/doc-gaps/docgap-dg-0001-argocd-namespace-not-preprovisioned.md) |
| DG-0002 | ArgoCD destination cluster not registered | `cluster "..." not found` | missing-from-docs | platform-devops | published | [docgap-dg-0002](../knowledge/doc-gaps/docgap-dg-0002-argocd-cluster-not-registered.md) |
| DG-0003 | ArgoCD RBAC project permissions not configured | `PermissionDenied` / `permission denied` | missing-from-docs | platform-devops | published | [docgap-dg-0003](../knowledge/doc-gaps/docgap-dg-0003-argocd-project-rbac-not-configured.md) |
