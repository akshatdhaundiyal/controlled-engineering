---
name: ctl-eng-checkpoint
description: "Atomic unit implementation executor enforcing the 'Checkpoint & Explain' protocol. Requires a mandatory Pre-Generation Audit (Core operation, Deliberate exclusions, Diff preview) and human approval before touching disk."
argument-hint: "[optional: unit number or description]"
---

# Gate 3: Atomic Unit Execution ("Checkpoint & Explain" Loop)

**Outcome**: Controlled, atomic implementation of changes one unit at a time. Each unit is strictly audited for minimalism and YAGNI before any file is touched, and verified immediately after.

## Invariants & Rules
1. **Never Batch Multiple Units Autonomously**: Each unit is a discrete transaction requiring human visibility.
2. **Mandatory Pre-Generation Audit**: Before editing or creating any file, present:
   - The single core operation being performed.
   - The deliberate exclusions (abstractions, helpers, defensive wrappers omitted).
   - The proposed diff preview.
3. **Diff Size Discipline**: Keep diffs minimal and targeted (<150 lines modified per unit).
4. **Immediate Verification**: Run the verification command immediately after disk write.

## Workflow

### Step 1: Scope the Atomic Unit
1. Identify the single file or tight logical pair to modify.
2. Ensure you have the active Verification Contract and ADR in context.
3. Review local repository instructions (`AGENTS.md` / `GEMINI.md`) for negative constraints.

### Step 2: Present the Pre-Generation Audit
Before invoking any file write or edit tool, format and display the audit block to the user:

```markdown
### 🛡 Pre-Generation Audit: Unit [N] - [Component / File Name]
- **Target File**: `[repo-relative/path/to/file.ext]`
- **Single Core Operation**: [1-2 sentences on what this code does]
- **Deliberate Exclusions (YAGNI Audit)**:
  - [x] No premature abstractions: [Specific base classes or interfaces excluded]
  - [x] No speculative error handling: [Excluded catch-alls/fallbacks]
  - [x] No unnecessary helpers: [Inline implementation details preserved]
  - [x] No new dependencies: [Standard library and existing packages used]
- **Proposed Diff Preview**:
  [Concise unified diff or snippet of changes]
```

### Step 3: Human Approval Gate
Ask the user:
> "Unit [N] Pre-Generation Audit ready. May I apply this change to `[target file]`?"

**STOP HERE**. Do NOT call `write_to_file` or `replace_file_content` until the user confirms.

### Step 4: Apply Change & Verify
1. Once approved, apply the edit to disk using `replace_file_content` (prefer minimal surgical edits).
2. Proactively run the unit's deterministic verification command (from Gate 2).
3. Report the exact exit code and test output.
4. If verification passes, summarize the unit and proceed to the next unit or Gate 4.
