---
name: ctl-eng-adr
description: "Lightweight Architecture Decision Record (ADR) generator and tradeoff analyzer. Evaluates 2-3 concrete options, documents deliberate anti-pattern exclusions, and enforces an explicit human architectural veto before implementation."
argument-hint: "[optional: architectural decision title or dilemma]"
---

# Gate 1: Architecture Decision Record (ADR) & Tradeoff Matrix

**Outcome**: A durable 1-page Architecture Decision Record (`docs/adr/NNN-<title>.md`) comparing concrete approaches, articulating why an option is selected, documenting what was deliberately rejected, and securing the user's architectural sign-off.

## Invariants & Rules
1. **Never implement without an architectural consensus on non-trivial changes**: If a change involves more than a 10-line direct fix, evaluate whether architectural choices exist.
2. **Always include a Minimalist / Flat Option**: Option A must represent the simplest, most direct procedural/flat implementation with zero new classes or files.
3. **Document Anti-Patterns & Exclusions**: Explicitly list abstractions (e.g. Factories, Adapters, Strategy patterns, Base Classes) that were rejected under YAGNI principles.
4. **Human Veto Power**: The user must actively accept or veto the proposed decision before any test contract or code is drafted.

## Workflow

### Step 1: Discover Next ADR Sequence Number
1. Check `<repo-root>/docs/adr/` (create it if absent).
2. Scan for existing files matching `[0-9]{3}-*.md`.
3. Select the next sequential 3-digit number (e.g. `001`, `002`, `003`).

### Step 2: Formulate Concrete Alternatives & Empirical Spikes
Compare 2 to 3 realistic options:
- **Option A (Concrete / Flat / Minimal)**: Inline logic, concrete functions, standard library / existing dependencies, zero speculative indirection.
- **Option B (Modular / Pattern-Based)**: Layered abstraction, interface/strategy, separate service class. Only justify if future variability is guaranteed by requirements.
- **Empirical Spike (Bake-Off)**: When an architectural tradeoff is close or high-risk, write two isolated 30-line benchmark scripts in `scratch/` to gather real latency, memory, or diff-size metrics before deciding.

### Step 3: Stress-Test with Red-Team Lenses
Before finalizing the decision, evaluate the leading option against 3 mandatory adversarial lenses:
1. **The YAGNI Lens**: What parts of this proposal can be deleted while preserving 90% of the user value?
2. **The Skeptic Lens**: What breaks when inputs are invalid, concurrency is high, or dependencies fail?
3. **The Maintainer Lens**: In 6 months, will an engineer reading only the code understand the control flow without reading this ADR?

### Step 4: Draft the ADR Document
Using `templates/adr-template.md`, structure the ADR with:
- **Context & Problem Statement**: The exact dilemma.
- **Options Evaluated**: Clear comparison table or bullet breakdown.
- **Red-Team Assessment**: Summary of findings from the 3 adversarial lenses.
- **Decision & Rationale**: The chosen path and the explicit reasons why.
- **Consequences & Tradeoffs**: Gains and losses acknowledged upfront.
- **Deliberate Exclusions**: Patterns avoided to keep diffs small.

### Step 5: Present Checkpoint & Await Sign-Off
Save the ADR to `<repo-root>/docs/adr/NNN-<slug>.md`.

Present the decision summary and tradeoffs to the user. Ask:
> "ADR `docs/adr/NNN-<slug>.md` drafted. Do you accept this architectural approach and its tradeoffs, or would you like to veto/adjust the design?"

**STOP HERE**. Wait for human sign-off before proceeding to verification contracts or code.
