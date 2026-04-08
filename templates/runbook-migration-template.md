---
id: RBK-XXXX
type: runbook
title: <Platform/Service Migration Guide>
domain: <argocd|appservice|aca|podman|weblogic>
platforms: [<from>+<to>]
severity: sev-3
status: <draft|published>
owner: <team>
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [migration, onboarding, step-by-step]
related_ids: []
error_signatures: []
---

# Runbook: <Title>

## Summary

High-level overview of what this migration accomplishes.

## Prerequisites

Before starting, ensure you have:
- [ ] Checklist item 1
- [ ] Checklist item 2
- [ ] Access to X service

## Step-by-Step Migration

### Phase 1 — <Phase Name>

**Step 1: <Description>**
- [ ] Subtask 1
- [ ] Subtask 2

```bash
# Command to execute
```

**Verify:**
```bash
# Command to verify completion
```

Expected output: ...

---

### Phase 2 — <Phase Name>

**Step 2: <Description>**
- [ ] Subtask 1
- [ ] Subtask 2

```bash
# Command to execute
```

**Verify:**
```bash
# Command to verify completion
```

Expected output: ...

---

## Post-Migration Validation

Run this final checklist to confirm the migration is complete:

```bash
# Final validation commands
```

Expected results:
- Service is running in target platform
- No errors in logs
- Health checks pass

## Rollback

If anything goes wrong:

```bash
# Rollback commands
```

## Common Issues

| Error | Cause | Fix |
|---|---|---|
| Error message | Why it happens | How to fix it |

## Related Artifacts

- Related Incident:
- Related Doc Gap:
- Related Runbook:
