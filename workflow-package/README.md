# Workflow Setup Checklist

This is what you do manually for each new project. The files in this
package are what you reference / copy from.

---

## One-time setup (do once, applies to everything after)

- [ ] Set up GitHub connector in claude.ai
  - Settings → Connectors → GitHub → Authenticate
  - Test by asking chat to read a file from any repo

- [ ] Create global `~/.claude/CLAUDE.md`
  - Personal preferences (communication style, no preamble, etc.)
  - R/Quarto conventions you always want
  - The four measurable rules (don't guess, no speculative
    abstractions, tell me what I need to hear, flag vague rules)
  - Applies to every Code session on your machine

- [ ] Save this workflow package somewhere accessible
  - Suggested: `~/notes/workflow-package/` or similar
  - This is your reference library — never edit the templates here,
    copy them into projects and edit the copies

- [ ] Tag the final state of the Cinderhaven Audit repo
  - `git tag v1.0-shipped` (or whatever name fits)
  - `git push --tags` if you want it on the remote

---

## Per-project setup (do for each new project)

### Phase 1: Plan in chat (do this BEFORE creating the repo)

- [ ] Open a new chat in claude.ai (no project yet)
- [ ] Run the 95% confidence prompt
  - Reference: `reference/95-percent-confidence-prompt.md`
- [ ] Have the interview conversation
- [ ] Capture the output: business question, scope, approach, what's
      explicitly out of scope, what "done" looks like
- [ ] This output becomes the starting content for PLAN.md and
      CLAUDE.md

### Phase 2: Create the repo

- [ ] Create new repo (locally and on GitHub)
- [ ] Decide public vs. private
- [ ] Create `.gitignore` (exclude rendered output, _freeze/,
      .Rproj.user/, renv/library/, .env, *.db, large files, client
      data)
- [ ] Copy the five .md templates from `templates/` into repo root:
  - CLAUDE.md
  - DECISIONS.md
  - HANDOFF.md
  - PLAN.md
  - FAILURES.md
- [ ] Fill in the bracketed [PROJECT NAME] and [BUSINESS QUESTION]
      sections in each
- [ ] Fill in PLAN.md with the first arc based on the 95% confidence
      conversation

### Phase 3: Set up slash commands

- [ ] Create `.claude/commands/` directory in the repo
- [ ] Copy `slash-commands/log.md` to `.claude/commands/log.md`
- [ ] Copy `slash-commands/wrap.md` to `.claude/commands/wrap.md`

### Phase 4: First commit

- [ ] `git add -A`
- [ ] `git commit -m "chore: initial project setup with workflow files"`
- [ ] `git push`
- [ ] Tag the initial state: `git tag v0.1-foundation`

### Phase 5: Create the chat project

- [ ] In claude.ai: New Project → name it
- [ ] Open `reference/chat-project-instructions.md`
- [ ] Copy the instructions text, fill in [PROJECT NAME] and the "What
      this project is" paragraph, paste into the project's
      instructions field
- [ ] Upload all five .md files (CLAUDE.md, DECISIONS.md, HANDOFF.md,
      PLAN.md, FAILURES.md) to project knowledge
- [ ] Test: open a chat in the project, ask "what is this project
      about" — confirm it reads from the files correctly

### Phase 6: Test the loop

- [ ] Open a fresh Claude Code session in VS Code
- [ ] Confirm Code reads CLAUDE.md automatically at session start
- [ ] Make a tiny change (add a comment somewhere)
- [ ] Run `/log` — confirm HANDOFF.md updated and commit happened
- [ ] Run `/wrap` — confirm full protocol works (summary, file
      updates, commit with summary in body)
- [ ] If anything in the loop feels wrong, tune the slash command
      files before doing real work

---

## For two projects starting in parallel

- Run Phase 1 separately for each project (different chats, different
  business questions)
- Run Phases 2-6 separately for each project (separate repos, separate
  chat projects)
- The one-time setup only happens once

The two projects share:
- Global ~/.claude/CLAUDE.md
- The workflow package as reference
- The GitHub connector
- Your personal preferences

Each project has its own:
- Repo
- Five .md files
- .claude/commands/ directory
- Chat project with its own instructions and knowledge files

---

## What this package contains

```
workflow-package/
├── README.md                           (this file - the checklist)
├── templates/
│   ├── CLAUDE.md                       (project rules, voice, behavior)
│   ├── DECISIONS.md                    (durable choices log)
│   ├── HANDOFF.md                      (session state log)
│   ├── PLAN.md                         (current work arc)
│   └── FAILURES.md                     (things that didn't work)
├── slash-commands/
│   ├── log.md                          (/log command)
│   └── wrap.md                         (/wrap command)
└── reference/
    ├── 95-percent-confidence-prompt.md (project kickoff prompt)
    └── chat-project-instructions.md    (instructions for chat projects)
```
