# Project Audit

## Phase 1: Baseline Assessment
**Date:** 2026-05-16
**Project:** claude-solo-dev-workflow

### What Was Intended
A best-practices workflow for solo developers who have never worked professionally as devs. The system should act as guardrails — telling you what to do next, in what order, without needing prior dev experience to follow along.

### What Exists Today
A working workflow package built entirely in Claude Chat. Two versions:
- **v1 (workflow-package/):** Lightweight — templates, slash commands, reference docs. Covers the full dev cycle from idea to ship.
- **v2 (repo-update/):** Phase-gated agent workflow with 6 specialized subagents (planner, code reviewer, data science reviewer, prose reviewer, remediation tracker, final auditor).

Both are pure Markdown — no executable code. The workflow is operational and actively used by the author.

### Tech Stack
- Markdown files (templates, slash commands, agent definitions)
- Claude Code slash command system (`.claude/commands/`)
- Git + GitHub for hosting
- No runtime dependencies, no build step, no executable code

### Project Health Indicators
- Activity: **Active** — recent commits, merged PR, ongoing use
- Documentation: **Good** — comprehensive README, clear structure, command reference
- Test coverage: **N/A** — no executable code to test
- Dependencies: **None** — pure Markdown

### Gap Analysis
| Intended | Actual | Gap |
|---|---|---|
| Usable by someone who's never coded | Written by/for someone who's been using Claude Code for a while | Assumed knowledge is high — terms like "slash commands", "worktrees", "subagents" aren't explained |
| Best practices workflow | Workflow exists and works | The practices ARE there, but setup requires copying files, cloning repos, editing config — no hand-holding for a true beginner |
| Shareable with others | Works for the author | No "absolute beginner" onboarding path — README assumes you already have Claude Code installed and know what a terminal is |

### Audit Motivation
The author wants to share this with a friend who has never coded before. The audit needs to answer: **what would a complete beginner need changed or added to successfully use this workflow?**

---

## Phase 2: Internal Review
**Date:** 2026-05-16
**Dimensions reviewed:** Documentation, Architecture, UX, DevEx

### Top Opportunities (by leverage)

| # | Finding | Dimension | Impact | Effort | Leverage | Severity |
|---|---------|-----------|--------|--------|----------|----------|
| 1 | No "start from zero" beginner guide — setup assumes terminal/git knowledge | Documentation | 5 | 2 | 2.5 | critical |
| 2 | Two versions (v1/v2) in same repo with no "which one do I use?" guidance | Architecture | 4 | 1 | 4.0 | important |
| 3 | Template CLAUDE.md is data-science-specific (R, Quarto, charts) — confuses non-DS beginners | UX | 4 | 2 | 2.0 | important |
| 4 | Duplicate/conflicting init.md files (root vs workflow-package/) | Architecture | 3 | 1 | 3.0 | important |
| 5 | Setup requires 3+ manual copy operations with no verification step | DevEx | 4 | 3 | 1.3 | important |
| 6 | Path references are Mac/Linux only (`~/`, `cp`, `/tmp/`) — breaks on Windows | DevEx | 3 | 2 | 1.5 | important |
| 7 | No "verify your setup worked" check after installation | DevEx | 3 | 2 | 1.5 | minor |
| 8 | Dev jargon used without definitions: "subagents", "worktrees", "phase-gated", "context compaction" | Documentation | 3 | 2 | 1.5 | minor |

### Detailed Findings

#### Documentation

**Critical:** No beginner onboarding path exists. The README opens with "Clone this repo somewhere accessible" — a sentence that assumes you know what cloning is, what a repo is, and what "accessible" means in a filesystem context. A complete beginner would stall at step 1 of setup.

