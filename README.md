<div align="center">
  <img src="favicon.svg" width="80" alt="agents logo"/>

  # agents

  Reusable Claude Code GitHub Actions workflows.
  Any repo can call an agent in ~8 lines — no copy-pasting workflows.
</div>

---

## Quick Start

**1. Add `ANTHROPIC_API_KEY` as a secret** in your repo or org:
`GitHub → Settings → Secrets → Actions → New secret`

**2. Create a caller workflow** in your repo for each agent you want:

```yaml
# .github/workflows/lint.yml
name: 🧹 Claude Lint & Format

on:
  workflow_dispatch:

jobs:
  lint:
    uses: lorenzomagnino/agents/.github/workflows/claude-lint.yml@main
    secrets: inherit
```

**3. Run it** from `Actions → Claude Lint & Format → Run workflow`.

The agent checks out your code, runs the task, writes a report to `reports/`, and opens a PR.

---

## How it works

- `uses:` points to a reusable workflow in this repo — no code is copied to your repo
- `secrets: inherit` passes your secrets to the agent:
  - `ANTHROPIC_API_KEY` — authenticates Claude
  - `GITHUB_TOKEN` — auto-injected by GitHub; lets the agent create branches and PRs **in your repo**

---

## Agents

| Workflow | What it does | Inputs |
|---|---|---|
| `claude-structure.yml` | Fix project layout, missing `__init__.py`, misplaced files | — |
| `claude-lint.yml` | ruff, mypy, pre-commit, dead code removal | — |
| `claude-config.yml` | Migrate hardcoded values to Hydra config | — |
| `claude-docker.yml` | Add/fix Dockerfile with multi-stage build | — |
| `claude-tests.yml` | Fix failing tests, scaffold missing ones | — |
| `claude-perf.yml` | Vectorization, JIT, CPU/GPU portability, parallelism | `target_file` |
| `claude-network.yml` | Neural network review and smoke tests | — |
| `claude-flamegraph.yml` | Profile with py-spy/scalene/memray, then analyse | `script`, `duration` |

---

## Agents with inputs

```yaml
# Optimize a specific file (omit target_file to scan all of /src/)
jobs:
  perf:
    uses: lorenzomagnino/agents/.github/workflows/claude-perf.yml@main
    with:
      target_file: 'src/train.py'
    secrets: inherit
```

```yaml
# Flamegraph a specific script
jobs:
  flamegraph:
    uses: lorenzomagnino/agents/.github/workflows/claude-flamegraph.yml@main
    with:
      script: 'src/main.py'    # default: src/main.py
      duration: '60'           # profiling duration in seconds, default: 30
    secrets: inherit
```

---

## What every agent follows

All agents share a common ruleset (`.github/prompts/_global.md`):

- KISS principle — simplest solution that works
- PEP8, max line length 88
- No inline comments; Google-style docstrings on public functions
- Minimal diffs — only change what the task requires
- Run `pytest tests/ -v` after any code change and fix regressions before opening the PR
- Write a report to `reports/<agent>-report.md` before opening the PR
- Open a PR with the report as the body

---

## Requirements

- `ANTHROPIC_API_KEY` set as a repo or org secret
- This repo must remain **public** (required for the prompt checkout step inside each workflow)
