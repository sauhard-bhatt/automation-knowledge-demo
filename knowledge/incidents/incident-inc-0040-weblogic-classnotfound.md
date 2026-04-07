---
id: INC-0040
type: incident
title: ClassNotFoundException in WebLogic
domain: weblogic
platforms: [weblogic]
severity: sev-1
status: published
created: 2026-04-06
updated: 2026-04-06
tags: [weblogic, java, classnotfound]
error_signatures: ["ClassNotFoundException", "java.lang.ClassNotFoundException"]
---

# ClassNotFoundException in WebLogic

## Error
```
java.lang.ClassNotFoundException: <class-name>
```

## Fix
```bash
# Check server logs
tail -f $DOMAIN_HOME/servers/AdminServer/logs/AdminServer.log

# Verify JAR in classpath
ls -la $DOMAIN_HOME/lib/ | grep <jar-name>

# Or check application lib
ls -la $DOMAIN_HOME/applications/<app-name>/lib/ | grep <jar-name>

# Add missing JAR if needed
cp <jar-file> $DOMAIN_HOME/lib/

# Restart server
$DOMAIN_HOME/bin/stopWebLogic.sh
$DOMAIN_HOME/bin/startWebLogic.sh
```

## Verify
```bash
tail -f $DOMAIN_HOME/servers/AdminServer/logs/AdminServer.log | grep "Started"
```