What's missing for a true beginner:
- What is Claude Code? (1 sentence)
- How do I install it? (link + "do this first")
- What is a terminal? Where do I find it?
- What is git? Do I need it? (yes, and here's how to install it)

**Minor:** The 95-percent-confidence-prompt.md has an excellent "why each piece is there" section — this teaching style should be replicated elsewhere. The /init command's "WHAT TO DO NEXT" block (workflow-package/slash-commands/init.md:148-247) is the gold standard in this repo for beginner-friendliness.

#### Architecture

**Important:** Two versions coexist without clear routing. A beginner sees `workflow-package/` and `repo-update/v2-phase-gated-agent-workflow/` and has no idea which to use. The repo-update/README.md explains both, but it's buried.

**Important:** Two different `init.md` files exist:
- `init.md` (root) — older, simpler version
- `workflow-package/slash-commands/init.md` — newer, more complete version with expanded next-steps guide
These conflict. The root version copies fewer commands (just log.md, wrap.md) while the package version copies 5 commands.

**Observation:** The structure makes sense to someone who built it iteratively but would confuse a newcomer reading top-down.

#### UX (Beginner Usability)

**Important:** The CLAUDE.md template is heavily tailored to data science:
- "Primary language: [R / Python / etc.]"
- "Rendering: [Quarto / etc.]"
- "Economist style for written deliverables"
- "Charts must be readable by non-data-scientist audiences"

A beginner building a web app, a game, or learning to code with no specific project type would find this template alienating — it implies this workflow is for a specific kind of work they're not doing.

**Good:** The /commands card and /init next-steps are well-written for someone who already has Claude Code running. The "WHAT TO DO NEXT" section in the newer init.md is excellent — explicit, ordered, with WHY explanations.

#### DevEx (Setup Friction)

**Important:** Installation requires:
1. Clone the repo (requires git knowledge)
2. Copy slash commands to `~/.claude/commands/` (requires understanding hidden directories, paths)
3. Set up global `~/.claude/CLAUDE.md` (requires knowing what this is and where it goes)

Each step is a potential failure point. No single command or script handles this.

**Important:** All paths use Unix conventions (`~/`, `cp`, `/tmp/`). A Windows user (which the author IS) would need to mentally translate every instruction. The init.md references `/tmp/claude-solo-dev-workflow` which doesn't exist on Windows.

### Summary

The workflow content itself is strong — well-thought-out, practical, and genuinely useful. The problem isn't what it teaches, it's who can access it. Everything assumes you've already gotten over the "what even is a terminal" hurdle. The highest-leverage fix is a single beginner onboarding document that bridges "I've never coded" to "I can run /init". The second biggest win is simplifying the repo structure so a beginner sees one clear path, not two versions and duplicate files.

---

## Phase 3: Landscape Scan
**Date:** 2026-05-16
**Category:** AI coding workflow packages + solo developer frameworks

### Competitors / Similar Projects

| # | Name | Stars | Description | Target |
|---|------|-------|-------------|--------|
| 1 | Superpowers | 194K | Harness-agnostic agentic skills framework. 7-phase workflow (Brainstorm→Spec→Plan→TDD→Dev→Review→Finalize). Auto-triggers from context. | Experienced devs, multiple AI tools |
| 2 | GStack | 89.7K | Garry Tan's Claude Code setup. 23 role-based slash commands modeling a virtual dev team (CEO review, eng review, QA). | Solo devs using Claude Code |
| 3 | GitHub Spec-Kit | 101K | Official GitHub spec-driven dev toolkit. 7-phase sequential workflow with Markdown artifacts per phase. 70+ extensions. | Teams + solo devs with AI agents |
| 4 | claude-code-workflows | 355 | Recipe-based Claude Code workflow with 20+ subagents. Five recipe commands for different task types. | Teams, multi-person projects |
| 5 | awesome-cursorrules | 39.5K | Curated collection of 150+ Cursor AI rule files across 13 tech categories. | Cursor users (rules library, not workflow) |
| 6 | claude-md-templates | 207 | CLAUDE.md authoring best practices. Global/project/local templates + modular rules. | Claude Code users (config, not workflow) |
| 7 | ForeverAloneProgramming | 123 | Solo-dev adaptation of Agile Unified Process. 4 phases: Inception→Elaboration→Construction→Transition. | Intermediate solo devs |
| 8 | Solo Developer's Manifesto | 183 | Community guide: Planning→Implementation→Measurement→Retrospective. Includes soft skills. | Solo devs (written guide, not tool) |

### Feature Matrix

| Feature | This Project | Superpowers | GStack | Spec-Kit | claude-code-workflows |
|---------|:---:|:---:|:---:|:---:|:---:|
| Phased workflow (explicit order) | ✅ | ✅ | 🟡 | ✅ | ✅ |
| Slash commands | ✅ | ❌ (auto) | ✅ | ✅ | ✅ |
| Solo developer focus | ✅ | ❌ | ✅ | 🟡 | ❌ |
| Beginner-friendly | 🟡 | ❌ | ❌ | 🟡 | ❌ |
| Zero toolchain dependency | ✅ | ❌ (shell) | ✅ | ❌ (Python) | ✅ |
| Session continuity (handoff) | ✅ | ❌ | ❌ | ❌ | ❌ |
| Review gates (multi-reviewer) | ✅ | ✅ | ✅ | 🟡 | ✅ |
| Decision/failure logging | ✅ | ❌ | ❌ | ❌ | ❌ |
| Project scaffolding (/init) | ✅ | ❌ | ❌ | ✅ | ✅ |
| Scope creep detection | ✅ | ❌ | ❌ | ❌ | ❌ |
| Cross-model review (Gemini) | ✅ | ❌ | ❌ | ❌ | ❌ |
| Git worktree isolation | ❌ | ✅ | ❌ | ❌ | ❌ |
| TDD enforcement | ❌ | ✅ | ❌ | ❌ | ❌ |
| Multi-tool support (not just Claude) | ❌ | ✅ | ❌ | ✅ | ❌ |
| Large extension ecosystem | ❌ | ❌ | ❌ | ✅ (70+) | ❌ |

### Landscape Position

#### Table Stakes (standard in category — do we have them?)
- ✅ Phased workflow with explicit ordering
- ✅ Slash commands or equivalent invocation
- ✅ Review/QA gates before shipping
- ✅ Project scaffolding
- ❌ **TDD / test enforcement** — Superpowers and professional workflows enforce this; we don't mention testing at all

#### Where This Project Is Stronger
- **Session continuity** — HANDOFF.md + /wrap + /log is unique. Nobody else solves "I closed my laptop, now what?" This is a genuine differentiator.
- **Decision + failure logging** — DECISIONS.md and FAILURES.md capture institutional knowledge. No competitor does this.
- **Scope creep detection** — Actively watching for drift and flagging it. Unique.
- **Beginner guidance** — The /init next-steps walkthrough and /commands card, while imperfect, are more hand-holding than any competitor offers.
- **Zero install** — Pure Markdown, no Python, no shell scripts, no build step.

#### Where This Project Is Weaker
- **Traction** — 0 community users vs. 194K (Superpowers), 89.7K (GStack), 101K (Spec-Kit). The project is invisible.
- **No testing discipline** — No TDD, no test reminders, no coverage tracking. Superpowers builds its entire workflow around RED-GREEN-REFACTOR.
- **No multi-tool support** — Only works with Claude Code. Spec-Kit supports 30+ agents. Superpowers supports 6 AI harnesses.
- **No extension/plugin system** — Spec-Kit has 70+ community extensions. This project is take-it-or-leave-it.
- **Data-science-specific templates** — While competitors are language/domain-agnostic, this project's templates assume R/Python/Quarto.

#### Unique Differentiators
1. **Session continuity system** (HANDOFF.md + /wrap + /log) — solves a problem nobody else addresses
2. **Explicit failure capture** (FAILURES.md) — prevents repeating dead ends across sessions
3. **Scope creep watchdog** — actively monitors for drift, unique among all competitors
4. **"Never worked as a dev" target audience** — every competitor targets experienced developers
5. **Retrospective built into session end** (/wrap asks "what would you do differently?")

#### Category Trends
- **Auto-triggering over manual commands** — Superpowers (194K stars) doesn't use slash commands at all; skills trigger automatically from context. The market is moving toward invisible orchestration.
- **"Personal config goes viral" pattern** — GStack (one person's setup, open-sourced) went from 0 to 89.7K stars in weeks. There's massive appetite for "show me how a good developer works."
- **Spec-first development** — GitHub officially backing spec-driven dev (Spec-Kit) signals this is becoming mainstream, not niche.
- **The beginner gap is wide open** — Every major project targets experienced developers. Nobody is solving "I've literally never coded before and want guardrails." This is an uncontested niche.

### Summary

This project occupies a unique position: it's the only workflow package that combines (a) solo-developer focus, (b) session continuity, (c) failure/decision logging, and (d) a beginner-friendly intent — with zero toolchain dependency. The biggest competitors (Superpowers, GStack, Spec-Kit) all have massive traction but target experienced developers. The "complete beginner" niche is completely unserved. The main risk is obscurity — the project has zero external visibility while competitors have 100K+ stars.

---

## Phase 4: Differentiation & Next Moves
**Date:** 2026-05-16

### Cross-Reference Summary

The internal opportunities (Phase 2) and landscape position (Phase 3) point in the same direction: **this project's biggest weakness (inaccessible to beginners) is also its biggest opportunity (nobody else serves beginners either).** Fixing the accessibility problems isn't just internal hygiene — it's the strategic move that would put this project in an uncontested niche.

The session continuity system (HANDOFF.md + /wrap + /log) is the strongest unique differentiator and should be the headline when positioning this project. No competitor — not even the 194K-star Superpowers — solves "I closed my laptop, what was I doing?" This matters even more for beginners who can't reconstruct context from code alone.

The foundational cleanup (duplicate files, broken Windows paths, confusing repo structure) is prerequisite to everything else. You can't share this with your friend if the repo confuses them before they even get to the good parts.

### Ranked Next Moves

| # | Move | Category | Strategic | Internal | Effort | Score | Description |
|---|------|----------|-----------|----------|--------|-------|-------------|
| 1 | Write a "Start From Zero" beginner guide | Leapfrog | 5 | 5 | 2 | 5.0 | A single doc that bridges "never coded" to "running /init". Covers: what is Claude Code, install it, what is a terminal, what is git. Puts this project in an uncontested niche. |
| 2 | Clean up repo structure (one clear path) | Foundational | 3 | 5 | 1 | 8.0 | Remove duplicate init.md, add "which version?" routing at top of README, resolve conflicting files. 30 minutes of work, unblocks everything else. |
| 3 | Make templates domain-agnostic | Close gap | 4 | 4 | 2 | 4.0 | Replace R/Python/Quarto defaults with generic placeholders. Add optional "data science flavor" as a variant, not the default. Opens the door to any beginner, not just data-science beginners. |
| 4 | Add Windows instructions | Foundational | 2 | 4 | 1 | 6.0 | Add Windows equivalents for all paths and commands. The author and the target friend are both on Windows — this is basic correctness. |
| 5 | Position session continuity as the headline | Double down | 5 | 2 | 1 | 7.0 | Rewrite README intro to lead with "the problem nobody else solves: what happens when you close your laptop." Makes the unique value immediately obvious. |
| 6 | Add basic test awareness to workflow | Close gap | 3 | 3 | 2 | 3.0 | Don't need full TDD enforcement (that's Superpowers' territory). Just add "did you test this?" to /pre-ship and a mention in the workflow. Closes a table-stakes gap without overengineering. |
| 7 | Write a "share this with a friend" quick-start | Leapfrog | 4 | 3 | 2 | 3.5 | A short companion doc specifically for sending to someone: "Your friend set this up for you. Here's what it does and how to use it." Lowers the barrier from "read the whole repo" to "read this one page." |

### Recommended Sequence

**Week 1 — Foundation (do first, enables everything else):**
1. Clean up repo structure (#2) — 30 min
2. Add Windows instructions (#4) — 20 min
3. Remove data-science defaults from templates (#3) — 30 min

**Week 2 — The strategic move:**
4. Write the "Start From Zero" beginner guide (#1) — 1 hour
5. Write the "share with a friend" quick-start (#7) — 30 min

**Week 3 — Positioning:**
6. Rewrite README to lead with session continuity (#5) — 20 min
7. Add test awareness to workflow (#6) — 20 min

The first week is cleanup that takes ~1 hour total. The second week is the high-value creative work. The third week is polish.

### What NOT to Do

- **Don't add multi-tool support.** Superpowers and Spec-Kit own that space with massive head starts. Trying to support Cursor/Copilot/Aider would dilute focus without catching up. Claude Code-only is fine — it's what your audience will use.
- **Don't build an extension/plugin system.** Spec-Kit has 70+ extensions because it targets teams with diverse needs. You target beginners who need one opinionated path, not choices. Simplicity IS the feature.
- **Don't add TDD enforcement.** Superpowers built its entire identity around RED-GREEN-REFACTOR. Competing on testing rigor means competing against a 194K-star project on its home turf. A light "did you test?" reminder is enough.
- **Don't chase auto-triggering (Superpowers' model).** Explicit slash commands are actually BETTER for beginners — they're visible, predictable, and teachable. Auto-triggering is magic, and magic confuses new users.
- **Don't try to get 100K stars.** The "personal config goes viral" pattern requires an existing audience (Garry Tan is YC's CEO). Focus on making it work perfectly for your friend first. If it's genuinely good for beginners, word of mouth will find its audience.
