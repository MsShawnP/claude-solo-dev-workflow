# claude-solo-dev-workflow

A workflow for solo developers using Claude Code and Claude chat together. Templates, slash commands, agents, and reference materials for running projects with structured state management, review gates, and decision tracking.

## Versions

### v1 — Original Workflow (`workflow-package/`)

The original workflow for solo portfolio projects. Emphasizes:

- State in files, not in sessions
- Structured journaling at session end
- Explicit failure capture (not just success)
- Vertical slices over horizontal phases
- Measurable rules over vague guidance

**Best for:** Getting started with structured Claude Code development. Lightweight, no agent orchestration.

**Setup:** See `workflow-package/README.md`

---

### v2 — Phase-Gated Agent Workflow (`v2-phase-gated-agent-workflow/`)

A complete phase-gated development workflow using Claude Code's subagent system. Six specialized agents handle planning, code review, data/analysis validation, prose/narrative review, remediation tracking, and final audit. Built for data science, analytics, and reporting projects but works for any project type.

**What it adds over v1:**

- **Automated phase prompting** — Claude Code tells you where you are and what comes next at every phase boundary, including after session restarts and context compaction
- **Dedicated review agents** — separate code quality, data/analysis correctness, and prose/narrative reviews run as distinct phases with structured findings
- **Data science validation layer** — checks aggregation logic, join integrity, metric definitions, chart-data alignment, and traces summary numbers back to source data
- **Remediation tracking** — consolidates all review findings into a single prioritized checklist with resolution status
- **Scope change protocol** — amendments to the plan are logged, and all reviews check against the current spec
- **Cross-model scope review** — optional step to send the project plan to a second LLM (e.g., Gemini) for independent validation before building

**Phase flow:**

```
PLAN → BUILD → CODE REVIEW → DATA REVIEW → PROSE REVIEW → REMEDIATE → AUDIT → COMMIT
                    ↑                                           │
                    └───────────────────────────────────────────┘
                                  (loop if needed)
```

**Best for:** Data science, analytics, reporting, and any project where analytical correctness and narrative quality matter as much as code quality.

**Setup:** See `v2-phase-gated-agent-workflow/README.md`

## Origin

Built by Shawn Phillips for solo portfolio and consulting work — data analysis, reporting, visualization, data hygiene audits, and adjacent projects. Distilled from working in Claude Code across multiple projects.

## License

MIT
