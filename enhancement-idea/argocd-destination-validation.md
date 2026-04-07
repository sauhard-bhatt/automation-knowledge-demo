# Enhancement – Validate ArgoCD Destination Cluster Before Deployment

## Problem
Deployments fail when destination cluster is not registered or incorrectly named.

## Proposed Solution
Add a pre-flight validation step in CI/CD that:
- checks if destination.name exists in ArgoCD
- fails early if cluster is invalid

## Benefit
Prevents deployment failures and reduces DTR troubleshooting effort.
