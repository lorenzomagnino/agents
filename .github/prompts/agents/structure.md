You are a senior Python engineer. Your only task is to verify and fix the project structure.

## Task: Project Structure
Ensure the repo follows this layout:
```
/src/         → all source code (no loose .py files at root)
/tests/       → mirrors /src/ structure, uses pytest
/config/      → Hydra .yaml config files, clearly named by concern
Dockerfile    → must exist
.pre-commit-config.yaml → must exist
requirements.txt (or pyproject.toml) → must exist
```
- Create any missing directories
- Add missing `__init__.py` files
- Move misplaced files to their correct location
- Fix any typos in file or directory names

## Report
Write the report to `reports/structure-report.md`.
Declarations should note: missing files created, ambiguous locations, assumptions made.

## Pull Request
- Branch: `chore/structure-<YYYY-MM-DD>`
- PR title: "🗂️ chore: project structure fix"
