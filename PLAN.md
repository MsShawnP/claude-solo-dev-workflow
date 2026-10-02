# claude-solo-dev-workflow — Current Work Plan

The current arc of work. Updated when the arc changes, not every session.

---

## Goal

Make this workflow usable by someone who has never coded before — clean up the repo, fix platform issues, write beginner docs, and position the unique value clearly.

## Why this arc, why now

The author wants to share this with a friend who has never coded. The audit (2026-05-16) revealed that the workflow content is strong but inaccessible to beginners — and that "complete beginner" is an uncontested niche in the AI coding workflow space.

## Tasks

### Week 1 — Foundation (enables everything else)

- [x] **Clean up repo structure** — Removed duplicate init.md and chat-project-instructions.md from root. Added "which version?" routing to README.
- [x] **Add Windows instructions** — Added Windows equivalents for all paths in README, init.md, and add-workflow.md.
- [x] **Make templates domain-agnostic** — Replaced R/Python/Quarto defaults with generic placeholders. Data-science voice moved to commented-out optional block.

### Week 2 — The strategic move

- [x] **Write "Start From Zero" beginner guide** — Created `workflow-package/START-HERE.md`. Covers terminal, git, Claude Code install, setup, and first project walkthrough.
- [x] **Write "share with a friend" quick-start** — Created `workflow-package/QUICK-START-FOR-FRIENDS.md`. Designed to be sent directly — 30-second overview, 3 commands, what to expect.

### Week 3 — Positioning

- [x] **Rewrite README to lead with session continuity** — New intro leads with "the problem nobody else solves" and points beginners to START-HERE.md.
- [x] **Add basic test awareness** — Added test nudge to CLAUDE.md template and expanded /pre-ship with a test section. Don't need full TDD �� just awareness that testing exists and matters.

## Out of scope for this arc

- Multi-tool support (Cursor, Copilot, Aider) — competitors' territory
- Extension/plugin system — complexity that beginners don't need
- TDD enforcement — Superpowers' identity, not ours
- Auto-triggering skills — explicit commands are better for beginners
- Chasing GitHub stars or virality — make it work for one person first

## Definition of done for this arc

- [ ] A complete beginner can go from "I've never coded" to running /init by following the Start From Zero guide, without needing to ask for help
- [ ] All paths and instructions work on Windows
- [ ] The README makes it immediately clear what this project does and why it's different (session continuity, beginner focus)
- [ ] Templates work for any project type, not just data science
- [ ] The repo has one clear path through it (no confusing duplicate files or unexplained versions)

---

---

## Decomposition: Week 1 — Foundation

Goal: Make the repo clean, navigable, cross-platform, and domain-agnostic so it's ready to share.

Steps:

### Task 1: Clean up repo structure

- [ ] 1A: Delete the duplicate `init.md` at the repo root
    - Depends on: none
    - Done when: Only one `init.md` exists (in `workflow-package/slash-commands/`)
- [ ] 1B: Delete the duplicate `chat-project-instructions.md` at the repo root
    - Depends on: none
    - Done when: Only one copy exists (in `workflow-package/reference/`)
- [ ] 1C: Add a "Which version should I use?" section at the top of `repo-update/README.md`
    - Depends on: none
    - Done when: README has a clear 3-sentence routing section that tells a beginner "start with v1 (workflow-package/)" and explains when v2 is appropriate
- [ ] 1D: Verify no broken references after cleanup
    - Depends on: 1A, 1B
    - Done when: Grep for references to root-level `init.md` or `chat-project-instructions.md` returns zero matches

### Task 2: Add Windows instructions

- [ ] 2A: Add Windows path equivalents to `workflow-package/README.md` setup section
    - Depends on: none
    - Done when: Every `~/` path has a Windows equivalent shown, every `cp` has a `copy` or PowerShell equivalent
- [ ] 2B: Fix Windows-incompatible paths in `workflow-package/slash-commands/init.md`
    - Depends on: none
    - Done when: The init command no longer references `/tmp/` — uses a cross-platform approach or shows both OS paths
- [ ] 2C: Verify all remaining slash commands for platform-specific assumptions
    - Depends on: 2A, 2B
    - Done when: Grep for `~/`, `/tmp/`, `cp ` across all .md files returns zero hits without a Windows alternative shown nearby

### Task 3: Make templates domain-agnostic

- [ ] 3A: Rewrite the "Stack and tools" section of `workflow-package/templates/CLAUDE.md`
    - Depends on: none
    - Done when: The section uses generic placeholders (e.g., "Primary language: [your language]") instead of listing R/Python/Quarto specifically
- [ ] 3B: Rewrite the "Voice and standards" section to be generic
    - Depends on: none
    - Done when: Default voice section works for any project type (not "Economist style" or chart-specific guidance). Data-science voice moved to a commented-out "optional: data science flavor" block.
- [ ] 3C: Review template for other domain-specific assumptions
    - Depends on: 3A, 3B
    - Done when: A beginner building a web app, a game, or a CLI tool wouldn't feel like the template wasn't made for them

### Integration check

- [ ] DONE: All Week 1 tasks complete
    - Depends on: 1D, 2C, 3C
    - Done when: A fresh reader can navigate the repo without confusion, all instructions work on Windows, and templates feel welcoming to any project type

---

## Arc history

(No prior arcs — this is the first structured arc for this project.)

---

## Improvement history

<!-- Entries are added by /improve — don't delete this section -->

### 2026-10-01 — Audit (health check only)
- **Findings:** 1 critical, 4 important, 3 nice-to-have
- **Top concerns:** The README's documented first step, /clarify (and /decompose), is missing from the public package; both live only on PR #4 (origin/claude/peaceful-kalam-b698ec), open since 2026-05-17, so a beginner hits an unknown-command error at step 1. The credential-redaction edits to log.md and wrap.md have sat uncommitted since 2026-07-22 (957868a claims them but doesn't contain them), alongside an unreferenced workflow-package/.gitleaks.toml.
- **Other items:** init.md's generated .gitignore ignores *.html, misses .env.*/*.key/*.pem/credentials.*, and skips existing .gitignore files; the package has drifted from ~/.claude/commands (wrap.md 82 lines, plus missing handoff/next/health/new-project/publish/update-workflow/ui-review/clarify/decompose/audit-*); HANDOFF.md stops at 2026-05-16, PLAN.md DoD/subtask boxes unchecked, FAILURES.md missing. Nice: 4 stale remote branches (2 merged, d2e38cb unmerged journal, PR #4); mixed CRLF/LF with no .gitattributes; corrupted em dash at PLAN.md:31.
- **Rule-11 review:** /clarify + /decompose missing from package (PR #4 unmerged) — kept as critical (reviewer 1 confirmed facts, reviewer 2 confirmed severity).
- **Verified OK:** gitleaks 8.30.1 with repo config: 0 leaks across 20 commits and working tree; repo .gitignore covers .env, .env.*, *.pem, *.key, credentials.*, secrets.*; pre-commit hook installed and resolves; all relative Markdown links resolve; no binaries tracked; README has what/how/stack; design-system path exists; main is 0 ahead / 0 behind origin/main. No test suite (pure Markdown), no DB tests. Security and code-quality reviews done manually (/security-review and /ce:review skills not run from the subagent); no data-correctness review (no calculations). Tree was dirty before the audit (M log.md, M wrap.md, ?? workflow-package/.gitleaks.toml), so this entry is not committed.
- **Action taken:** Audit only — no fixes this session
- **Next review:** 2026-12-30
