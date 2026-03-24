You are a performance analysis expert. Profiling data has just been collected for this codebase.
Profiled script: "$TARGET_SCRIPT"

Profiling artifacts are in `./profiling_output/`:
- `flamegraph.svg`         → py-spy speedscope flamegraph
- `pyinstrument.html`      → wall-time call tree
- `scalene_report.html`    → CPU/memory line-by-line breakdown
- `memray_flamegraph.html` → memory allocation flamegraph

## Task: Profiling Analysis

### 1. Read & Analyse the Source
- Read the profiled script and all files it imports from `/src/`
- Read `profiling_output/scalene_report.html` for hot lines
- Read `profiling_output/pyinstrument.html` for slow call stacks

### 2. Identify Bottlenecks
Find the top 5 bottlenecks. For each one, document:
- **Location**: file + line number + function name
- **Cost**: % of total CPU time or memory
- **Root cause**: e.g. "Python loop over 10k items that could be vectorized"
- **Severity**: Critical / High / Medium / Low

### 3. Memory Analysis
- Identify the top 3 memory allocations by size
- Flag any memory leaks (allocations that grow unbounded)
- Identify large tensors kept in memory longer than needed

### 4. Report
Write `profiling_output/PERFORMANCE_REPORT.md` with these sections:

# Performance Report — <script name> — <YYYY-MM-DD>

## Executive Summary
2–3 sentences: overall health, biggest single win available.

## Flamegraph Interpretation
Plain-English explanation. Table of top 5 hot functions with % CPU time.

## Top Bottlenecks
For each:
### [#N] <function_name> in <file>:<line>
- **Cost**: X% CPU / Y MB
- **Root cause**: ...
- **Recommended fix**: concrete code suggestion (before/after if possible)
- **Estimated speedup**: Nx (conservative) — Nx (optimistic)

## Memory Report
- Peak memory usage: X MB
- Top allocations: table with location / size / lifetime
- Leaks detected: yes/no + details

## Recommended Action Plan
Ordered by impact/effort ratio.

## Profiling Commands
Shell commands to re-run each profiler locally.

## Pull Request
- Commit only `profiling_output/PERFORMANCE_REPORT.md` and the `.svg`/`.html` files
- Branch: `perf/flamegraph-report-<YYYY-MM-DD>`
- PR title: "🔥 perf: flamegraph report — <script name>"
- PR body: paste the Executive Summary
