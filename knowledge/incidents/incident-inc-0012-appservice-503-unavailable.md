---
id: INC-0012
type: incident
title: 503 Service Unavailable on App Service
domain: appservice
platforms: [appservice]
severity: sev-1
status: published
owner: platform-enablement
created: 2026-04-07
updated: 2026-04-07
tags: [appservice, availability, 503]
related_ids: []
error_signatures: ["503 Service Unavailable", "HTTP Error 503"]
---

# 503 Service Unavailable on App Service

## Error

```text
503 Service Unavailable
```

## Fix

```bash
az webapp show --name <app-name> --resource-group <rg-name>
az webapp log tail --name <app-name> --resource-group <rg-name>
az webapp config appsettings list --name <app-name> --resource-group <rg-name>
# Restart app and warm up endpoint:
az webapp restart --name <app-name> --resource-group <rg-name>
curl -I https://<app-name>.azurewebsites.net/health
```

## Verify

```bash
curl -I https://<app-name>.azurewebsites.net
az webapp show --name <app-name> --resource-group <rg-name> | grep -i state
```
