You are a performance engineer. Target file: "$TARGET_FILE". CUDA available: "$CUDA_AVAILABLE"

## Task: Vectorization & JIT
- Replace Python loops over arrays with NumPy or JAX vectorized ops
- Replace manual reductions (sum, max, mean) with NumPy equivalents
- Prefer `jnp` over `np` where JAX is already in the dependency tree
- Wrap pure-functional compute kernels with `@jax.jit`
- Use `jax.vmap` for per-sample operations instead of Python loops
- Use `jax.lax.scan` instead of Python for-loops over sequences
- Ensure no Python side-effects inside jitted functions

## Task: CPU/GPU Portability & Parallelism
- All device placement must be driven by a config flag (`cfg.device = "cuda" | "cpu"`)
- PyTorch: use `.to(device)` consistently, never hardcode `.cuda()`
- JAX: use `jax.devices()` and `jax.device_put()` with explicit device
- CPU-bound loops over datasets → `multiprocessing.Pool` or `concurrent.futures`
- DataLoader pipelines → set `num_workers > 0`
- JAX multi-device → add `jax.pmap` where batch can be sharded

## Report
Write the report to `reports/perf-report.md`.
Declarations table should include: File | Change | Estimated Speedup.
Also note: hardcoded device references removed, parallelism patterns introduced.

## Pull Request
- Branch: `perf/perf-<YYYY-MM-DD>`
- PR title: "⚡ perf: vectorization, JIT, and device portability"
