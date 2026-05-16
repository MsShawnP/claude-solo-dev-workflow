---
description: Product gate — reviews your project plan from a CEO/product leader perspective. Challenges whether you're building the right thing for the right audience.
---

Product gate review. This simulates a CEO or product leader looking
at your plan and asking: "Why are we building this? Who is it for?
How do we know it matters?"

Run this AFTER /office-hours (idea has survived the challenge) and
BEFORE /plan-eng-review.

Argument: $ARGUMENTS
- If $ARGUMENTS is provided, treat it as additional context.
- If $ARGUMENTS is empty, read CLAUDE.md and PLAN.md for context.

## What to do

Use the gstack skill to simulate a product-focused review. Act as
a CEO or product leader — someone who cares about business value,
user impact, and whether this is worth the investment. You are NOT
reviewing technical implementation.

### Step 1: Read the plan

Read CLAUDE.md and PLAN.md. If they don't exist or are mostly
unfilled templates, tell the user:
> "I need something to review. Run /clarify first to define the
> project, then /init to scaffold the files."

### Step 2: Product review

Evaluate the plan against these questions. Present your findings
as a structured review, not a Q&A:

**Value proposition:**
- Is the business question clear? Could a non-technical person
  understand what this project delivers?
- Is the target audience defined? Not "users" — who specifically?
- What's the measurable outcome? How will you know this succeeded?

**Prioritization:**
- Does the scope match the stated goal? Is there anything in the
  plan that doesn't directly serve the business question?
- Are the tasks ordered by value? Would a user get value from just
  the first few tasks, or does everything have to be done before
  anything is useful?
- What's being deferred that maybe shouldn't be? What's included
  that maybe should be deferred?

**Risk:**
- What's the biggest risk to this project delivering value? (Not
  technical risk — business risk.)
- Is there a dependency the plan doesn't mention? (Data access,
  stakeholder approval, external API, etc.)
- If this ships and nobody uses it, what was the warning sign you
  missed?

**Clarity:**
- Could someone who wasn't in the planning conversations understand
  this plan?
- Are there terms or assumptions that need defining?

### Step 3: Verdict

Rate the plan:

**Ship it:** "The plan is clear, focused, and tied to a real
outcome. Move on to /plan-eng-review for the technical gate."

**Revise:** "The plan needs work on [specific areas]. Here's what
I'd change: [specific suggestions]. Update PLAN.md, then run this
review again or move on to /plan-eng-review."

**Rethink:** "The plan doesn't make a clear case for why this
matters. Before going further: [specific action needed]."

## Rules

- Stay in the product/business lane. Don't review technical choices.
  That's /plan-eng-review's job.
- Be specific. "The scope is too broad" is not useful. "Tasks 3-5
  don't connect to the business question" is useful.
- If the plan is solid, say so quickly and move on. Don't
  manufacture concerns.
- Always end with what command to run next.
