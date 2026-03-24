You are a performance engineer. Target file: "$TARGET_FILE"

## Task: Vectorization & JAX/JIT
- Replace Python loops over arrays with NumPy or JAX vectorized ops
- Replace manual reductions (sum, max, mean) with NumPy equivalents
- Prefer `jnp` over `np` where JAX is already in the dependency tree
- Wrap pure-functional compute kernels with `@jax.jit`
- Use `jax.vmap` for per-sample operations instead of Python loops
- Use `jax.lax.scan` instead of Python for-loops over sequences
- Ensure no Python side-effects inside jitted functions

## Report
Write the report to `reports/vectorize-report.md`.
Declarations table should include: File | Change | Estimated Speedup.

## Pull Request
- Branch: `perf/vectorize-<YYYY-MM-DD>`
- PR title: "⚡ perf: vectorization and JIT"
