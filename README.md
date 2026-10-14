# Controlled Engineering: Controlled Agent SDLC (CASDLC)

A software engineering-grounded framework and skill toolkit for AI coding agents. Designed for **total human control, deep explainability, and zero black-box magic**.

Unlike autonomous agent loops that modify multiple files without explanation or speculative frameworks that pile on premature abstractions, **Controlled Engineering** translates classic software engineering discipline into deterministic agent gates.

---

## 🏛 The 6 SDLC Gates

| Gate | Skill | Trigger | Deliverable & Contract |
| :--- | :--- | :--- | :--- |
| **Orchestrator** | `/ctl-eng` | Any stage / status check | Smart assessment and lifecycle routing |
| **0. Scope Freeze** | `/ctl-eng-rfc` | Starting a feature or refactor | 1-page RFC defining Problem, Goals, and strict **Non-Goals**. Human signs off on scope before code. |
| **1. Architecture Decision** | `/ctl-eng-adr` | Technical forks or structural choices | 1-page ADR comparing 2–3 concrete options with explicit tradeoffs and human veto. |
| **2. Verification Contract** | `/ctl-eng-verify` | Pre-implementation | Executable test commands, assertion matrix, and failure traps defined upfront (strict TDD). |
| **3. Checkpoint & Explain** | `/ctl-eng-checkpoint` | Implementation execution | Atomic units (<150 lines diff) with a mandatory **Pre-Generation Audit** and human sign-off per unit. |
| **4. Static Analysis & CI** | `/ctl-eng-audit` | Post-implementation | Project-native test runner, linter, and type checker execution producing an objective scorecard. |
| **5. Knowledge Compounding** | `/ctl-eng-compound` | Feature completion | High-signal, non-redundant learnings updating repo rules (`AGENTS.md`) without doc rot. |

---

## 📦 Installation & Distribution

This plugin is designed to be version-controlled and published on GitHub.

### Option 1: Global Installation (All Projects)
Clone into your global Antigravity/Gemini configuration directory:
```bash
git clone https://github.com/<your-username>/controlled-engineering.git ~/.gemini/config/plugins/controlled-engineering
```

### Option 2: Project-Local Installation (Team / Specific Repo)
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
