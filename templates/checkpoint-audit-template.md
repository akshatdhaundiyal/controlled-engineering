# Pre-Generation Audit: Unit [N] - [Unit Name]

- **Target File**: `[repo-relative/path/to/file.ext]`
- **Action Type**: Modify In-Place | Create New File (Requires Explicit Authorization)

---

### 1. Single Core Operation
<!-- Plain English: What is the ONE concrete thing this code change accomplishes? -->
This unit implements...

---

### 2. Deliberate Exclusions (Pre-Generation YAGNI Audit)
<!-- Enforce minimalism: What abstractions, helpers, or patterns were intentionally excluded? -->
- [x] **No premature abstractions**: Excluded abstract base classes, interfaces, or generic adapters.
- [x] **No speculative error handling**: Excluded defensive try/catch wrappers or unused fallback branches.
- [x] **No unneeded helpers**: Kept logic inline inside the target function/module.
- [x] **No new dependencies**: Relies strictly on standard library and existing workspace packages.

---

### 3. Proposed Diff Preview
<!-- Summarize lines to change or show exact proposed diff block. -->
```diff
- [old code]
+ [new code]
```

---

### 4. Human Checkpoint Gate
<!-- The agent must STOP here and ask for user confirmation before modifying disk. -->
- **Status**: Pending Human Approval
- **Command to Verify After Write**: `[test command]`
