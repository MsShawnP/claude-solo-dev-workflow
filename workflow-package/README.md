# Workflow Package

**The problem nobody else solves:** You close your laptop, come back
tomorrow, and have no idea where you were or what you were doing.
This workflow fixes that — and a lot more.

It gives you a structured process for building software: what to do
first, when to stop and review, how to capture decisions and failures
so you don't repeat them, and how to hand off context between sessions
so you never lose your thread.

**New to development?** Start with [START-HERE.md](START-HERE.md) —
it walks you through everything from installing your tools to running
your first project.

**Already have Claude Code running?** Keep reading below.

---

## Commands

These are the slash commands available in every project. Type `/` in
Claude Code to see them, or run `/commands` for a quick reference card.

### Setup
| Command | What it does |
|---|---|
| `/init` | Scaffold a new project with all workflow files. Guided "what to do next" walkthrough. |
| `/add-workflow` | Add workflow files to a project that already has code. |

### Before building
| Command | What it does |
|---|---|
| `/office-hours` | Critical-friend conversation. Stress-tests your idea before you build it. |
| `/plan-ceo-review` | Product gate. Is this worth building? Is the scope right? |
| `/plan-eng-review` | Architecture gate. Will the technical approach work? |

### While working
| Command | What it does |
|---|---|
| `/log` | Save a checkpoint after each meaningful change. |
| `/improve` | Audit and improve the project (code, tests, security, data). Also: `/improve audit-only`. |
| `/qa` | Test the project in a real browser via gstack. |

### Before shipping
| Command | What it does |
|---|---|
| `/pre-ship` | Verify: runs from scratch, no secrets, deps pinned, README current, work pushed. |

### When stopping
| Command | What it does |
|---|---|
| `/wrap` | End-of-session protocol. Captures everything for the next session. |

### Anytime
| Command | What it does |
|---|---|
| `/commands` | Quick reference card with all commands and the full workflow order. |

---

## The workflow

### New projects (13 steps)

```
Phase 1 — Build the right thing
  1. /clarify            Interview until the idea is clear
  2. /office-hours       Challenge the idea, find problems
  3. /plan-ceo-review    Product check: worth building?
  4. /plan-eng-review    Technical check: will it work?

Phase 2 — Build it right
  5. /init               Scaffold project files
  6. /ce:brainstorm      Spec out the approach
  7. /ce:plan            Detailed implementation plan
  8. /ce:work            Execute the plan
  9. /ce:review          Multi-reviewer code review
 10. /qa                 Test it in a browser

Phase 3 — Finish and learn
 11. /pre-ship           Verify it works from scratch, no secrets
 12. /ce:compound        Capture learnings for future sessions
 13. Ship

While working, repeat as needed:
     /log               After each meaningful change
     /wrap              When done for the day
```

### Improving existing projects

```
  1. /improve            Audit + fix (or /improve audit-only)
  2. /qa                 Test the fixes in a browser
  3. /wrap               End the session
```

### Tier shortcuts

You don't always need all 13 steps:

| Tier | When | What to run |
|---|---|---|
| **Quick** | Throwaway, < 1 day | `/clarify` only, then build |
| **Medium** | Feature, weekend project | Skip steps 2-4, start at `/clarify` then `/init` |
| **Heavy** | Product, maintained > 3 months | All 13 steps |

---

## Templates

Files that get copied into each project by `/init`:

| File | Purpose |
|---|---|
| `CLAUDE.md` | Project rules, context, voice, stack. Read by Claude at every session start. |
| `PLAN.md` | Current work arc — goal, tasks, definition of done, improvement history. |
| `HANDOFF.md` | Session-to-session state log. What happened, what's next. |
| `DECISIONS.md` | Durable choices with reasoning. Architecture, data, conventions. |
| `FAILURES.md` | What didn't work and why. Prevents repeating dead ends. |
| `src-CLAUDE.md` | Code conventions for `src/` directory. |
| `tests-CLAUDE.md` | Test conventions for `tests/` directory. |

---

## What the workflow does for you automatically

You don't have to remember what to do — the workflow prompts you:

| Situation | What Claude suggests |
|---|---|
| Session starts | Shows available commands, checks if project is due for review |
| You finish a task | "Good time to /log that." |
| You built something visible | "Want to run /qa to test that?" |
| You're about to stop | "Run /wrap before you go." |
| You drift from the plan | Flags work outside PLAN.md |
| You're about to make risky changes | Suggests creating a git branch first |
| You have unpushed commits | Reminds you to push/backup |
| Project is overdue for review | Suggests `/improve audit-only` |
| You don't know what's available | "Run /commands." |

---

## Setup

### One-time (do once)

1. Clone this repo somewhere accessible:

   **Mac/Linux:**
   ```
   git clone https://github.com/MsShawnP/claude-solo-dev-workflow.git ~/projects/reference/claude-solo-dev-workflow
   ```

   **Windows (PowerShell):**
   ```
   git clone https://github.com/MsShawnP/claude-solo-dev-workflow.git "$env:USERPROFILE\projects\reference\claude-solo-dev-workflow"
   ```

2. Copy the slash commands to your global Claude commands:

   **Mac/Linux:**
   ```
   cp workflow-package/slash-commands/*.md ~/.claude/commands/
   ```

   **Windows (PowerShell):**
   ```
   Copy-Item workflow-package\slash-commands\*.md "$env:USERPROFILE\.claude\commands\"
   ```

3. Set up your global CLAUDE.md with personal preferences
   and the four measurable rules.

   - **Mac/Linux:** `~/.claude/CLAUDE.md`
   - **Windows:** `%USERPROFILE%\.claude\CLAUDE.md`

### Per project

For a **new project:** Run `/init Project Name | Business question`

For an **existing project:** Run `/add-workflow` or `/improve`

---

## Package contents

```
workflow-package/
├── README.md                            (this file)
├── templates/
│   ├── CLAUDE.md                        (project rules and context)
│   ├── DECISIONS.md                     (durable choices log)
│   ├── HANDOFF.md                       (session state log)
│   ├── PLAN.md                          (current work arc)
│   ├── FAILURES.md                      (failure log)
│   ├── src-CLAUDE.md                    (code conventions)
│   └── tests-CLAUDE.md                  (test conventions)
├── slash-commands/
│   ├── init.md                          (/init — scaffold project)
│   ├── log.md                           (/log — save checkpoint)
│   ├── wrap.md                          (/wrap — end session)
│   ├── improve.md                       (/improve — audit and fix)
│   ├── commands.md                      (/commands — quick reference)
│   ├── pre-ship.md                      (/pre-ship — shipping checklist)
│   ├── office-hours.md                  (/office-hours — challenge idea)
│   ├── plan-ceo-review.md              (/plan-ceo-review — product gate)
│   ├── plan-eng-review.md              (/plan-eng-review — arch gate)
│   ├── qa.md                            (/qa — browser testing)
│   └── add-workflow.md                  (/add-workflow — retrofit)
└── reference/
    ├── 95-percent-confidence-prompt.md  (project kickoff prompt)
    └── chat-project-instructions.md     (chat project instructions)
```
