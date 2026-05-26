---
name: pr-submission
description: >
  Prepare and submit GitHub pull requests with prior-art research, scoped
  change framing, PR body formatting, issue linking, and verification notes.
  Use whenever asked to submit, open, create, update, or polish a PR.
license: MIT
compatibility: Requires git and gh CLI for GitHub operations.
metadata:
  author: shaun-tsai
  version: "1.0"
allowed-tools: Bash(git:*) Bash(gh:*) Read Write
---

# PR Submission

Use this skill whenever creating, updating, or preparing a pull request. The
goal is to make PRs easy for maintainers to review: focused scope, clear
problem statement, prior-art research, honest verification, and no hidden
behavioral changes.

## Contract

This skill guarantees:

- Search existing issues/PRs before opening a new issue or PR.
- Keep one logical change per PR.
- Preserve unrelated local changes.
- Write a PR body that states problem, impact, implementation, scope boundary,
  investigation, testing, and risks.
- For OpenAB PRs, follow the richer style used by PR #885 where appropriate:
  `Summary`, `Before / After`, `Data Flow (ASCII)`, `Investigation`, `Changes`,
  and `Testing`.
- Never paste secrets, tokens, private keys, or raw sensitive logs into an issue
  or PR body.

## Workflow

### 1. Inspect State

Run:

```bash
git status --short
git branch --show-current
git remote -v
```

Rules:

- Do not overwrite or revert unrelated dirty work.
- If unrelated dirty files exist, leave them alone.
- If the PR requires files already dirty from someone else, inspect carefully
  and work with the changes rather than reverting them.

### 2. Prior Research

Before opening an issue or PR, search:

```bash
gh issue list -R OWNER/REPO --search "<keywords>" --limit 20
gh pr list -R OWNER/REPO --search "<keywords>" --state all --limit 20
```

For technical or ecosystem claims, also inspect primary references:

- Upstream docs/specs.
- Related PRs/issues.
- Existing implementation and tests.
- Comparable projects when relevant.

Record prior research in the PR body. Do not overclaim if evidence is weak.

### 3. Make Focused Changes

Use a branch name such as:

```text
docs/<short-topic>
fix/<short-topic>
feat/<short-topic>
```

Commit title convention:

```text
docs: <short description>
fix: <short description>
feat: <short description>
test: <short description>
refactor: <short description>
```

Keep the diff narrow. Do not bundle cleanups unless needed for the PR.

### 4. Choose PR Body Shape

Use the compact template for small docs-only changes. Use the full template for
behavioral, integration, or debugging changes.

For OpenAB or ACP-related PRs with meaningful behavior, prefer the PR #885 style
in [references/openab-pr-885-style.md](references/openab-pr-885-style.md).

## Compact PR Template

```markdown
## Summary

- <what changed>
- <why it matters>
- <what did not change / scope boundary>

## Testing

- <command or "Not run (docs-only)">

Fixes #<issue>
```

## Standard PR Template

```markdown
## Summary

- Problem: <what is broken or missing>
- Why it matters: <user/operator impact>
- What changed: <implementation summary>
- What did NOT change: <scope boundary>

## Prior Research

- Existing issues/PRs checked: <links or "none found">
- Existing code/docs checked: <files>
- External references checked: <links, if any>

## Before / After

```text
BEFORE:
<old behavior>

AFTER:
<new behavior>
```

## Changes

| File | Change |
|------|--------|
| `<path>` | <summary> |

## Testing

- <exact command>
- <manual verification>

## Risks and Mitigations

- Risk: <risk>
  - Mitigation: <mitigation>

## Compatibility / Migration

- Backward compatible? Yes/No
- Config/env changes? Yes/No
- Migration needed? Yes/No
```

## Deep Investigation Template

Use this when the PR fixes a confusing runtime issue, protocol integration,
multi-agent behavior, error handling, or infrastructure bug:

```markdown
## Summary

Closes #<issue>.

<short narrative of the user-visible problem and the root cause.>

This PR fixes the gap by:

1. <fix 1>
2. <fix 2>

## Before / After

```text
BEFORE:
<old user-visible output or behavior>

AFTER:
<new user-visible output or behavior>
```

## Data Flow (ASCII)

```text
<ASCII diagram showing where data/control/error flows before and after>
```

## Investigation

### <Reference 1>

- <finding>
- <how it informed the fix>

### <Reference 2>

- <finding>
- <how it informed the fix>

### Key Takeaway

<cross-source conclusion>

## Changes

| File | Change |
|------|--------|
| `<path>` | <change> |

## Testing

- <unit/integration/manual test>
- <what was not verified>
```

## Issue Body Template

```markdown
## Problem

<what is wrong, from the user's/operator's perspective>

## Why It Matters

<impact>

## Current Behavior

<observed behavior, logs/output if safe>

## Expected Behavior

<desired behavior>

## Prior Research

- Related issues/PRs:
- Docs/code checked:
- External references:

## Proposed Fix

<smallest safe change>

## Safety / Scope

- No secrets included.
- No unrelated behavior changes intended.
```

## PR Creation

After committing and pushing:

```bash
gh pr create -R OWNER/REPO \
  --title "<conventional commit style title>" \
  --body-file /path/to/pr-body.md
```

If an issue was opened:

- Link it with `Fixes #<issue>` when the PR fully resolves it.
- Use `Related #<issue>` when it only documents or partially addresses it.

## Anti-Patterns

- Opening a PR without searching existing issues/PRs.
- Submitting a large mixed PR with docs, refactors, and behavior changes bundled.
- Claiming a fix is verified when only the diff was inspected.
- Putting secrets or raw token-bearing logs into GitHub.
- Using shell inline PR bodies with backticks, angle brackets, or mentions that
  the shell can interpret. Write body files and pass `--body-file`.
- Saying "minor change" without explaining the user-visible effect.

