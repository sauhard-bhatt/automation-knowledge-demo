# ArgoCD Sync Failure – Namespace Missing

## Problem
Developer reported ArgoCD application stuck in OutOfSync state.

## Platform
ArgoCD / AKS

## Error Message
namespaces "pad-dev" not found

## Root Cause
## Fix
1. Create namespace
kubectl create namespace pad-dev

2. Re-sync application in ArgoCD
