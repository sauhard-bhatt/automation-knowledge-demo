---
id: INC-0010
type: incident
title: TargetInvocationException in App Service
domain: appservice
platforms: [appservice]
severity: sev-2
status: published
created: 2026-04-06
updated: 2026-04-06
tags: [appservice, runtime-error, target-invocation]
error_signatures: ["TargetInvocationException"]
---

# TargetInvocationException in App Service

## Error
```
TargetInvocationException: Exception has been thrown by the target of an invocation.
```

## Fix
```bash
# Check Application Insights logs
az monitor app-insights query --app <app-insights-name> \
  --query "exceptions | where type == 'TargetInvocationException'" \
  --scope last_24h

# Check App Service logs
az webapp log tail --name <app-name> --resource-group <rg-name>

# Restart app
az webapp restart --name <app-name> --resource-group <rg-name>
```

## Verify
```bash
az webapp show --name <app-name> --resource-group <rg-name> \
  | grep -i "state"
```
