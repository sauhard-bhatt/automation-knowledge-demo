# Automation Knowledge Demo

Markdown-first knowledge base for ArgoCD troubleshooting, runbook quality, and future remediation automation.

## Quick Start

**Got an ArgoCD error?** → [START-HERE.md](START-HERE.md)

**Want copy-paste fixes?** → [QUICK-FIX.md](QUICK-FIX.md)

**Want complete incident details?** → [knowledge/incidents/](knowledge/incidents/)

---

## Goals

- Keep operational knowledge human-readable and machine-parseable.
- Make incident retrieval deterministic for GitHub Copilot.
- Enable future automation by linking signatures to runbooks and automation hooks.
- **Precision-first answers: no fluff, exact fixes.** → [PRECISION-GUIDE.md](PRECISION-GUIDE.md)

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
