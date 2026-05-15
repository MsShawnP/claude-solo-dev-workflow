---
description: Show available workflow commands and when to use each one
---

Print this quick reference card. No arguments needed.

```
---------------------------------------------------
WORKFLOW COMMANDS — quick reference
---------------------------------------------------

Type / in the chat to see all available commands.
These are the workflow commands and when to use them:

DURING SETUP
  /init         Set up a new project with all workflow files.
                Use once, at the very beginning.

  /add-workflow  Add workflow files to a project that already
                exists. Use when you have code but no PLAN.md,
                HANDOFF.md, etc.

WHILE WORKING
  /log          Save a checkpoint. Run after each meaningful
                change — bug fixed, feature added, decision
                made. Quick, takes 10 seconds.

  /improve      Review and improve the project. Audits your
                code, tests, security, and workflow files,
                then walks you through fixing what matters.
                Also works as: /improve audit-only (just the
                health check, no fixes).

WHEN STOPPING
  /wrap         End-of-session protocol. Captures everything
                that happened so your next session picks up
                right where you left off. Run this before you
                close Claude Code.

ANYTIME
  /commands     This card. Shows what's available.

---------------------------------------------------
TIP: Type / and you'll see a list of all commands.
     Arrow-key to the one you want and hit Enter.
---------------------------------------------------
```

After printing the card, add a one-line suggestion based on the
current project state:

- If PLAN.md has no active tasks → "You might want to start with
  /improve to see what needs work."
- If HANDOFF.md's last entry is old → "Looks like it's been a while.
  Try /improve audit-only for a quick health check."
- If there are uncommitted changes → "You have uncommitted changes.
  Run /log to save a checkpoint."
- If none of the above apply → "You're in good shape. Keep working
  and run /log when you finish something."
