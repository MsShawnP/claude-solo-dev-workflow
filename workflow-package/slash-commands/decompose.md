---
description: Break a task into smaller, individually-testable sub-tasks
---

## Prerequisites — check BEFORE doing anything

1. Run `git rev-parse --is-inside-work-tree` to confirm we're in a git repo.
2. If NOT in a git repo, **STOP immediately** and tell the user:

   ```
   ⚠️  No git repository found in this directory.

   /decompose needs to run inside an initialized project.
   Running it outside a repo can create files in the wrong
   place and cause a mess with worktrees and folders.

   What to do:
   - If this is a NEW project: run /new-project or /init first.
   - If the project exists elsewhere: navigate to that
     directory and run /decompose again.
   ```

   Do NOT proceed. Do NOT create any files.

3. If we ARE in a git repo but inside a `.claude/worktrees/` path, **STOP** and warn:

   ```
   ⚠️  You're inside a Claude worktree, not your main project.

   Navigate to your actual project directory before running
   /decompose.
   ```

   Do NOT proceed.

---

Break the given task into smaller sub-tasks that can each be implemented and tested independently. The pattern: instead of going from A directly to B, go A → A1 → A2 → A3 → B.

**Task to decompose:** $ARGUMENTS

If no task was provided, read `PLAN.md` for the current focus and ask the user which item to decompose.

**Decomposition rules:**

1. Each sub-task must be:
   - Implementable on its own without the others existing first (where possible)
   - Testable on its own — there's something concrete you can run/check
   - Small enough to fit in a single focused work session (< 2 hours of work)

2. If a sub-task is still too big, recurse: decompose it further.

3. Explicit dependencies. If A2 depends on A1, say so.

4. Each sub-task gets a one-sentence "done when" — the concrete verification.

**Output format:**

Write to `PLAN.md` under a new `## Decomposition: <task name>` section:

```markdown
## Decomposition: <task name>

Goal: <one sentence>

Steps:
- [ ] A1: <description>
    - Depends on: (none / A0)
    - Done when: <verification>
- [ ] A2: <description>
    - Depends on: A1
    - Done when: <verification>
- [ ] A3: <description>
    - Depends on: A1, A2
    - Done when: <verification>
- [ ] B (integration): combine A1, A2, A3 into final form
    - Done when: <verification>
```

**After writing:**

1. Show the decomposition to the user.
2. Ask if it matches their mental model. Iterate if not.
3. Once accepted, suggest starting with the first sub-task that has no dependencies.

**Watch for these decomposition smells:**

- A step that's "set up the framework" with no concrete deliverable — too vague, decompose further.
- A step that bundles "implement X and tests" — split implementation and verification.
- A step whose "done when" is "looks good" — replace with a testable assertion.
- More than 7 sub-tasks at one level — likely needs another level of grouping.
