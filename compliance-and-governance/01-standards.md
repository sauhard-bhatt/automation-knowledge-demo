# Standards

## Artifact Rules

1. One error signature pattern maps to one incident artifact.
2. Each incident includes clear fix and verify steps.
3. Doc-gap artifacts must identify:
- what is missing
- who owns the missing step
- what request to send
- how to verify completion
4. Migration runbooks must include:
- prerequisites checklist
- phased steps
- verification after each phase
- rollback section

## Metadata Rules

Required metadata keys for all artifacts:
- id
- type
- title
- domain
- platforms
- severity
- status
- owner
- created
- updated
- tags
- related_ids
- error_signatures

## Quality Rules

1. Commands must be copy-paste ready.
2. No ambiguous placeholders in final examples unless intentionally templated.
3. Links must be valid relative links.
4. Avoid long prose in user-facing sections.
