<div align="center">
  <img src="favicon.svg" width="80" alt="agents logo"/>

  # agents

  Reusable Claude Code GitHub Actions workflows.
  Any repo can call an agent in ~5 lines — no copy-pasting workflows.
</div>

---

## Usage

Add a caller workflow to any consumer repo:

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

For agents that accept inputs:

```yaml
jobs:
  vectorize:
    uses: lorenzomagnino/agents/.github/workflows/claude-vectorize.yml@main
    with:
      target_file: 'src/train.py'
    secrets: inherit
```

## Agents

| Workflow | Description | Inputs |
|---|---|---|
| `claude-structure.yml` | Fix project layout, missing `__init__.py`, misplaced files | — |
| `claude-lint.yml` | ruff, mypy, pre-commit, dead code removal | — |
| `claude-config.yml` | Migrate hardcoded values to Hydra config | — |
| `claude-docker.yml` | Add/fix Dockerfile with multi-stage build | — |
| `claude-tests.yml` | Fix failing tests, scaffold missing ones | — |
| `claude-vectorize.yml` | Replace loops with NumPy/JAX, add `@jax.jit` | `target_file` |
| `claude-device.yml` | CPU/GPU portability, parallelism | — |
| `claude-network.yml` | Neural network review and smoke tests | — |
| `claude-flamegraph.yml` | Profile with py-spy/scalene/memray, then analyse | `script`, `duration` |

## Requirements

- `ANTHROPIC_API_KEY` set as an org or repo secret
- This repo must be **public** (used for the prompt checkout)
