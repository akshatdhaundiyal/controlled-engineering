---
name: eng-audit
description: "Repository-native static analysis, lint, and full test suite verification gate. Executes linters, type-checkers, and test suites, compiling a clean, objective quality scorecard."
argument-hint: "[optional: audit target or full]"
---

# Gate 4: Static Analysis & CI Verification Gate

**Outcome**: An objective Quality Scorecard confirming that all tests pass, types are valid, linters are satisfied, and git diffs are clean and free of leftover debugging artifacts.

## Invariants & Rules
1. **Never suppress lint or type errors with hacks**: Fix the underlying issue cleanly or adhere to documented project exemptions.
2. **Deterministic Tooling**: Run the repository's native verification scripts or package commands directly.
3. **Diff Cleanliness**: Verify `git status` and `git diff` to ensure no temporary scratch files, debug `print()` statements, or unintended file mutations exist.

## Workflow

### Step 1: Execute Native Quality Checks
Run each of the following configured for the project (adjusting for language environment):
1. **Test Suite**: Run full or scoped tests (e.g., `uv run pytest tests/`).
2. **Linter**: Run code style/linter (e.g., `uv run ruff check .` or `npm run lint`).
3. **Type Checker**: Run static type verification (e.g., `uv run mypy .` or `npm run typecheck`).

### Step 2: Inspect Git Diff & Working Tree
1. Run `git status -s` to verify only intended files were modified.
2. Check for leftover console logs, temporary comments, or unused imports.

### Step 3: Compile and Present Quality Scorecard
Format a clean markdown table presenting the audit results:

```markdown
### 📋 Quality Scorecard
| Check | Tool / Command | Result | Notes |
| :--- | :--- | :--- | :--- |
| **Unit & Integration Tests** | `[test command]` | ✅ PASS | [N] passed in [X]s |
| **Lint & Code Style** | `[lint command]` | ✅ PASS | 0 errors |
| **Static Type Analysis** | `[type command]` | ✅ PASS | 0 errors |
| **Working Tree Cleanliness** | `git status` | ✅ PASS | Only intended files modified |
```

If all checks pass, hand off to Gate 5 (Knowledge Compounding). If any check fails, stop and diagnose the root cause cleanly.
