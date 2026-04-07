---
id: INC-0022
type: incident
title: Port already in use in ACA
domain: aca
platforms: [aca]
severity: sev-2
status: published
owner: platform-enablement
created: 2026-04-07
updated: 2026-04-07
tags: [aca, port, startup]
related_ids: []
error_signatures: ["Port already in use", "address already in use", "bind: address already in use"]
---

# Port Already in Use in ACA

## Error

```text
Port already in use
```

## Fix

```bash
az containerapp show --name <app-name> --resource-group <rg-name> | jq '.properties.configuration.ingress'
# Set correct target port to match container app listening port:
az containerapp ingress update --name <app-name> --resource-group <rg-name> --target-port <port>
# Redeploy container if app listens on different port:
az containerapp update --name <app-name> --resource-group <rg-name> --image <image>
```

## Verify

```bash
az containerapp show --name <app-name> --resource-group <rg-name> | jq '.properties.configuration.ingress.targetPort'
az containerapp logs show --name <app-name> --resource-group <rg-name>
```
