# Precision-First Documentation Guide

Every artifact follows this rule: **answer contains only information needed to resolve the issue**.

## Writing Rules

- No explanations unless required for the fix.
- No context unless required to understand severity.
- One error signature = one incident file.
- Commands are ready to copy-paste.
- Facts only; no editorial commentary.

## Answer Format

```
## Error
<exact error text>

## Fix
<command(s) to run>

## Verify
<command(s) to confirm resolution>
```

## No Section Bloat

- If Root Cause is obvious from error, omit it.
- If Prevention is not actionable now, omit it.
- Tests supersede lengthy explanations.
