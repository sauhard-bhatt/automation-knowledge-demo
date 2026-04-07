---
id: INC-0032
type: incident
title: Volume mount denied on Podman
domain: podman
platforms: [podman]
severity: sev-2
status: published
owner: platform-enablement
created: 2026-04-07
updated: 2026-04-07
tags: [podman, volume, permissions]
related_ids: []
error_signatures: ["Volume mount denied", "permission denied", "cannot mount"]
---

# Volume Mount Denied on Podman

## Error

```text
Volume mount denied
```

## Fix

```bash
# Check host path exists and permissions:
ls -la <host-path>
# For SELinux systems, relabel volume mount:
podman run -v <host-path>:<container-path>:Z <image>:<tag>
# If needed, adjust ownership/permissions:
chmod -R 755 <host-path>
chown -R <user>:<group> <host-path>
```

## Verify

```bash
podman inspect <container-id> | grep -i Mounts -A 20
podman logs <container-id>
```
