# Verification Contract: [Feature / Unit Name]

- **Date**: YYYY-MM-DD
- **Target Components**: [e.g. `packages/memory/retrieval.py`]
- **Associated ADR**: [Link to ADR]

---

## 1. Deterministic Verification Commands
<!-- Exact shell commands to execute. Must exit with code 0 for success. -->
```bash
# Unit test command
uv run pytest tests/test_feature.py -v

# Static analysis / lint command
uv run ruff check .
```

---

## 2. Invariants & Test Matrix

| ID | Input / Precondition | Action | Expected Output / State Change | Invariant Checked |
| :--- | :--- | :--- | :--- | :--- |
| **TC-01** | Valid query string | Call function `fn(query)` | Returns parsed result dict | Schema matches contract |
| **TC-02** | Empty / None input | Call function `fn("")` | Raises `ValueError` | Input boundary enforcement |
| **TC-03** | Concurrent calls | 10 async tasks | All complete without race | Thread safety / concurrency |

---

## 3. Negative Scenarios & Error Traps
<!-- Explicit edge cases or documented exceptions that MUST be handled. -->
- **Boundary Conditions**: 
- **Expected Exceptions**: 
- **Explicit Non-Handling (YAGNI)**: Do not wrap with catch-all `except Exception:` unless explicitly mandated.

---

## 4. Human Verification Sign-Off
- [ ] Test commands run cleanly locally.
- [ ] Invariant matrix covers critical failure modes.
- [ ] No test-only mocks or OS hacks polluting production code.
- **Signed by**: [User] | **Date**: YYYY-MM-DD
