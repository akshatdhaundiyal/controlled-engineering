---
name: ctl-eng-debug
description: "Scientific 4-phase root-cause debugging loop. Enforces deterministic reproduction, root-cause isolation, and hypothesis validation before touching any production code."
argument-hint: "[optional: failing test name, error message, or bug description]"
---

# Controlled Debugging (`ctl-eng-debug`)

**Outcome**: A verified, surgical bug fix with zero speculative edits, backed by a deterministic regression test and a clear root-cause explanation.

---

## 🔬 Core Philosophy
- **Never guess-and-check**: Modifying production code in the hope that a bug goes away is strictly forbidden.
- **No production edits without a failing test**: Every bug must be proven to exist with a reproduction fixture before any fix is attempted.
- **Explain the mechanism**: You must explain *why* the failure occurs at the byte/logic level to the human before writing the patch.

---

## The 4-Phase Debugging Protocol

### Phase 1: Deterministic Reproduction
1. Extract the minimal reproduction conditions from the error report or logs.
2. Formulate a minimal, standalone reproduction:
   - Preferred: A new or isolated failing test case (e.g. in `tests/test_regression.py` or alongside existing tests).
   - Alternative: A 10-line standalone reproduction script in `scratch/`.
3. Execute the reproduction command natively (e.g., `uv run pytest tests/test_regression.py -k test_bug -v`).
4. **Gate**: Confirm the test fails with the *exact* expected failure signature.

### Phase 2: Root-Cause Isolation
1. Trace the code path backward from the failure point.
2. Read surrounding code context — do not speculate from error messages alone.
3. Formulate the exact failure condition:
   - What was the expected invariant?
   - What was the actual runtime state / input value?
   - Which specific line or expression triggered the divergence?

### Phase 3: Hypothesis & Explanation Checkpoint
Present the diagnostic findings to the user:
```markdown
### 🔍 Root-Cause Diagnosis
- **Reproduction**: `<exact test command and failing assertion>`
- **Failing Invariant**: `<what should have happened>`
- **Observed Behavior**: `<what actually happened>`
- **Mechanism / Root Cause**: `<the exact line and why it failed>`
- **Proposed Surgical Fix**: `<the minimal lines to change>`
- **Risk Assessment**: `<any potential ripple effects>`
```

**STOP HERE**. Secure human confirmation that the explanation and proposed fix are understood before touching production code.

### Phase 4: Surgical Patch & Verification
1. Apply the minimal in-place change using surgical replacements.
2. Run the reproduction command: Confirm it now **passes**.
3. Run the broader test suite (Gate 4): Confirm **zero regressions**.
4. Offer knowledge capture (Gate 5 `/ctl-eng-compound`): If the bug revealed a subtle library trap or non-obvious invariant, record it.
