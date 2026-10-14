---
name: eng-verify
description: "Test-Driven Verification Contract generator. Establishes exact shell commands, acceptance criteria, invariant matrices, and failure traps before implementation begins."
argument-hint: "[optional: target feature or component]"
---

# Gate 2: Executable Verification Contract (Test-First Spec)

**Outcome**: An unambiguous Verification Contract detailing exact shell commands, input/output invariants, and negative test traps that will validate the implementation.

## Invariants & Rules
1. **Verification Before Code**: Every feature, refactor, or fix must have an objective, runnable definition of "Done" *before* modifying production code.
2. **Deterministic Shell Commands**: Commands must run natively in the repository without manual environment setup (e.g., `uv run pytest tests/test_foo.py -v`).
3. **No Speculative Test Frameworks**: Reuse existing test packages and fixtures already in the repo; do not introduce new assertion libraries.
4. **No Production Code Mock Polluting**: Never pollute core production classes with test-only mocks or OS hacks.

## Workflow

### Step 1: Inspect Test Harness & Environment
1. Inspect the repository for its test runner:
   - Python: `pyproject.toml` (pytest, unittest), virtual environment commands (`uv run`, `poetry run`, `pytest`).
   - Node: `package.json` (`npm test`, `pnpm test`, `vitest`, `jest`).
   - Rust: `Cargo.toml` (`cargo test`).
2. Identify existing test files related to the target component.

### Step 2: Author the Invariant Matrix
Define 2–5 concrete test cases covering:
- **Happy Path Invariant**: The primary expected behavior and output schema.
- **Boundary / Edge Conditions**: Empty strings, nulls, zero values, or high concurrency.
- **Negative Scenarios**: Expected explicit exceptions or error messages.
- **Regression Traps**: Known failure modes from past bugs or complex interactions.

### Step 3: Draft Verification Contract
Using `templates/verification-contract-template.md`:
- List the exact runnable shell command.
- Present the table of Test Cases (TC-01, TC-02...).
- Specify the target test file to create or extend.

### Step 4: Human Sign-Off
Present the verification matrix to the user:
> "Verification Contract defined:
> - Command: `<exact test command>`
> - Test Cases: [TC-01, TC-02, ...]
> Do these test conditions comprehensively cover acceptance, or should any edge cases be added?"

**STOP HERE**. Secure user confirmation on the verification criteria before moving to implementation.
