---
id: INC-0030
type: incident
title: Image pull failed on Podman
domain: podman
platforms: [podman]
severity: sev-1
status: published
created: 2026-04-06
updated: 2026-04-06
tags: [podman, container, image-pull]
error_signatures: ["Failed to pull image", "Error: image not found"]
---

# Image Pull Failed on Podman

## Error
```
Failed to pull image <image>: Error: image not found
Error: error pulling image: Get https://...: connecting to the docker daemon failed
```

## Fix
```bash
# Check image exists
podman image ls | grep <image>

# Or pull manually
podman pull <registry>/<image>:<tag>

# If registry auth needed
podman login <registry>

# Then pull
podman pull <registry>/<image>:<tag>

# Restart container
podman restart <container-id>
```

## Verify
```bash
podman image ls | grep <image>
podman inspect <container-id>
```
