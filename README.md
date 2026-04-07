# Automation Knowledge Demo

Markdown-first knowledge base for cross-platform troubleshooting: **ArgoCD+AKS, App Service, ACA, Podman, WebLogic, and more**.

## Entry Points

| Use Case | Go To |
|---|---|
| **Pick platform, find error, copy fix** | [BY-PLATFORM.md](BY-PLATFORM.md) |
| **Quick fixes by platform (copy-paste)** | [QUICK-FIX-PLATFORM.md](QUICK-FIX-PLATFORM.md) |
| **Guided 4-step troubleshooting** | [START-HERE.md](START-HERE.md) |
| **Search by platform + error pattern** | [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md) |
| **All incidents by error signature** | [indexes/error-signatures-index.md](indexes/error-signatures-index.md) |
| **All incidents by platform** | [indexes/by-platform.md](indexes/by-platform.md) |

## Key Principles

- **Precision-first:** No fluff, exact fixes only → [PRECISION-GUIDE.md](PRECISION-GUIDE.md)
- **Platform-aware:** Same error, different platform, different fix
- **Copy-paste ready:** All commands are tested and immediately runnable
- **Machine-readable:** Frontmatter enables Copilot and automation routing

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for:
- Supported platforms
- File naming rules
- Required frontmatter
- Canonical sections
- Platform-aware linking

## Controlled Vocabulary

See [TAXONOMY.md](TAXONOMY.md) for:
- Platforms list
- Severity levels
- Tag families
- Error signature format

## Canonical Information Architecture

```text
.
├── README.md
├── CONTRIBUTING.md
├── TAXONOMY.md
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
		├── doc-gaps-index.md
		├── automations-index.md
		├── tags-index.md
		└── error-signatures-index.md
```

## Legacy Content

Existing folders are still valid inputs while migrating into `knowledge/`:

- `cases/` -> `knowledge/incidents/`
- `runbooks/` -> `knowledge/runbooks/`
- `doc-gaps/` -> `knowledge/doc-gaps/`
- `enhancement-idea/` -> `knowledge/automations/`

## Naming Convention

Use lowercase kebab-case and stable IDs:

- Incident: `incident-inc-0001-argocd-namespace-missing.md`
- Runbook: `runbook-rbk-0001-argocd-sync-failures.md`
- Doc Gap: `docgap-gap-0001-onboarding-namespace-step.md`
- Automation: `automation-aut-0001-destination-preflight-validator.md`
- Decision: `decision-adr-0001-case-format-standard.md`

## Linking Convention

- Use relative Markdown links only.
- Include the artifact ID in visible link text.
- Add reciprocal links whenever two artifacts are related.
- Prefer explicit labels in each document:
	- `Related Incident:`
	- `Related Runbook:`
	- `Related Doc Gap:`
	- `Related Automation:`

## Source of Truth

- Folder-level conventions: `CONTRIBUTING.md`
- Controlled vocabulary: `TAXONOMY.md`
- Cross-document navigation: files in `indexes/`
