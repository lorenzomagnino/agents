## Code Standards
- Follow the KISS principle — simplest solution that works
- Follow PEP8; max line length 88 characters
- No inline comments; use docstrings on public functions only (Google style)
- Extract repeated logic into helper functions when used 2 or more times

## Testing
- After making any code changes, run `pytest tests/ -v` to verify nothing is broken
- Fix any regressions introduced by your changes before opening the PR

## Report
Before opening the PR, write a Markdown report to `reports/<agent>-report.md`:

# <Title> Report — <YYYY-MM-DD>

## What Was Done
- bullet list of every change made

## Problems Encountered
- describe every issue found and how it was resolved

## Declarations
- anything notable (assumptions made, edge cases flagged, items skipped and why)

## Pull Request
- Create a new branch and open a PR to the default branch
- Branch: `<type>/<slug>-<YYYY-MM-DD>`
- PR title: include an emoji, type (chore/perf/fix), and a short description
- PR body: paste the full report
