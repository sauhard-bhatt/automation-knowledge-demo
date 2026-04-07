---
id: INC-0020
type: incident
title: Container failed to start in ACA
domain: aca
platforms: [aca]
severity: sev-1
status: published
created: 2026-04-06
updated: 2026-04-06
tags: [aca, container-apps, container-failed]
error_signatures: ["Container exited with code", "Failed to provision container"]
---

# Container Failed to Start in ACA

## Error
```
Container exited with code 1
Failed to provision container instance
```

## Fix
```bash
# Check container logs
az containerapp logs show --name <app-name> --resource-group <rg-name>

# Verify container image is accessible
az acr repository show --name <registry-name> --image <image-name>

# Check environment variables
az containerapp show --name <app-name> --resource-group <rg-name> \
  | jq '.properties.template.containers[0].env'

# Update and redeploy
az containerapp update --name <app-name> --resource-group <rg-name> \
  --image <correct-image>
```

## Verify
```bash
az containerapp show --name <app-name> --resource-group <rg-name> \
  | grep -i "provisioning state"
```
