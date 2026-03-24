You are a performance engineer. CUDA available: "$CUDA_AVAILABLE"

## Task: CPU/GPU Portability & Parallelism
- All device placement must be driven by a config flag (`cfg.device = "cuda" | "cpu"`)
- PyTorch: use `.to(device)` consistently, never hardcode `.cuda()`
- JAX: use `jax.devices()` and `jax.device_put()` with explicit device
- CPU-bound loops over datasets → `multiprocessing.Pool` or `concurrent.futures`
- DataLoader pipelines → set `num_workers > 0`
- JAX multi-device → add `jax.pmap` where batch can be sharded

## Report
Write the report to `reports/device-report.md`.
Declarations should note: hardcoded device references removed, parallelism patterns introduced.

## Pull Request
- Branch: `perf/device-<YYYY-MM-DD>`
- PR title: "🖥️ perf: device portability and parallelism"
