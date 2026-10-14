---
name: ctl-eng-rfc
description: "Interactive RFC and Scope Freeze for features, refactors, and systems work. Defines explicit Problem, Goals, Non-Goals, and Technical Constraints before any code or architecture is designed. Enforces a human approval checkpoint."
argument-hint: "[optional: feature or change description]"
---

# Gate 0: Interactive RFC & Scope Freeze

**Outcome**: A frozen 1-page Request for Comments (RFC) establishing the exact problem statement, measurable goals, strict non-goals, and repository constraints.

## Invariants & Rules
1. **Never write code or architecture in this skill**: Clarify *what* problem is being solved and *what is explicitly out of scope* before deciding *how* to build it.
2. **Explicit Non-Goals are mandatory**: A feature scope is defined as much by what it rejects as what it includes. You must list at least 2 explicit non-goals.
3. **Respect Repository Rules**: Inspect local project instructions (`AGENTS.md`, `GEMINI.md`, `CLAUDE.md`) to extract existing constraints (e.g. zero new dependencies, flat functions, minimal diffs).

## Workflow

### Step 1: Context & Constraint Gathering
1. Read the user's prompt and examine any referenced files or modules.
2. Inspect the repository root for:
   - `AGENTS.md` / `GEMINI.md` / `CLAUDE.md` (for coding standards, minimalism rules, dependency policies).
   - `pyproject.toml` / `package.json` / `Cargo.toml` (for current dependencies and runtime versions).
3. If the user's request is underspecified, formulate 1–3 targeted questions to clarify the core objective and constraints. Use the host's blocking question tool if available, or present clear choices in chat.

### Step 2: Draft the 1-Page RFC
Draft the RFC adhering to the standard template (`templates/rfc-template.md`):
- **Problem Statement**: What deficiency or need exists?
- **Goals**: 2–4 concrete, verifiable outcomes.
- **Non-Goals**: Explicit boundaries (features, premature optimizations, or speculative flexibility deliberately rejected).
- **Technical Constraints**: Runtime environment, dependency boundaries, architectural style.

### Step 3: Present and Request Human Sign-off
Present the RFC draft clearly in chat or propose saving to `docs/rfc/YYYY-MM-DD-<feature-slug>-rfc.md` (or the project's documentation root).

Prompt the human for sign-off:
> "RFC draft ready for review. Do the goals and non-goals accurately reflect your intent before we proceed to architectural design?"

**STOP HERE**. Do not proceed to architecture or implementation until the user affirms the scope.
