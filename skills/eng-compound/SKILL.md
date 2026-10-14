---
name: eng-compound
description: "Durable institutional learning engine. Captures verified, non-obvious engineering insights and edge-case invariants, updating repo instructions (AGENTS.md) or docs/solutions/ without documentation rot."
argument-hint: "[optional: topic or learning summary]"
---

# Gate 5: Living Knowledge Compounding

**Outcome**: High-signal, durable capture of non-obvious discoveries, API idiosyncrasies, or architectural invariants directly into repository instructions or solutions archive, preventing future regression.

## Invariants & Rules
1. **High Signal Bar**: Only record learnings that required non-obvious debugging or represent repo-specific invariants. Reject obvious advice (e.g. "remember to import json" or "run tests").
2. **Prevent Documentation Cruft**: Prefer a single surgical bullet in `AGENTS.md` / `GEMINI.md` over creating redundant markdown files.
3. **Verify Before Recording**: Never record speculative hypotheses; only record solutions verified by passing tests or runtime execution.

## Workflow

### Step 1: Retrospective Audit
Examine the session's debugging cycles and friction points:
- Did an external library exhibit unexpected behavior or undocumented API constraints?
- Did an OS/platform-specific quirk (Windows vs Linux, PowerShell vs bash) require a workaround?
- Did an architectural decision expose a subtle race condition or invariant?

If the answer is **No** (the implementation was routine), exit cleanly:
> "No non-obvious learnings identified; skipping knowledge compounding to keep repo instructions lean."

### Step 2: Deduplication Check
1. Search `AGENTS.md`, `GEMINI.md`, and `docs/solutions/` for existing coverage of this topic.
2. If already covered, refine the existing text rather than appending a duplicate entry.

### Step 3: Record the Learning
Choose the appropriate destination:
- **Project Rule Update (`AGENTS.md` / `GEMINI.md`)**: Use when the learning dictates coding behavior across all future features (e.g. "When querying table X, always pass explicit tenant ID"). Keep it under 2 lines.
- **Durable Solution Note (`docs/solutions/YYYY-MM-DD-<topic>.md`)**: Use for deep troubleshooting or complex environment/driver configurations.

### Step 4: Confirm with User
Present the proposed addition:
> "Identified durable learning:
> `[Exact text to append]`
> Would you like to commit this to `[AGENTS.md / docs/solutions/]`?"
