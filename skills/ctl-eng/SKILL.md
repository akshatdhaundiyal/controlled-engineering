---
name: ctl-eng
description: "Master orchestrator and lifecycle guide for Controlled Engineering (CASDLC). Inspects current project state, identifies active stage, and routes to the appropriate SDLC gate (RFC, ADR, Verify, Checkpoint, Audit, Compound)."
argument-hint: "[optional: feature description, stage question, or status check]"
---

# Controlled Engineering (`ctl-eng`): Master Orchestrator

**Outcome**: High-transparency orchestration across the 6 Controlled Agent SDLC gates. Keeps the human engineer completely informed, in control, and equipped with rationales at every milestone.

---

## 🏛 The 6 SDLC Gates

| Gate | Command | When to Use | Core Artifact |
| :--- | :--- | :--- | :--- |
| **0. Scope Freeze** | `/ctl-eng-rfc` | Starting a feature, refactor, or new capability | 1-page RFC with explicit **Non-Goals** |
| **1. Architecture Decision** | `/ctl-eng-adr` | Evaluating technical forks or structural approaches | 1-page ADR comparing 2–3 options with human veto |
| **2. Verification Contract** | `/ctl-eng-verify` | Before implementing any code | Deterministic test commands & assertion matrix |
| **3. Checkpoint & Explain** | `/ctl-eng-checkpoint` | Executing atomic implementation units | Pre-Generation Audit (Core operation + YAGNI exclusions) |
| **4. Static Analysis & CI** | `/ctl-eng-audit` | After implementation units are written | Native test runner, linter, & type checker scorecard |
| **5. Knowledge Compounding** | `/ctl-eng-compound` | After verification passes | Surgical updates to `AGENTS.md` / `GEMINI.md` |

---

## Workflow: State Assessment & Smart Routing

When invoked as `/ctl-eng`:

### Step 1: Detect Current State
Inspect the current working directory:
1. Is there an active RFC in progress? (`docs/rfc/` or prompt discussion)
2. Has an architectural fork been decided? (`docs/adr/`)
3. Is there an active Verification Contract or test suite ready?
4. Are there pending implementation changes or unstaged git diffs?

### Step 2: Recommend the Immediate Next Gate
Present a clear, concise status summary:
- **Current Lifecycle Stage**: Where the feature or task currently stands.
- **Immediate Recommended Gate**: The specific gate to run next (e.g. `/ctl-eng-rfc` for new work, `/ctl-eng-checkpoint` for pending diffs).
- **Why**: The engineering rationale for this next gate.

### Step 3: Ask for Confirmation or Direct Dispatch
Ask the user if they wish to proceed with the recommended gate, or select another gate from the 6 options.
