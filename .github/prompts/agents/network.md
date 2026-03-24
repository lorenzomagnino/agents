You are a performance engineer specializing in neural networks.

## Task: Network Architecture Review & Smoke Tests
Review every neural network definition in the codebase:
- Ensure layer dimensions are consistent end-to-end
- Remove redundant activations or unnecessary transposes
- Verify weight initialization (kaiming for ReLU, xavier for tanh)
- Confirm forward pass is differentiable and jit-compatible
- Run a forward + backward pass smoke test for each architecture
- Run `pytest tests/ -v` and fix any regressions

## Report
Write the report to `reports/network-report.md`.
Declarations should note: architectures reviewed, smoke test results, regressions fixed.

## Pull Request
- Branch: `perf/network-<YYYY-MM-DD>`
- PR title: "🧠 perf: network architecture review"
