# ArgoCD Sync Failure – Destination cluster mismatch

## Problem
Application does not deploy to the expected cluster. Sync fails or resources appear in the wrong place.

## Platform
ArgoCD / AKS

## Error Message
cluster "Customer-Service-prod" not found

## Root Cause
ArgoCD Application destination.name references a cluster that is not registered in ArgoCD (or wrong cluster name).

## Fix
1. In ArgoCD: Settings → Clusters, verify the destination cluster exists/registered.
2. Compare the Application spec.destination.name to the registered cluster name.
3. Update the Application destination to the correct cluster.
4. Re-sync.

## Prevention
- Standardize destination cluster naming in onboarding docs.
- Add validation for destination cluster name during PR review.

## Automation Opportunity
Create a preflight validator that checks destination.name matches one of the registered clusters (via ArgoCD API).
