# Copilot Query Examples

Two situations, two different prompts. Match your situation to the right pattern.

---

## Situation A — First Deployment / Missing Prerequisite

Use this when you are deploying for the first time and hit an error that suggests something was never set up by DevOps.

**Pattern:**
> `I am deploying [service] to [platform] for the first time. I get [paste exact error]. What prerequisite step am I missing and who needs to do it?`

**Examples:**

Prompt:
> `I am deploying my service to ArgoCD on AKS for the first time. I get: namespaces "pad-dev" not found. What prerequisite step am I missing and who needs to do it?`

Expected response shape:
- `What is missing`
- `Who owns this step`
- `What to ask them to do`
- `How to verify it is done`

Reference: [DG-0001](../knowledge/doc-gaps/docgap-dg-0001-argocd-namespace-not-preprovisioned.md)

---

Prompt:
> `I am deploying to ArgoCD for the first time. I get: cluster "Customer-Service-prod" not found. What step did I miss?`

Expected response shape:
- `What is missing`
- `Who owns this step`
- `What to ask them to do`
- `How to verify it is done`

Reference: [DG-0002](../knowledge/doc-gaps/docgap-dg-0002-argocd-cluster-not-registered.md)

---

## Situation A Sub-Question — "Was This Documented?"

Not sure if the step was in your guide or is a true gap? Ask Copilot to help you figure it out.

**Pattern:**
> `I got [error] when deploying [service] to [platform] for the first time. Was this step in my onboarding guide or is it a true documentation gap?`

**Examples:**

Prompt:
> `I got: namespaces "pad-dev" not found when deploying to ArgoCD for the first time. Was this step in my onboarding guide or is it a true gap?`

Expected response shape:
- `Quick Self-Check` — keyword search to perform in your guide
- `If found` — step was documented but skipped
- `If NOT found` — true gap, need to update docs
- `What to do next` — DevOps request with or without doc update request

Reference: [DG-0001 Quick Self-Check section](../knowledge/doc-gaps/docgap-dg-0001-argocd-namespace-not-preprovisioned.md#quick-self-check)

---

## Situation B — Pipeline Regression (Was Working, Now Broken)

Use this when a pipeline that previously worked is now failing. Paste the exact error text.

**Pattern:**
> `[paste exact error text]`

Copilot returns `Fix` + `Verify` only. No explanation unless you ask.

**Examples:**

Prompt:
> `cluster "Customer-Service-prod" not found`

Expected response shape:
- `Fix`
- `Verify`

Reference: [INC-0003](../knowledge/incidents/incident-inc-0003-destination-mismatch.md)

---

Prompt:
> `namespaces "pad-dev" not found`

Expected response shape:
- `Fix`
- `Verify`

Reference: [INC-0001](../knowledge/incidents/incident-inc-0001-namespace-missing.md)

---

## Situation C — Migration / Adoption

Use this when you need step-by-step guidance for moving services or adopting new platforms.

**Pattern:**
> `How do I [migrate/move/adopt] [service/technology] from [X] to/on [Y]?`

**Examples:**

Prompt:
> `How do I migrate my service from Podman to AKS with ArgoCD?`

Expected response shape:
- `Prerequisites` — what you need before starting (checklist)
- `Step-by-step phases` — numbered phases with sub-steps and checkboxes
- `Verification` — commands to verify each phase succeeded
- `Rollback` — how to reverse if something goes wrong
- `Common issues` — troubleshooting table

Reference: [RBK-0005](../knowledge/runbooks/runbook-rbk-0005-podman-to-aks-argocd-migration.md)

---

Prompt:
> `How do I move my existing AKS service to be managed by ArgoCD?`

Expected response shape:
- `Prerequisites checklist`
- `Phase-by-phase steps with inline checkboxes`
- `Commands to run at each step`
- `Verification after each phase`
- `Rollback instructions`

Reference: [RBK-0006](../knowledge/runbooks/runbook-rbk-0006-adopt-argocd-for-existing-aks-service.md)

---

## Root-Cause Prompt (Optional)

Use this when you want to understand why, not just how to fix.

**Pattern:**
> `For [error text] give likely root cause and fix`

Expected response shape:
- `Likely Root Cause`
- `Confirm`
- `Fix`

Reference: [ADR-0002](../knowledge/decisions/decision-adr-0002-copilot-precision-response-contract.md)
