---
id: RBK-0003
type: runbook
title: Copilot Error Query Demo
domain: platform
platforms: [argocd+aks, appservice, aca, podman, weblogic]
severity: sev-4
status: published
owner: platform-enablement
created: 2026-04-07
updated: 2026-04-07
tags: [copilot, query-flow, precision]
related_ids: [INC-0003, INC-0020, INC-0040]
error_signatures: ["cluster \".*\" not found", "Container exited with code", "java.lang.ClassNotFoundException"]
---

# Runbook: Copilot Error Query Demo

## Summary

Use this runbook to validate the end-to-end user experience: user pastes an error, Copilot returns only fix and verify steps.

## Demo Scenario 1: Pipeline Error

### User Prompt

`cluster "Customer-Service-prod" not found`

### Expected Copilot Response

## Fix
```bash
argocd cluster list
argocd cluster add <kube-context> --name Customer-Service-prod
# OR patch destination to registered cluster name
kubectl patch app <app-name> -n argocd --type merge \
  -p '{"spec":{"destination":{"name":"<registered-cluster-name>"}}}'
argocd app sync <app-name>
```

## Verify
```bash
argocd app get <app-name> | grep Destination
```

### Source Artifact

- Incident: [INC-0003](../incidents/incident-inc-0003-destination-mismatch.md)

## Demo Scenario 2: Platform Log Error (ACA)

### User Prompt

`Container exited with code 1`

### Expected Copilot Response

## Fix
```bash
az containerapp logs show --name <app-name> --resource-group <rg-name>
az containerapp update --name <app-name> --resource-group <rg-name> --image <correct-image>
```

## Verify
```bash
az containerapp show --name <app-name> --resource-group <rg-name> | grep -i provisioning
```

### Source Artifact

- Incident: [INC-0020](../incidents/incident-inc-0020-aca-container-failed.md)

## Demo Scenario 3: Onboarding Clarification

### User Prompt

`How do I onboard a service to ArgoCD on AKS?`

### Expected Copilot Response

## Steps
1. Create target namespace.
2. Ensure destination cluster is registered in ArgoCD.
3. Create ArgoCD Application manifest with correct repo/path/values file.
4. Sync application.
5. Verify Synced and Healthy.

### Source Artifacts

- Platform index: [By Platform](../../indexes/by-platform.md)
- Error-first lookup: [Error Signatures by Platform](../../indexes/error-signatures-by-platform.md)

## Precision Rule

Copilot response must not include background text when user asks for direct troubleshooting.

## Related Artifacts

- Related Incident: [INC-0003](../incidents/incident-inc-0003-destination-mismatch.md)
- Related Runbook: [RBK-0004](runbook-rbk-0004-platform-onboarding-quick-steps.md)
