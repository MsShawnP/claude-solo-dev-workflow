# Workflow Setup Checklist

This is what you do for each new project. Most of the setup is
automated by the `/init` slash command in Claude Code.

---

## One-time setup (do once, applies to everything after)

- [ ] Set up GitHub connector in claude.ai
  - Settings → Connectors → GitHub → Authenticate
  - Test by asking chat to read a file from any repo

- [ ] Create global `~/.claude/CLAUDE.md`
  - Personal preferences (communication style, no preamble, etc.)
  - Conventions you always want (language, framework defaults)
  - The four measurable rules (don't guess, no speculative
    abstractions, tell me what I need to hear, flag vague rules)
  - Applies to every Code session on your machine

- [ ] Save this workflow package somewhere accessible
  - Suggested: `~/notes/workflow-package/` or similar
  - This is your reference library — never edit the templates here,
    copy them into projects and edit the copies
  - `/init` will find it automatically in `~/notes/`, `~/repos/`,
    or `~/` — or clone it from GitHub if not found

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

### Phase 2: Scaffold the project with `/init`

- [ ] Create and `cd` into your project directory
- [ ] `git init` (if not already a repo)
- [ ] Open Claude Code and run:
      `/init Project Name | One-sentence business question`
- [ ] `/init` handles:
  - Copying the five .md templates (CLAUDE.md, DECISIONS.md,
    HANDOFF.md, PLAN.md, FAILURES.md) into the repo root
  - Replacing `[PROJECT NAME]` in all templates
  - Setting the business question in CLAUDE.md
  - Creating `.claude/commands/` with log.md, wrap.md, and init.md
  - Creating .gitignore (if none exists)
  - Initial commit

After `/init` finishes:

- [ ] Fill in CLAUDE.md — stack, voice, domain context
- [ ] Fill in PLAN.md — first arc goal, tasks, definition of done
- [ ] Push to GitHub when ready (`git remote add origin ...` then
      `git push -u origin main`)

### Phase 3: Create the chat project (if using claude.ai chat)

- [ ] In claude.ai: New Project → name it
- [ ] Open `reference/chat-project-instructions.md`
- [ ] Copy the instructions text, fill in [PROJECT NAME] and the "What
      this project is" paragraph, paste into the project's
      instructions field
- [ ] Upload all five .md files (CLAUDE.md, DECISIONS.md, HANDOFF.md,
      PLAN.md, FAILURES.md) to project knowledge
- [ ] Test: open a chat in the project, ask "what is this project
      about" — confirm it reads from the files correctly

### Phase 4: Test the loop

- [ ] Open a fresh Claude Code session
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
- Run Phases 2-4 separately for each project (separate repos, separate
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
│   ├── init.md                         (/init command - project setup)
│   ├── log.md                          (/log command)
│   └── wrap.md                         (/wrap command)
└── reference/
    ├── 95-percent-confidence-prompt.md (project kickoff prompt)
    └── chat-project-instructions.md    (instructions for chat projects)
```
