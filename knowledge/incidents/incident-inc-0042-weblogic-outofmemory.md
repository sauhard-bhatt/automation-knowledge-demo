---
id: INC-0042
type: incident
title: OutOfMemoryError on WebLogic
domain: weblogic
platforms: [weblogic]
severity: sev-1
status: published
owner: platform-enablement
created: 2026-04-07
updated: 2026-04-07
tags: [weblogic, memory, jvm]
related_ids: []
error_signatures: ["OutOfMemoryError", "java.lang.OutOfMemoryError"]
---

# OutOfMemoryError on WebLogic

## Error

```text
java.lang.OutOfMemoryError
```

## Fix

```bash
# Check memory pressure and recent OOM logs:
tail -f $DOMAIN_HOME/servers/AdminServer/logs/AdminServer.log | grep -i OutOfMemoryError
# Increase JVM heap in start script (example):
# USER_MEM_ARGS="-Xms1024m -Xmx4096m"
# Export and restart server
$DOMAIN_HOME/bin/stopWebLogic.sh
$DOMAIN_HOME/bin/startWebLogic.sh
```

## Verify

```bash
tail -f $DOMAIN_HOME/servers/AdminServer/logs/AdminServer.log | grep -i "Server state changed to RUNNING"
```
