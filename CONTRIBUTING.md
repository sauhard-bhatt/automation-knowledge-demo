# Contributing Guide

## Scope

This repository is a Markdown-first operational knowledge graph for cross-platform troubleshooting (ArgoCD, App Service, ACA, Podman, WebLogic, etc).

## Supported Platforms

- `argocd+aks`
- `appservice`
- `aca` (Azure Container Apps)
- `podman`
- `weblogic`
- More platforms welcome

## Artifact Types

- Incident: a specific failure pattern with evidence and resolution.
- Runbook: repeatable triage and remediation workflow.
- Doc Gap: missing or unclear platform documentation that caused operational friction.
- Automation: proposal or implementation-ready design to prevent or auto-remediate failures.
- Decision: architecture record for standards in this repository.

## Canonical Folder Layout

- `knowledge/incidents/`
- `knowledge/runbooks/`
- `knowledge/doc-gaps/`
- `knowledge/automations/`
- `knowledge/decisions/`
- `indexes/`
- `templates/`

## File Naming

- Lowercase kebab-case only.
- Prefix with type + stable ID + short slug.
- Examples:
  - `incident-inc-0001-argocd-namespace-missing.md`
  - `runbook-rbk-0001-argocd-sync-failures.md`
  - `docgap-gap-0001-onboarding-namespace-step.md`
  - `automation-aut-0001-destination-preflight-validator.md`

## Required Frontmatter Keys

All new knowledge artifacts must include:

- `id`
- `type`
- `title`
- `domain`
- `platforms` ← array of platforms, e.g., [argocd+aks, appservice, aca]
- `severity`
- `status`
- `owner`
- `created`
- `updated`
- `tags`
- `related_ids`
- `error_signatures`

## Required Body Sections

Use exact heading names:

- Summary
- Symptoms
- Error Signatures
- Root Cause
- Resolution
- Verification
- Prevention
- Automation Hooks
- Related Artifacts

## Linking Rules

- Use relative links only.
- Include ID in link text (example: INC-0001 Namespace Missing).
- Add reciprocal links between related artifacts.
- Update the relevant index file for every new or updated artifact.
- Update platform-aware indexes: [indexes/by-platform.md](indexes/by-platform.md) and [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md).

## Precision-First Writing

- One error signature = one incident file.
- Fixes are platform-specific. Same error, different platforms, different commands.
- No fluff. Answer contains only information needed to resolve issue.
- No background/history unless required for the fix.

## Admin Maintenance Workflow

1. Capture exact user error text from pipeline logs, platform logs, or onboarding blocker.
2. Determine platform (`argocd+aks`, `appservice`, `aca`, `podman`, `weblogic`).
3. Search [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md).
4. If match exists, update existing incident.
5. If no match exists, create new incident from [templates/incident-template.md](templates/incident-template.md).
6. Add direct fix and verify commands.
7. Update indexes:
   - [indexes/incidents-index.md](indexes/incidents-index.md)
   - [indexes/by-platform.md](indexes/by-platform.md)
   - [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md)
8. If issue is onboarding confusion, add/update onboarding runbook.
9. If repeatable prevention is possible, add automation artifact.

## Copilot Response Contract for This Repo

- Error-only user prompt: return `Fix` + `Verify` only.
- Root-cause request: return `Likely Root Cause`, `Confirm`, `Fix`.
- Onboarding how-to request: return numbered `Steps` only.
- If same error maps to multiple platforms, ask one platform clarifying question.

Reference: [ADR-0002](knowledge/decisions/decision-adr-0002-copilot-precision-response-contract.md)

## Pull Request Checklist

- Platform specified in frontmatter.
- Added or updated frontmatter.
- Used canonical headings.
- Added reciprocal links.
- Updated runbook/incident/decision indexes where applicable.
- Updated platform indexes:
  - [indexes/by-platform.md](indexes/by-platform.md)
  - [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md)
- Response shape remains precise per contract.
