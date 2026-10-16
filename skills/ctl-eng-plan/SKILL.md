---
name: ctl-eng-plan
description: "Author a comprehensive, durable implementation plan in docs/plans/ synthesizing Scope Freeze (RFC), Architecture (ADR), Verification Contract (TDD), and Atomic Units."
argument-hint: "[feature description or requirements doc path]"
---

# Controlled Implementation Plan (`ctl-eng-plan`)

**Outcome**: A durable, version-controlled implementation plan saved directly to `<repo-root>/docs/plans/YYYY-MM-DD-HHMM-<feature>-plan.md`. Serves as the verified execution roadmap for `/ctl-eng-checkpoint`.

---

## 🛡 Invariants & Rules
1. **Durable In-Repo Location**: Plans are always written to `<repo-root>/docs/plans/YYYY-MM-DD-HHMM-<feature-slug>-plan.md`. Never hide plans in ephemeral session temp folders.
2. **Mandatory Non-Goals & ADR Reference**: Every plan must state what is *out of scope* and reference existing or newly needed ADRs in `docs/adr/`.
3. **Executable Verification Contract**: Every plan must include the exact test commands and invariant matrix that define "Done".
4. **Human Review Checkpoint**: The plan must be reviewed and affirmed by the user before any implementation begins.

---

## Workflow

### Step 1: Synthesize Scope & Constraints (Gate 0)
1. Read the user's requirements or feature description.
2. Check `AGENTS.md` / `GEMINI.md` for repo-level constraints (e.g. minimalism, YAGNI, existing dependencies).
3. Identify:
   - Problem statement & core goals.
   - **Strict Non-Goals** (at least 2 explicit boundaries).

### Step 2: Architecture & ADR Reference (Gate 1)
1. Inspect existing ADRs in `docs/adr/`.
2. Check if this feature requires a new architectural decision or adheres to existing records (e.g., ADR-001).
3. If an architectural fork exists, propose drafting an ADR via `/ctl-eng-adr`.
4. Document deliberate anti-patterns and boilerplate excluded.

### Step 3: Define Executable Verification Contract (Gate 2)
1. Determine the exact test commands (`uv run pytest tests/...`).
2. Draft the Invariant & Test Case Matrix (happy path, boundaries, negative traps).

### Step 4: Break Down Atomic Implementation Units (Gate 3)
Break the work into small, reviewable units (<150 lines diff each):
- **Unit 1**: Target file, single core operation, deliberate exclusions, verification check.
- **Unit 2**: Target file, single core operation, deliberate exclusions, verification check.
- **Unit N**: Final integration check.

### Step 5: Save & Present Plan Document
1. Compute filename: `docs/plans/YYYY-MM-DD-HHMM-<feature-slug>-plan.md` using current local wall-clock time.
2. Write the file cleanly to disk.
3. Present the plan summary and clickable link to the user:
   > "Implementation plan ready at `docs/plans/YYYY-MM-DD-HHMM-<feature-slug>-plan.md`.
   > Does this execution roadmap look good to begin Unit 1 via `/ctl-eng-checkpoint`?"
