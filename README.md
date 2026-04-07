# Automation Knowledge Demo

Markdown-first knowledge base for cross-platform troubleshooting: ArgoCD+AKS, App Service, ACA, Podman, WebLogic, and more.

## Entry Points

| Use Case | Go To |
|---|---|
| Pick platform, find error, copy fix | [BY-PLATFORM.md](BY-PLATFORM.md) |
| Quick fixes by platform (copy-paste) | [QUICK-FIX-PLATFORM.md](QUICK-FIX-PLATFORM.md) |
| Guided troubleshooting flow | [START-HERE.md](START-HERE.md) |
| Search by platform + error pattern | [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md) |
| All incidents by platform | [indexes/by-platform.md](indexes/by-platform.md) |
| Copilot prompt examples | [indexes/copilot-query-examples.md](indexes/copilot-query-examples.md) |

## Copilot Behavior Contract

- Decision: [ADR-0002](knowledge/decisions/decision-adr-0002-copilot-precision-response-contract.md)
- Demo use-cases: [RBK-0003](knowledge/runbooks/runbook-rbk-0003-copilot-error-query-demo.md)
- Onboarding quick steps: [RBK-0004](knowledge/runbooks/runbook-rbk-0004-platform-onboarding-quick-steps.md)

## Key Principles

- Precision-first: No fluff, exact fixes only → [PRECISION-GUIDE.md](PRECISION-GUIDE.md)
- Platform-aware: Same error, different platform, different fix
- Copy-paste ready: Commands are immediately runnable
- Machine-readable: Frontmatter enables Copilot and automation routing

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
    ├── decisions-index.md
    ├── by-platform.md
    ├── error-signatures-by-platform.md
    ├── copilot-query-examples.md
    └── tags-index.md
```

## Legacy Content

Existing folders are still valid inputs while migrating into knowledge:

- cases -> knowledge/incidents
- runbooks -> knowledge/runbooks
- doc-gaps -> knowledge/doc-gaps
- enhancement-idea -> knowledge/automations
