# Documentation Gap – ArgoCD Onboarding

## Problem
ArgoCD onboarding document did not mention that namespace must exist before deployment.

## Impact
Multiple teams failed onboarding.

## Proposed Fix
Add namespace validation step in onboarding guide.

## Owner
Platform Team

# Automation Idea – ArgoCD Namespace Validation

## Problem
ArgoCD deployments fail if namespace does not exist.

## Proposed Solution
Add GitHub Action pre-flight validation that checks namespace existence.

## Benefit
Prevents deployment failures before ArgoCD sync.
