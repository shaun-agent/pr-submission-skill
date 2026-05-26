# OpenAB PR #885 Style Reference

Reference PR:

- https://github.com/openabdev/openab/pull/885

Use this style for OpenAB PRs that fix runtime behavior, protocol handling,
multi-agent routing, observability, error reporting, or infrastructure behavior.

## Shape

PR #885 used:

1. `## Summary`
2. `## Before / After`
3. `## Data Flow (ASCII)`
4. `## Investigation: ...`
5. `## Changes`
6. `## Testing`

## What Made It Good

- It began with the user-visible failure, not the implementation detail.
- It linked the issue being closed.
- It explained why the old behavior was insufficient.
- It showed before/after output.
- It used an ASCII data-flow diagram to make the control path clear.
- It researched the relevant ecosystem:
  - ACP spec behavior
  - comparable ACP clients
  - agent-side conventions
  - adjacent bugs/issues
- It summarized the cross-repo takeaway.
- It ended with exact files changed and verification.

## Reusable Pattern

```markdown
## Summary

Closes #<issue>.

<Problem in user/operator terms.>

This PR fixes both gaps:

1. <fix one>
2. <fix two>

## Before / After

```text
BEFORE:
<old behavior>

AFTER:
<new behavior>
```

## Data Flow (ASCII)

```text
<diagram>
```

## Investigation: <topic>

### <Primary source>

- <finding>

### <Comparable implementation>

- <finding>

### Key Takeaway Across Sources

<conclusion>

## Changes

| File | Change |
|------|--------|
| `path` | summary |

## Testing

- <tests>
- <manual verification>
```

## When Not To Use This Full Style

Use the compact template instead for:

- Typo fixes.
- Small docs-only clarifications.
- Dependency bumps with no behavior change.
- Mechanical formatting.

