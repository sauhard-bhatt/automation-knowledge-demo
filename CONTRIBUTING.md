# Contributing Guide

## Scope

This repository is a Markdown-first operational knowledge graph for troubleshooting and automation design.

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
- `platform`
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

## Pull Request Checklist

- Added or updated frontmatter.
- Used canonical headings.
- Added reciprocal links.
- Updated type index under `indexes/`.
- Added or updated signature mapping in `indexes/error-signatures-index.md` when relevant.
