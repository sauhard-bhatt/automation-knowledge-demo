# Copilot Query Examples

Use these prompts to validate precise response behavior.

## Error-only Prompt

Prompt:
`cluster "Customer-Service-prod" not found`

Expected shape:
- `Fix`
- `Verify`

Reference:
- [RBK-0003](../knowledge/runbooks/runbook-rbk-0003-copilot-error-query-demo.md)

## Root-Cause Prompt

Prompt:
`For cluster "Customer-Service-prod" not found give likely root cause and fix`

Expected shape:
- `Likely Root Cause`
- `Confirm`
- `Fix`

Reference:
- [ADR-0002](../knowledge/decisions/decision-adr-0002-copilot-precision-response-contract.md)

## Onboarding Prompt

Prompt:
`How to onboard service to ArgoCD on AKS?`

Expected shape:
- `Steps`

Reference:
- [RBK-0004](../knowledge/runbooks/runbook-rbk-0004-platform-onboarding-quick-steps.md)
