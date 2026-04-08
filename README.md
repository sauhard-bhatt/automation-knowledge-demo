# Automation Knowledge Demo

Knowledge base for app dev teams deploying on ArgoCD+AKS, App Service, ACA, Podman, WebLogic, and more.

**Three use cases this repo solves:**

| Situation | Description | Go To |
|---|---|---|
| **A — Missing step (first deploy)** | You deployed for the first time and hit an error. DevOps owns a prerequisite that was never set up. | [START-HERE.md → Situation A](START-HERE.md) → [indexes/doc-gaps-index.md](indexes/doc-gaps-index.md) |
| **B — Pipeline regression** | Your pipeline was working. Today it failed. You need root cause and fix. | [START-HERE.md → Situation B](START-HERE.md) → [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md) |
| **C — Migration / adoption** | How do I move my service from platform X to Y? How do I adopt a new workflow? Step-by-step with checklist. | [START-HERE.md → Situation C](START-HERE.md) → [indexes/runbooks-index.md](indexes/runbooks-index.md) |

**Not sure which?** → [START-HERE.md](START-HERE.md)

## Entry Points

| I want to… | Go To |
|---|---|
| Find what prerequisite I'm missing (first deploy) | [indexes/doc-gaps-index.md](indexes/doc-gaps-index.md) |
| Find the fix for a broken pipeline | [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md) |
| Step-by-step migration / adoption guide with checklist | [indexes/runbooks-index.md](indexes/runbooks-index.md) |
| Browse all incidents by platform | [indexes/by-platform.md](indexes/by-platform.md) |
| Quick fixes by platform (copy-paste) | [QUICK-FIX-PLATFORM.md](QUICK-FIX-PLATFORM.md) |
| Copilot prompt examples | [indexes/copilot-query-examples.md](indexes/copilot-query-examples.md) |

## Migration Runbooks

| Scenario | Runbook |
|---|---|
| Migrate service from Podman to AKS with ArgoCD | [RBK-0005](knowledge/runbooks/runbook-rbk-0005-podman-to-aks-argocd-migration.md) |
| Adopt ArgoCD for existing AKS service (GitOps workflow) | [RBK-0006](knowledge/runbooks/runbook-rbk-0006-adopt-argocd-for-existing-aks-service.md) |

Each runbook includes:
- ✅ Prerequisites checklist
- ✅ Phase-by-phase steps with inline checkboxes
- ✅ Verification commands after each step
- ✅ Rollback instructions
- ✅ Common issues table

## Copilot Behavior Contract

- Decision: [ADR-0002](knowledge/decisions/decision-adr-0002-copilot-precision-response-contract.md)
- Demo use-cases: [RBK-0003](knowledge/runbooks/runbook-rbk-0003-copilot-error-query-demo.md)
- Onboarding quick steps: [RBK-0004](knowledge/runbooks/runbook-rbk-0004-platform-onboarding-quick-steps.md)

## Key Principles

- Precision-first: No fluff, exact fixes only → [PRECISION-GUIDE.md](PRECISION-GUIDE.md)
- Platform-aware: Same error, different platform, different fix
- Copy-paste ready: Commands are immediately runnable
- Machine-readable: Frontmatter enables Copilot and automation routing
- Migration-ready: Step-by-step runbooks with embedded checklists

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for supported platforms, file naming, required frontmatter, and admin maintenance workflow.

## Controlled Vocabulary

See [TAXONOMY.md](TAXONOMY.md) for platforms, severity, tags, and error-signature conventions.

## Canonical Information Architecture

```text
.
├── README.md
├── CONTRIBUTING.md
├── TAXONOMY.md
├── PRECISION-GUIDE.md
├── BY-PLATFORM.md
├── QUICK-FIX-PLATFORM.md
├── START-HERE.md
├── templates/
│   ├── incident-template.md
│   ├── runbook-template.md
│   ├── runbook-migration-template.md
│   ├── doc-gap-template.md
│   ├── automation-template.md
│   └── decision-template.md
├── knowledge/
│   ├── incidents/
│   ├── runbooks/
│   ├── doc-gaps/
│   ├── automations/
│   └── decisions/
└── indexes/
    ├── incidents-index.md
    ├── runbooks-index.md
    ├── automations-index.md
    ├── doc-gaps-index.md
    ├── decisions-index.md
    ├── by-platform.md
    ├── error-signatures-by-platform.md
    └── copilot-query-examples.md
```
