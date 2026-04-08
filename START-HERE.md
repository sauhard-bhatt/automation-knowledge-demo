# Start Here

Answer one question: **which situation are you in?**

---

## Situation A — "I am deploying for the first time and something is missing"

You followed the deployment steps but hit an error. A prerequisite was never done. Before raising a ticket to DevOps, ask yourself:

> **Was this step in my onboarding / deployment guide?**

### A1 — The step was in the guide but I skipped it

The documentation covered it. The step was missed during execution. In most cases for ArgoCD+AKS, the step still requires DevOps to action (namespace creation, cluster registration, RBAC) — but your request to them should reference that the step was already in the guide.

**Copilot prompt:**
> `I am deploying [service] to [platform] for the first time. I get [paste exact error]. The step may have been in our onboarding guide but was not done. What do I need to ask DevOps to action?`

### A2 — The step was never in any guide

True documentation gap. DevOps needs to action the setup AND the onboarding guide needs to be updated so the next team doesn't hit the same issue.

**Copilot prompt:**
> `I am deploying [service] to [platform] for the first time. I get [paste exact error]. This step does not appear in our onboarding guide. What prerequisite is missing, who owns it, and what should be added to the docs?`

### Either way — go here first:

**Go to:** [indexes/doc-gaps-index.md](indexes/doc-gaps-index.md)

Each entry has a forked section: "If the step was documented" vs "If the step was never documented" — both paths tell you exactly what to ask DevOps and what to verify.

---

## Situation B — "This pipeline was working. Today it failed."

You have a previously stable deployment that is now producing an error. Something changed — a config value, a permission, a cluster state. This is a **regression**: you need root cause and a fix.

**Go to:** [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md)

Match your platform and error pattern. Each row gives you:
- Direct fix command
- Link to full incident with verify step

**Copilot prompt pattern:**
> `[paste exact error text]`

Copilot will return Fix + Verify only. No explanation unless you ask.

---

## Situation C — "How do I migrate my service to [platform]?" or "How do I adopt [technology]?"

You need step-by-step guidance for a major infrastructure change: moving from one platform to another, or adopting a new deployment tool. These are **multi-step runbooks with embedded checklists** so you can track progress.

**Examples:**
- "How do I migrate my service from Podman to AKS with ArgoCD?"
- "How do I move my existing AKS deployment to be managed by ArgoCD?"
- "How do I transition my monolith to microservices on AKS?"

**Go to:** [indexes/runbooks-index.md](indexes/runbooks-index.md)

Find the migration/adoption runbook matching your scenario. Each runbook has:
- Prerequisites checklist
- Phase-by-phase steps with inline checkboxes
- Verification commands after each phase
- Rollback instructions
- Common issues reference

**Copilot prompt pattern:**
> `How do I [migrate service from X to Y] / [adopt technology Z] on [platform]?`

**Examples:**
> `How do I migrate my service from Podman to AKS with ArgoCD?`  
> `How do I move my existing AKS service to be managed by ArgoCD?`

Copilot will return:
- Prerequisites to check off
- Phase-by-phase steps with embedded checklist
- Commands to run
- How to verify at each step

---

## Quick Reference

| I want to… | Go to |
|---|---|
| Find what prereq I'm missing (first deploy) | [indexes/doc-gaps-index.md](indexes/doc-gaps-index.md) |
| Find the fix for a broken pipeline | [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md) |
| Step-by-step migration / adoption guide | [indexes/runbooks-index.md](indexes/runbooks-index.md) |
| Browse all incidents by platform | [indexes/by-platform.md](indexes/by-platform.md) |
| Copy-paste fix for known error | [QUICK-FIX-PLATFORM.md](QUICK-FIX-PLATFORM.md) |
| See Copilot prompt examples | [indexes/copilot-query-examples.md](indexes/copilot-query-examples.md) |
