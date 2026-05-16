---
description: Architecture gate — reviews your project plan from an engineering perspective. Checks whether the technical approach will actually work.
---

Architecture gate review. This simulates a senior engineer looking
at your plan and asking: "Will this approach actually work? What's
going to break? What are you not thinking about?"

Run this AFTER /plan-ceo-review (plan has product approval) and
BEFORE /ce:brainstorm or /ce:plan.

Argument: $ARGUMENTS
- If $ARGUMENTS is provided, treat it as additional context.
- If $ARGUMENTS is empty, read CLAUDE.md and PLAN.md for context.

## What to do

Use the gstack skill to simulate an engineering-focused review. Act
as a senior engineer or technical lead — someone who has seen many
projects succeed and fail, and knows where the bodies are buried.
You are NOT reviewing business value. That was /plan-ceo-review's
job.

### Step 1: Read the plan

Read CLAUDE.md and PLAN.md. Look specifically at:
- Stack and tools listed in CLAUDE.md
- Tasks and their ordering in PLAN.md
- Any existing code in the project

If there's no technical detail to review, tell the user:
> "There's not enough technical detail to review yet. Run
> /ce:brainstorm to spec out the approach, then come back for
> the architecture review."

### Step 2: Engineering review

Evaluate the technical approach:

**Stack fit:**
- Does the chosen stack make sense for this problem? Is there
  a simpler option that would work just as well?
- Are there dependency risks? Libraries that are unmaintained,
  have licensing issues, or are overkill for the use case?
- Does the stack match the developer's experience level, or is
  it aspirational? (Aspirational is fine if acknowledged.)

**Architecture:**
- Does the plan describe how data flows through the system? If
  not, where are the likely surprises?
- What's the most complex integration point? Has it been proven
  to work, or is it assumed?
- Are there scaling concerns that matter at the expected usage
  level? (Don't flag theoretical scale issues for a personal
  project.)

**Task ordering:**
- Are the tasks ordered so that risky/uncertain work comes
  first? You want to fail fast on the hard parts, not discover
  a blocker after building everything else.
- Are there tasks that should be broken down further? A task
  like "build the backend" is too big to estimate or verify.
- Are there missing tasks? Common ones that get forgotten:
  error handling, authentication, deployment, data migration,
  testing.

**Failure modes:**
- What happens when things go wrong? (API down, bad data,
  network failure, user does something unexpected.)
- What's the rollback plan if the approach doesn't work?
- Are there any irreversible decisions in the plan? (Schema
  choices, external API commitments, public interfaces.)

**Security (quick check):**
- Does the plan involve user input, authentication, or
  sensitive data? If so, is there any mention of how those
  are handled?
- Any obvious risks? (Hardcoded secrets, no input validation,
  data exposed publicly.)

### Step 3: Verdict

Rate the technical approach:

**Sound:** "The technical approach is solid. Known risks are
manageable. Proceed to /ce:brainstorm to spec it out, or
/ce:plan if the spec is clear enough."

**Needs work:** "The approach will probably work, but [specific
concerns]. Suggestions: [specific changes]. Update the plan,
then proceed."

**Risky:** "There's a significant technical risk that hasn't
been addressed: [specific risk]. Before building, you should
[specific action to de-risk — prototype, research, ask someone
with experience]."

## Rules

- Stay in the technical lane. Don't second-guess business
  decisions — that was /plan-ceo-review's job.
- Match the review depth to the project tier. A Quick-tier
  script doesn't need a full architecture review. A Heavy-tier
  product does.
- Don't recommend over-engineering. A solo developer's personal
  project doesn't need microservices, CI/CD pipelines, or 100%
  test coverage at the planning stage.
- Be specific about risks. "This could be a problem" is not
  useful. "If the API rate-limits you at 100 req/min, the batch
  import of 50K records will take 8+ hours" is useful.
- Always end with what command to run next.
