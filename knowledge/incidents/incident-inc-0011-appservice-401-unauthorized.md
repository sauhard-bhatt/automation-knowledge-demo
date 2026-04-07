---
id: INC-0011
type: incident
title: 401 Unauthorized on App Service
domain: appservice
platforms: [appservice]
severity: sev-2
status: published
owner: platform-enablement
created: 2026-04-07
updated: 2026-04-07
tags: [appservice, auth, unauthorized]
related_ids: []
error_signatures: ["401 Unauthorized", "HTTP Error 401"]
---

# 401 Unauthorized on App Service

## Error

```text
401 Unauthorized
```

## Fix

```bash
az webapp auth show --name <app-name> --resource-group <rg-name>
az webapp config appsettings list --name <app-name> --resource-group <rg-name>
az webapp identity show --name <app-name> --resource-group <rg-name>
# If managed identity missing or disabled:
az webapp identity assign --name <app-name> --resource-group <rg-name>
# If auth settings are incorrect, update auth config then restart app:
az webapp restart --name <app-name> --resource-group <rg-name>
```

## Verify

```bash
az webapp show --name <app-name> --resource-group <rg-name> | grep -i state
curl -I https://<app-name>.azurewebsites.net
```
