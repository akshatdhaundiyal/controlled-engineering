# Controlled Engineering: Controlled Agent SDLC (CASDLC)

A software engineering-grounded framework and skill toolkit for AI coding agents. Designed for **total human control, deep explainability, and zero black-box magic**.

Unlike autonomous agent loops that modify multiple files without explanation or speculative frameworks that pile on premature abstractions, **Controlled Engineering** translates classic software engineering discipline into deterministic agent gates.

---

## 🏛 The SDLC Lifecycle & Debugging Suite

| Gate / Mode | Command | When to Use | Deliverable & Contract |
| :--- | :--- | :--- | :--- |
| **Orchestrator** | `/ctl-eng` | Any stage / status check | Smart state assessment and lifecycle routing |
| **0. Scope Freeze** | `/ctl-eng-rfc` | Starting a feature or refactor | 1-page RFC defining Problem, Goals, and strict **Non-Goals**. |
| **1. Architecture Decision** | `/ctl-eng-adr` | Technical forks or structural choices | 1-page ADR with **Red-Team Lenses** (YAGNI, Skeptic, Maintainability) & human veto. |
| **2. Verification Contract** | `/ctl-eng-verify` | Pre-implementation | Executable test commands, assertion matrix, and failure traps (strict TDD). |
| **Implementation Plan** | `/ctl-eng-plan` | Durable multi-unit roadmaps | Full plan in `docs/plans/` synthesizing Scope, ADR, and Test matrix. |
| **3. Checkpoint & Explain** | `/ctl-eng-checkpoint` | Implementation execution | Atomic units (<150 lines diff) with **Pre-Generation Audit** + **Simplification Pass**. |
| **4. Static Analysis & CI** | `/ctl-eng-audit` | Post-implementation | Project-native test runner, linter, and type checker scorecard. |
| **5. Knowledge Compounding** | `/ctl-eng-compound` | Feature completion | High-signal, non-redundant learnings updating repo rules (`AGENTS.md`) without doc rot. |
| **Bug Diagnosis** | `/ctl-eng-debug` | When tests fail or bugs occur | 4-phase scientific root-cause isolation & minimal surgical patch. |
| **Commit & PR** | `/ctl-eng-pr` | Ready to ship verified changes | Conventional commit, branch hygiene check, structured PR with human sign-off. |
| **PR Babysitter** | `/ctl-eng-babysit` | Monitoring open PR to merge-ready | Reactive CI failure fix & review thread resolution; leaves merge to human. |

---

## 🔬 The 4-Phase Debugging Protocol (`/ctl-eng-debug`)

1. **Deterministic Reproduction**: Minimal failing test fixture executed natively before any production code is touched.
2. **Root-Cause Isolation**: Trace execution backward to isolate the exact line and runtime divergence.
3. **Hypothesis & Explanation Checkpoint**: Plain-English explanation of the failure mechanism presented to the human for approval.
4. **Surgical Patch & Verification**: Minimal in-place fix applied and validated with regression tests.

---

## 📦 Installation & Distribution

Controlled Engineering follows the open **Agent Skills** specification and is 100% compatible with [`skills.sh`](https://skills.sh) across coding agents (Antigravity, Claude Code, Cursor, Windsurf, Codex).

### Option 1: Install via `skills.sh` (Recommended for any Agent)
Install all skills across your agents:
```bash
npx skills add akshatdhaundiyal/controlled-engineering
```

Or install a specific skill (e.g. the master orchestrator or debugging loop):
```bash
npx skills add akshatdhaundiyal/controlled-engineering --skill ctl-eng
npx skills add akshatdhaundiyal/controlled-engineering --skill ctl-eng-debug
```

### Option 2: Global Plugin Installation (Antigravity / Gemini)
Clone into your global customization directory:
```bash
git clone https://github.com/akshatdhaundiyal/controlled-engineering.git ~/.gemini/config/plugins/controlled-engineering
```

### Option 3: Project-Local Installation (Team / Specific Repo)
Clone or add as a Git submodule inside your project's `.agents/plugins/` directory:
```bash
git submodule add https://github.com/<your-username>/controlled-engineering.git .agents/plugins/controlled-engineering
```

---

## 🔍 The "Checkpoint & Explain" Protocol

Before any code is generated or saved to disk, the agent must present an explicit **Pre-Generation Audit**:
1. **Core Operation**: A single, concrete explanation of what this unit does.
2. **Deliberate Exclusions**: Specific boilerplate, speculative helpers, unnecessary wrappers, or design patterns deliberately omitted.
3. **Diff Preview**: Exact lines added/modified.
4. **Human Veto**: The agent halts and waits for explicit human approval before applying changes.

---

## 📜 License
MIT
