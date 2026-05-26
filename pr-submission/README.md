# pr-submission

An Agent Skill for preparing GitHub issues and pull requests with prior
research, scoped framing, and maintainer-friendly PR bodies.

## What it does

- Searches existing issues/PRs before creating new ones.
- Formats compact, standard, and deep-investigation PR bodies.
- Encodes OpenAB PR #885's richer template for protocol/runtime fixes.
- Enforces explicit testing, scope boundaries, and no-secret hygiene.

## Requirements

- `git`
- GitHub CLI `gh`
- Authenticated GitHub session

## Installation

This skill is installed at:

```bash
/Users/shauntsai/.codex/skills/pr-submission
```

## Usage

The skill activates on prompts like:

- "submit this PR"
- "open a PR for this branch"
- "create an issue and PR"
- "format the PR body"
- "prepare a PR submission"

## License

MIT

