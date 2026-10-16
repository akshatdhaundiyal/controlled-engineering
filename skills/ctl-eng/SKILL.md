---
name: ctl-eng
description: "Master orchestrator and lifecycle guide for Controlled Engineering (CASDLC). Inspects current project state, identifies active stage, and routes to the appropriate SDLC gate (RFC, ADR, Verify, Checkpoint, Audit, Compound)."
argument-hint: "[optional: feature description, stage question, or status check]"
---

# Controlled Engineering (`ctl-eng`): Master Orchestrator

**Outcome**: High-transparency orchestration across the 6 Controlled Agent SDLC gates. Keeps the human engineer completely informed, in control, and equipped with rationales at every milestone.

---

## 🏛 The SDLC Lifecycle & Shipping Suite

| Gate / Mode | Command | When to Use | Core Artifact |
| :--- | :--- | :--- | :--- |
| **0. Scope Freeze** | `/ctl-eng-rfc` | Starting a feature, refactor, or new capability | 1-page RFC with explicit **Non-Goals** |
| **1. Architecture Decision** | `/ctl-eng-adr` | Evaluating technical forks or structural approaches | 1-page ADR with Red-Team Lenses & human veto |
| **2. Verification Contract** | `/ctl-eng-verify` | Before implementing any code | Deterministic test commands & assertion matrix |
| **3. Checkpoint & Explain** | `/ctl-eng-checkpoint` | Executing atomic implementation units | Pre-Generation Audit + Post-test simplification pass |
| **4. Static Analysis & CI** | `/ctl-eng-audit` | After implementation units are written | Native test runner, linter, & type checker scorecard |
| **5. Knowledge Compounding** | `/ctl-eng-compound` | After verification passes | Surgical updates to `AGENTS.md` / `GEMINI.md` |
| **Bug Diagnosis** | `/ctl-eng-debug` | When tests fail or bugs are reported | 4-phase scientific root-cause isolation & patch |
| **Commit & PR** | `/ctl-eng-pr` | Ready to ship verified changes | Conventional commit, branch push, structured PR |
| **PR Babysitter** | `/ctl-eng-babysit` | Monitoring open PR to merge-ready | Reactive CI failure fix & review thread resolution |

---

## Workflow: State Assessment & Smart Routing

When invoked as `/ctl-eng`:

### Step 1: Detect Current State
Inspect the current context and working directory:
1. **Is there an open PR needing review or with failing CI?** -> Route to `/ctl-eng-babysit`.
2. **Are all changes verified and ready to ship to GitHub?** -> Route to `/ctl-eng-pr`.
3. **Is there an active bug, error stack trace, or failing test?** -> Route immediately to `/ctl-eng-debug`.
4. **Is there an active RFC in progress?** (`docs/rfc/` or prompt discussion) -> Continue `/ctl-eng-rfc`.
5. **Has an architectural fork arisen?** (`docs/adr/`) -> Route to `/ctl-eng-adr`.
6. **Is an implementation ready to code?** -> Verify test contract with `/ctl-eng-verify`.
7. **Are there pending implementation changes or units?** -> Route to `/ctl-eng-checkpoint`.

### Step 2: Recommend the Immediate Next Gate
Present a clear, concise status summary:
- **Current Lifecycle Stage**: Where the feature or task currently stands.
- **Immediate Recommended Gate**: The specific gate to run next (e.g. `/ctl-eng-rfc` for new work, `/ctl-eng-checkpoint` for pending diffs).
- **Why**: The engineering rationale for this next gate.

### Step 3: Ask for Confirmation or Direct Dispatch
Ask the user if they wish to proceed with the recommended gate, or select another gate from the 6 options.
