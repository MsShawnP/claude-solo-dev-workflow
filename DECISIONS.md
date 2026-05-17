# claude-solo-dev-workflow — Decisions

Durable choices with rationale. These hold until explicitly reversed.

---

### 2026-05-16 — Solo dev workflow: minimal ceremony, no worktrees
- **Why:** Merge overhead, extra commands after wrap, and sessions ignoring context are all friction that outweighs the safety benefits for a solo developer.
- **Scope:** All workflow behavior — wrap, session start, branching strategy.
- **Do not:** Create worktrees automatically, require manual push after wrap, or begin work without reading project state files.
