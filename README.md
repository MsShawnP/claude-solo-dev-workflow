# claude-solo-dev-workflow — structured solo-dev process for Claude Code and Claude chat

Templates, slash commands, agents, and reference materials for running solo
projects with structured state management, review gates, and decision
tracking. Two versions live in this repo: the original file-based workflow
(v1) and a phase-gated agent workflow (v2).

## Which version should I use?

**Start with v1** (`workflow-package/`). It's simpler, requires no agents or
advanced features, and covers the full dev cycle.

**Use v2** (`repo-update/v2-phase-gated-agent-workflow/`) if you're doing
data science, analytics, or reporting projects and are comfortable with
Claude Code's subagent system. It adds automated review phases but is more
complex to run.

## v1 — Original Workflow (`workflow-package/`)

The original workflow for solo portfolio projects. Emphasizes:

- State in files, not in sessions
- Structured journaling at session end
- Explicit failure capture (not just success)
- Vertical slices over horizontal phases
- Measurable rules over vague guidance

Core commands (full set in `workflow-package/slash-commands/`, which also
includes `/qa`, `/pre-ship`, `/office-hours`, and plan-review commands):

- `/init` — Scaffold a new project with all workflow files and a guided walkthrough
- `/log` — Save a checkpoint (what changed, what's next)
- `/wrap` — End-of-session protocol (captures everything for next session)
- `/improve` — Review and improve an existing project (audit + guided fixes + tracking)
- `/add-workflow` — Retrofit workflow files onto an existing project

**Quick start:** see `workflow-package/README.md` and
`workflow-package/START-HERE.md` (beginner walkthrough). Setup is copying the
slash-command Markdown files into `~/.claude/commands/` and the templates
into your project — no build or install step.

## v2 — Phase-Gated Agent Workflow (`repo-update/v2-phase-gated-agent-workflow/`)

A phase-gated development workflow using Claude Code's subagent system.
Specialized agents handle planning, code review, data/analysis validation,
prose/narrative review, remediation tracking, and final audit. Built for data
science, analytics, and reporting projects but works for any project type.

What it adds over v1:

- **Automated phase prompting** — Claude Code tells you where you are and what
  comes next at every phase boundary, including after session restarts and
  context compaction
- **Dedicated review agents** — separate code quality, data/analysis
  correctness, and prose/narrative reviews with structured findings
- **Data science validation layer** — checks aggregation logic, join
  integrity, metric definitions, chart-data alignment; traces summary numbers
  back to source data
- **Remediation tracking** — consolidates review findings into a single
  prioritized checklist with resolution status
- **Scope change protocol** — plan amendments are logged; reviews check
  against the current spec
- **Cross-model scope review** — optional independent plan validation by a
  second LLM (e.g., Gemini) before building

Phase flow:

```
PLAN → BUILD → CODE REVIEW → DATA REVIEW → PROSE REVIEW → REMEDIATE → AUDIT → COMMIT
                    ↑                                           │
                    └───────────────────────────────────────────┘
                                  (loop if needed)
```

**Setup:** see `repo-update/v2-phase-gated-agent-workflow/README.md` — you
drop its `.claude/` directory (workflow definition + agent files) into your
project root.

## Tech stack

Plain Markdown throughout: slash-command prompt files, agent definitions, and
state-file templates for Claude Code. No code, no dependencies.

## Project structure

- `workflow-package/` — v1: `slash-commands/`, `templates/` (CLAUDE.md,
  PLAN.md, HANDOFF.md, DECISIONS.md, FAILURES.md, src/tests variants),
  `reference/` (chat project instructions, confidence prompt), START-HERE
  and quick-start guides
- `repo-update/` — staged repo README update plus
  `v2-phase-gated-agent-workflow/` (v2 documentation)
- `AUDIT.md`, `PLAN.md`, `DECISIONS.md`, `HANDOFF.md` — this repo's own
  workflow state files

## Origin

Built by Shawn Phillips for solo portfolio and consulting work — data
analysis, reporting, visualization, data hygiene audits, and adjacent
projects. Distilled from working in Claude Code across multiple projects.

## License

MIT — see [LICENSE](LICENSE).
