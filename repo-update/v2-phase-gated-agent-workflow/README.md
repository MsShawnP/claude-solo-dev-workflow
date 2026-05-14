# Development Workflow Template

A lightweight, phase-gated development workflow for Claude Code. Drop the `.claude/` directory into any project to get structured planning, review, validation, and audit phases.

## Setup

Copy the `.claude/` directory into your project root:

```
your-project/
├── .claude/
│   ├── CLAUDE.md          # Workflow definition (Claude Code reads this on session start)
│   └── agents/
│       ├── project-planner.md
│       ├── code-reviewer.md
│       ├── data-science-reviewer.md
│       ├── prose-reviewer.md
│       ├── remediation-tracker.md
│       └── final-auditor.md
├── ... your project files ...
```

Edit the **Project Context** section at the bottom of `.claude/CLAUDE.md` with your project's specifics.

## Usage

Start a Claude Code session in your project directory. Claude reads `.claude/CLAUDE.md` automatically.

**You don't need to memorize the phases.** Claude Code will prompt you at every phase boundary — telling you where you are, what just finished, and what comes next. It also reorients automatically on session start or after context compaction.

### Phase Commands

| Phase | Say this | Output |
|-------|----------|--------|
| **Plan** | "Run the planning agent" | `PROJECT_PLAN.md` |
| **Build** | (just work normally) | Your project |
| **Code Review** | "Run code review" | `REVIEW_CODE.md` |
| **Data Review** | "Run data review" | `REVIEW_DATA.md` |
| **Prose Review** | "Run prose review" | `REVIEW_PROSE.md` |
| **Remediate** | "Run remediation" | `REMEDIATION.md` |
| **Audit** | "Run final audit" | `AUDIT.md` |

After fixing issues: "Update remediation" to refresh the tracker.

### Phase Flow

```
PLAN → BUILD → CODE REVIEW → DATA REVIEW → PROSE REVIEW → REMEDIATE → AUDIT → COMMIT
                    ↑                                           │
                    └───────────────────────────────────────────┘
                                  (loop if needed)
```

### Cross-Model Scope Review (Optional)

After planning, you can send `PROJECT_PLAN.md` to a second model (e.g., Gemini) for an independent scope review. Recommended for complex or client-facing projects. Paste the plan and ask: "What's missing, what's unrealistic, what are the risks I haven't considered?"

### Scope Changes

When requirements change mid-project, just say what's changing. Claude Code updates `PROJECT_PLAN.md` with a change log entry. All reviews and audit check against the updated plan, not the original.

### Skipping Phases

- **No data/analysis component?** Skip Data Review.
- **No written narrative?** Skip Prose Review.
- **Quick fix or trivial change?** Skip straight to Code Review + Audit.
- **Exploratory work?** Skip Planning, run reviews when you're ready to formalize.

Claude Code detects which phases are relevant and adjusts its prompts accordingly.

## Artifacts Produced

| File | Phase | Purpose |
|------|-------|---------|
| `PROJECT_PLAN.md` | Plan | Scope, deliverables, approach, success criteria |
| `REVIEW_CODE.md` | Code Review | Code quality and reproducibility findings |
| `REVIEW_DATA.md` | Data Review | Analytical correctness and data integrity findings |
| `REVIEW_PROSE.md` | Prose Review | Narrative quality, audience calibration, claims vs. evidence |
| `REMEDIATION.md` | Remediate | Consolidated issue tracker with resolution status |
| `AUDIT.md` | Audit | Final pass/fail verdict with verification details |

Keep or `.gitignore` these as you prefer.

## Customization

- **Add project-specific checks:** Edit the agent files to include domain-specific validation (e.g., GS1/GTIN format checks for product data, rebate calculation rules for incentive data).
- **Add new agents:** Create a new `.md` file in `.claude/agents/` and reference it in `CLAUDE.md`.
- **Adjust severity criteria:** Edit the BLOCKING/ADVISORY definitions in any agent to match your risk tolerance.
