# ArgoCD Sync Failure – Helm values file missing

## Problem
ArgoCD Application fails to sync. Developer reports "something not working" after onboarding.

## Platform
ArgoCD / AKS / Helm

## Error Message
rpc error: code = Unknown desc = failed to generate manifest: open values/dev.yaml: no such file or directory

## Root Cause
ArgoCD Application points to a values file path that does not exist in the repo/branch.

## Fix
1. Confirm the repo path and branch used by the ArgoCD Application.
2. Verify the values file exists at the expected path.
3. Update the Application source configuration (or repo structure) so the referenced values file exists.
4. Re-sync the application.

## Prevention
- Add a preflight check in CI to validate referenced values files exist for the selected environment.
- Document expected repo layout and naming conventions for values files.

## Automation Opportunity
Add a GitHub Action that validates Helm chart paths + values file references for ArgoCD Application manifests.
