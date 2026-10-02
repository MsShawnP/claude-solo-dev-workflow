---
description: Interview user until 95% confident about what they actually want
---

## Prerequisites — check BEFORE starting the interview

1. Run `git rev-parse --is-inside-work-tree` to confirm we're in a git repo.
2. If NOT in a git repo, **STOP immediately** and tell the user:

   ```
   ⚠️  No git repository found in this directory.

   /clarify needs to run inside an initialized project.
   Running it outside a repo can create files in the wrong
   place and cause a mess with worktrees and folders.

   What to do:
   - If this is a NEW project: run /init first (it sets up
     the repo and workflow files for you).
   - If the project exists elsewhere: navigate to that
     directory and run /clarify again.
   - If you just need a bare repo here: run `git init` first,
     then re-run /clarify.
   ```

   Do NOT proceed with the interview. Do NOT create any files.

3. If we ARE in a git repo but inside a `.claude/worktrees/` path, **STOP** and warn:

   ```
   ⚠️  You're inside a Claude worktree, not your main project.

   Navigate to your actual project directory before running
   /clarify. Worktrees are temporary — anything created here
   may not end up where you expect.
   ```

   Do NOT proceed.

---

You are about to help the user with a project or task. Before any work begins, conduct an interview to reach 95% confidence about what they actually want — not what they think they should want.

**Rules for the interview:**

1. Ask one question at a time. Wait for the answer.
2. Challenge assumptions the user is making. Don't just accept the framing.
3. Probe edge cases they haven't considered.
4. Ask about constraints (time, scope, dependencies, deployment, audience).
5. Ask about what success looks like — what does "done" mean for this?
6. Ask about what they explicitly do NOT want, or have ruled out.
7. If they describe a solution, ask about the underlying problem.
8. If they describe a problem, ask about prior attempts and why those failed.

**Stop conditions:**

You may stop the interview only when all of these are true:
- You can describe the goal in one sentence and the user would agree.
- You know the scope boundaries (what's in, what's out).
- You know the constraints (time, tech, audience).
- You know what "done" looks like.
- You have surfaced at least 2 assumptions and either confirmed or revised them.
- You have asked about at least 1 edge case the user hadn't mentioned.

When you're done:

1. State your 95% understanding back to the user in 3–6 bullet points.
2. Ask: "Does this match what you want? Anything to correct?"
3. After confirmation, write the summary to `PLAN.md` (creating it if missing) under a `## Goal` section.
4. Detect whether this is one task or several:
   - If one task: suggest `/decompose` if it's larger than half a day's work.
   - If several tasks: strongly suggest `/decompose`.
5. Tell the user the suggested next command based on tier:
   - Quick: start coding, optionally `/decompose` first.
   - Medium: `/ce:brainstorm` (if CE installed) or proceed to coding.
   - Heavy: `/office-hours` (if gstack installed) for product/eng review.

If `PLAN.md` already exists with content, append a new `## Goal` section with timestamp rather than overwriting.

---

**Project description (if user provided one with the command):** $ARGUMENTS
