---
id: DG-0003
type: doc-gap
title: ArgoCD RBAC project permissions not configured
domain: argocd
platforms: [argocd+aks]
severity: sev-2
status: published
owner: platform-devops
gap_type: missing-from-docs
created: 2026-04-08
updated: 2026-04-08
tags: [rbac, argocd-project, first-deployment, cross-team, argocd]
related_ids: [INC-0004]
error_signatures: ["permission denied", "is not permitted to", "rpc error.*PermissionDenied"]
---

# Doc Gap: ArgoCD RBAC Project Permissions Not Configured

## What This Is

This is a **cross-team prerequisite gap**. ArgoCD uses Projects to restrict which repositories, clusters, and namespaces a team can deploy to. If the DevOps team has not added your application's repository, destination cluster, and namespace to an ArgoCD Project — or has not assigned your team's role to that project — every sync or get operation will be denied.

## Error You Will See

```
rpc error: code = PermissionDenied desc = application "pad-app" is not permitted to deploy to server ...
```

or

```
permission denied
```

or

```
User does not have permissions to manage application 'pad-app' in project 'default'
```

## Quick Self-Check

**Before reading the rest of this, check your onboarding/deployment guide:**

Search for these keywords in your guide:
- `ArgoCD Project`
- `argocd proj`
- `RBAC`
- `role-based access`
- `add-source`
- `add-destination`

If found: The step was documented but skipped → DG answer is "A1 — Documented but I skipped it"  
If NOT found: True gap → DG answer is "A2 — Never documented"

## What Is Missing

One or more of the following RBAC entries in the ArgoCD Project is absent:
- Your source repository is not in the project's allowed `sourceRepos`
- Your destination cluster/namespace is not in the project's allowed `destinations`
- Your team's role is not granted `sync` or `get` permission for the application

## Is This Step In Your Onboarding Documentation?

**Check your onboarding / deployment guide first.**

### If yes — the step was documented, you missed it

ArgoCD Project RBAC configuration is listed in the onboarding guide but was not done. This step requires DevOps access — you cannot self-serve it.

Send this request to DevOps:
> "Please add the following to ArgoCD Project `<project-name>`:
> - Source repo: `<git-repo-url>`
> - Destination: cluster `<cluster-name>`, namespace `<namespace>`
> - Role `<your-team-role>`: allow `sync` and `get` on application `<app-name>`
> This was listed in our onboarding guide and was missed during setup."

DevOps runs:
```bash
argocd proj get <project-name>
argocd proj add-source <project-name> <git-repo-url>
argocd proj add-destination <project-name> <cluster-name> <namespace>
argocd proj role add-policy <project-name> <role-name> \
  --action get --resource applications --object <project-name>/<app-name>
argocd proj role add-policy <project-name> <role-name> \
  --action sync --resource applications --object <project-name>/<app-name>
```

### If no — this step was never documented

True gap. Two actions needed:

1. Send this request to DevOps:
   > "Please add the following to ArgoCD Project `<project-name>`:
   > - Source repo: `<git-repo-url>`
   > - Destination: cluster `<cluster-name>`, namespace `<namespace>`
   > - Role `<your-team-role>`: allow `sync` and `get` on application `<app-name>`"

2. Ask the doc owner to add ArgoCD Project RBAC configuration as a required step in the onboarding guide.

DevOps runs:
```bash
argocd proj get <project-name>
argocd proj add-source <project-name> <git-repo-url>
argocd proj add-destination <project-name> <cluster-name> <namespace>
argocd proj role add-policy <project-name> <role-name> \
  --action get --resource applications --object <project-name>/<app-name>
argocd proj role add-policy <project-name> <role-name> \
  --action sync --resource applications --object <project-name>/<app-name>
```

## How To Verify It Is Done

Once DevOps confirms, run:
```bash
argocd proj get <project-name>
argocd app get <app-name>
argocd app sync <app-name>
```

Expected: `app get` and `app sync` complete without PermissionDenied errors.

## Related

- Incident: [INC-0004](../incidents/incident-inc-0004-rbac-denied.md)
- Runbook: [RBK-0004](../runbooks/runbook-rbk-0004-platform-onboarding-quick-steps.md)
