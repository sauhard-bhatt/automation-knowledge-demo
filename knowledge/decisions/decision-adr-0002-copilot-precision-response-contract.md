---
id: ADR-0002
type: decision
title: Copilot Precision Response Contract
domain: platform
platforms: [argocd+aks, appservice, aca, podman, weblogic]
severity: sev-4
status: published
owner: platform-enablement
created: 2026-04-07
updated: 2026-04-07
tags: [copilot, response-contract, precision]
related_ids: [RBK-0003]
error_signatures: []
---

# Decision: Copilot Precision Response Contract

## Context

The repository goal is error-first troubleshooting with concise responses for platform users.

## Decision

Copilot responses generated from this repository must follow these rules:

1. If prompt is an exact error message: respond with only `Fix` and `Verify` sections.
2. If prompt asks root cause, include `Likely Root Cause`, `Confirm`, `Fix`.
3. If prompt asks onboarding guidance, respond with numbered steps only.
4. Platform must be included in matching logic before selecting commands.
5. If same error exists on multiple platforms, Copilot must ask one clarifying question for platform.

## Mandatory Output Shapes

### Shape A: Error-only prompt

## Fix
<commands>

## Verify
<commands>

### Shape B: Root-cause request

## Likely Root Cause
<one line>

## Confirm
<commands>

## Fix
<commands>

### Shape C: Onboarding request

## Steps
1. <step>
2. <step>
3. <step>

## Consequences

- Faster and consistent responses.
- Administrators can maintain documentation without changing Copilot behavior.

## Related Artifacts

- Related Runbook: [RBK-0003](../runbooks/runbook-rbk-0003-copilot-error-query-demo.md)
- Related Runbook: [RBK-0004](../runbooks/runbook-rbk-0004-platform-onboarding-quick-steps.md)
