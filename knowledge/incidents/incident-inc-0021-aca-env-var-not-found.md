---
id: INC-0021
type: incident
title: Environment variable not found in ACA
domain: aca
platforms: [aca]
severity: sev-2
status: published
owner: platform-enablement
created: 2026-04-07
updated: 2026-04-07
tags: [aca, env, config]
related_ids: []
error_signatures: ["Environment variable not found", "KeyError", "Missing required environment variable"]
---

# Environment Variable Not Found in ACA

## Error

```text
Environment variable not found
```

## Fix

```bash
az containerapp show --name <app-name> --resource-group <rg-name> | jq '.properties.template.containers[0].env'
# Add/update missing env var:
az containerapp update --name <app-name> --resource-group <rg-name> \
  --set-env-vars <KEY>=<VALUE>
```

## Verify

```bash
az containerapp show --name <app-name> --resource-group <rg-name> | jq '.properties.template.containers[0].env'
az containerapp logs show --name <app-name> --resource-group <rg-name>
```
