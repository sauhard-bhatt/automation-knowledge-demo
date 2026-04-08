# Copilot Maintainer Instructions

## Goal

Use Copilot to speed up maintenance while preserving governance standards.

## Required Prompt Pattern for Maintainers

Include these constraints in admin prompts:

1. Keep user-facing response precise and actionable.
2. Follow metadata schema exactly.
3. Update the correct index when adding a new artifact.
4. Do not remove unrelated content.
5. Preserve existing ids and references.

## Mandatory Validation After Edits

- Run a repository-wide link check process if available.
- Confirm index discoverability for new artifacts.
- Confirm no legacy paths were reintroduced.

## Safety Guardrails

- Never commit credentials or secret values.
- Avoid destructive instructions without warnings.
- Prefer minimal diff edits.
