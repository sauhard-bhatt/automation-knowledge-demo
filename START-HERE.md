# Troubleshooting: 4 Steps

## Step 1: Pick Your Platform

Go to: [BY-PLATFORM.md](BY-PLATFORM.md) or [indexes/by-platform.md](indexes/by-platform.md)

Find your platform (ArgoCD+AKS, App Service, ACA, Podman, WebLogic, etc).

## Step 2: Find Your Error

Match your error to the table row.

## Step 3: Click Incident Link (optional)

For quick fix → copy command from table.

For full details → click incident link.

## Step 4: Copy & Run

Run fix command. Verify with verify command.

---

## Example

**Platform:** ArgoCD + AKS

**Error:** namespaces "pad-dev" not found

**Go to:** [indexes/by-platform.md](indexes/by-platform.md) → Table "ArgoCD + AKS" → Row "namespaces" → Copy fix

**Run:** `kubectl create namespace pad-dev`

---

## Alternative

For all platforms + all errors: [QUICK-FIX.md](QUICK-FIX.md)
