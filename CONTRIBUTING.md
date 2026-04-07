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
- `platforms` ← **NEW: array of platforms, e.g., [argocd+aks, appservice, aca]**
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
- Include ID in link text (example: `INC-0001 Namespace Missing`).
- Add reciprocal links between related artifacts.
- Update the relevant index file for every new or updated artifact.
- Update **platform-aware** indexes: [indexes/by-platform.md](indexes/by-platform.md) and [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md).

## Precision-First Writing

- **One error signature = one incident file.**
- **Fixes are platform-specific.** Same error, different platforms, different commands.
- **No fluff.** Answer contains only information needed to resolve issue.
- No Background, History, or Context unless required for the fix.

## Pull Request Checklist

- Platform specified in frontmatter.
- Added or updated frontmatter.
- Used canonical headings.
- Added reciprocal links.
- Updated type index under `indexes/`.
- Updated platform indexes:
  - [indexes/by-platform.md](indexes/by-platform.md)
  - [indexes/error-signatures-by-platform.md](indexes/error-signatures-by-platform.md)
- Fixes are platform-specific (no one-size-fits-all commands).
