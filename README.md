# Automation Knowledge Demo

Minimal knowledge base for app dev teams who need one of three outcomes: identify a missed prerequisite, fix a broken deployment, or follow a migration/adoption guide.

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

## Key Principles

- Precision-first: keep resolution content short and actionable.
- Platform-aware: Same error, different platform, different fix
- Copy-paste ready: Commands are immediately runnable
- Machine-readable: Frontmatter enables Copilot and automation routing
- Migration-ready: Step-by-step runbooks with embedded checklists

## Canonical Information Architecture

```text
.
├── README.md
├── START-HERE.md
├── templates/
│   ├── incident-template.md
│   ├── runbook-migration-template.md
│   └── doc-gap-template.md
├── knowledge/
│   ├── incidents/
│   ├── runbooks/
│   └── doc-gaps/
└── indexes/
    ├── runbooks-index.md
    ├── doc-gaps-index.md
    └── error-signatures-by-platform.md
```
