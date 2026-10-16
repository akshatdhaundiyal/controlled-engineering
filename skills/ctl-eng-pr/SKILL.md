---
name: ctl-eng-pr
description: "Disciplined Git commit, push, and PR authoring with explicit human checkpoints. Generates clear conventional commits, verifies branch hygiene, and crafts structured PR descriptions."
argument-hint: "[optional: PR title, commit message hint, or branch name]"
---

# Controlled Shipping (`ctl-eng-pr`): Commit, Push & PR

**Outcome**: A clean, reviewable pull request opened on GitHub with a conventional commit, zero untracked junk files, and a structured PR description grounded in the active RFC/ADR.

---

## 🛡 Invariants & Rules
1. **Never Commit Junk or Uninspected Files**: Never use `git add .` or `git add -A`. Inspect `git status -s` and stage files explicitly.
2. **Never Push Directly to Main**: If on `main` or `master` with unpushed work, automatically propose a descriptive feature branch (e.g. `feat/xyz` or `fix/xyz`).
3. **Structured PR Description**: PR bodies must state:
   - **Problem / Context**
   - **Key Changes** (bulleted)
   - **Non-Goals / Exclusions** (from RFC/ADR)
   - **Verification Evidence** (exact tests passed and command run)
4. **Human Confirmation Gate**: Always preview the commit message and PR description for human approval before pushing to the remote.

---

## Workflow

### Step 1: Pre-Commit Hygiene & Staging
1. Run `git status -s` and `git diff --stat`.
2. Ensure no scratch files, debug logs, or unwanted temporary files are present.
3. Check the current branch:
   - If on `main` or `master`: Propose creating and checking out a new branch:
     `git checkout -b <type>/<descriptive-slug>`
4. Stage only the intended files:
   `git add <file1> <file2> ...`

### Step 2: Formulate Conventional Commit
Draft a concise, conventional commit message:
```text
<type>(<scope>): <short imperative summary>

- <why this change was made>
- <what was deliberately excluded or modified>
```

Present the proposed commit message and staged file list to the user:
> "Ready to commit [N] files with message:
> `<commit message>`
> May I create this commit?"

**Checkpoint**: Wait for human approval, then run `git commit -m "..."`.

### Step 3: Push to Remote
1. Check the remote branch tracking status.
2. Push with upstream tracking:
   `git push -u origin <branch-name>`
3. If push succeeds, proceed to Step 4. If authentication fails, report exact status.

### Step 4: Compose Structured PR Description
Using the active conversation context, RFC, and ADR, draft the PR title and description:

```markdown
## Summary & Context
<!-- 2-3 sentences explaining the problem and why this change exists -->

## Key Changes
<!-- Bullet points detailing concrete modifications -->
- 

## Deliberate Exclusions (YAGNI)
<!-- What was deliberately omitted or deferred -->
- 

## Verification Evidence
<!-- Exact command executed and test output -->
- Command: `uv run pytest tests/...`
- Result: ✅ [N] tests passed, 0 failures
```

### Step 5: Create or Update PR
1. Check if an open PR already exists for this branch:
   `gh pr list --head <branch-name> --json number,url` (if `gh` CLI available)
2. If `gh` is available:
   - Create PR: `gh pr create --title "<title>" --body "<description>"`
   - Or update existing: `gh pr edit --title "<title>" --body "<description>"`
   - Output the clickable PR URL.
3. If `gh` is not installed:
   - Print the complete PR title and Markdown description in chat.
   - Provide the direct GitHub compare link:
     `https://github.com/<owner>/<repo>/compare/<base>...<branch-name>`
4. Handoff: Offer to monitor the PR with `/ctl-eng-babysit`.
