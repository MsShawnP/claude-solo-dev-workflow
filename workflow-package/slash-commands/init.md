---
description: Initialize a new project with the solo dev workflow structure. Run from the project directory.
---

Set up a new project with the full workflow structure. Do these in
order.

Argument: $ARGUMENTS
- $ARGUMENTS should contain two things, separated by a pipe:
  PROJECT_NAME | BUSINESS_QUESTION
- Example: "Trade Spend Diagnostic | For a $25M specialty food brand,
  where is the trade spend going and what's the addressable improvement?"
- If $ARGUMENTS is empty, ask for the project name and business
  question before proceeding.

## Step 1: Verify prerequisites

1. Confirm we're in a git repo (`git rev-parse --is-inside-work-tree`).
   If not, ask the user: initialize one here, or are we in the wrong
   directory?
2. Check if the workflow-package repo is cloned locally. Look in these
   locations in order:
   - `~/notes/workflow-package/`
   - `~/claude-solo-dev-workflow/workflow-package/`
   - `~/repos/claude-solo-dev-workflow/workflow-package/`
   If not found, clone it:
   `git clone https://github.com/MsShawnP/claude-solo-dev-workflow.git /tmp/claude-solo-dev-workflow`
   and use `/tmp/claude-solo-dev-workflow/workflow-package/` as the
   source.
3. Check if any workflow files already exist (CLAUDE.md, PLAN.md,
   HANDOFF.md, DECISIONS.md, FAILURES.md, .claude/commands/). If
   they do, stop and report what's already there. Do not overwrite
   without explicit confirmation.

## Step 2: Create directory structure

```
.claude/
  commands/
```

## Step 3: Copy and fill templates

Copy these files from the workflow-package `templates/` directory into
the project root:

- CLAUDE.md
- DECISIONS.md
- HANDOFF.md
- PLAN.md
- FAILURES.md

In every copied file, replace `[PROJECT NAME]` with the PROJECT_NAME
from $ARGUMENTS.

In CLAUDE.md, replace `[One sentence. If you can't write this sentence
cleanly, the project isn't scoped enough yet.]` with the
BUSINESS_QUESTION from $ARGUMENTS.

Leave all other bracketed sections as-is — they get filled in during
the 95% confidence conversation or as the project develops.

## Step 4: Copy slash commands

Copy from the workflow-package `slash-commands/` directory:

- `log.md` → `.claude/commands/log.md`
- `wrap.md` → `.claude/commands/wrap.md`

Also copy this file (`init.md`) into `.claude/commands/init.md` so
future projects can be initialized the same way.

## Step 5: Create .gitignore (if one doesn't exist)

If no .gitignore exists, create one with sensible defaults:

```
# Rendered output
*.html
_freeze/
_site/

# R
.Rproj.user/
.Rhistory
.RData
.Rdata
renv/library/

# Python
__pycache__/
*.pyc
.venv/
venv/

# Environment and secrets
.env
*.env

# Data files (uncomment if needed)
# *.db
# *.sqlite
# data/raw/

# OS
.DS_Store
Thumbs.db
```

If a .gitignore already exists, skip this step — do not modify it.

## Step 6: Initial commit

1. `git add -A`
2. `git commit -m "chore: initialize project with solo dev workflow"`
3. Report the commit hash and file list.

Do not push. Do not create tags — the user decides when to tag.

## Step 7: Report

After setup is complete, print:

```
Project initialized: [PROJECT_NAME]

Files created:
  CLAUDE.md          — project rules and context (fill in stack, voice, domain)
  DECISIONS.md       — durable choices log
  HANDOFF.md         — session state log
  PLAN.md            — current work arc (fill in first arc tasks)
  FAILURES.md        — things that didn't work
  .claude/commands/
    log.md           — /log slash command
    wrap.md          — /wrap slash command
    init.md          — /init slash command (this file)

Next steps:
  1. Fill in CLAUDE.md — stack, voice, domain context
  2. Fill in PLAN.md — first arc goal, tasks, definition of done
  3. If using claude.ai chat project: create it, paste instructions
     from reference/chat-project-instructions.md, upload the 5 .md files
  4. Start building
```

## Rules

- Do not modify any existing files without asking.
- Do not push to remote.
- If any step fails, stop and report. Do not attempt to fix
  automatically.
- This command is idempotent for the check step — running it on an
  already-initialized project should report what exists and stop,
  not duplicate anything.
