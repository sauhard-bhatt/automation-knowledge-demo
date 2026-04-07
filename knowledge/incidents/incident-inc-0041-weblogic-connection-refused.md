---
id: INC-0041
type: incident
title: Connection refused on WebLogic
domain: weblogic
platforms: [weblogic]
severity: sev-1
status: published
owner: platform-enablement
created: 2026-04-07
updated: 2026-04-07
tags: [weblogic, connectivity]
related_ids: []
error_signatures: ["Connection refused", "java.net.ConnectException: Connection refused"]
---

# Connection Refused on WebLogic

## Error

```text
java.net.ConnectException: Connection refused
```

## Fix

```bash
# Check server process:
ps -ef | grep -i weblogic
# Check listen port:
netstat -an | grep <port>
# Check server log for startup failures:
tail -f $DOMAIN_HOME/servers/AdminServer/logs/AdminServer.log
# Start server if down:
$DOMAIN_HOME/bin/startWebLogic.sh
```

## Verify

```bash
netstat -an | grep <port>
curl -I http://<host>:<port>/console
```
