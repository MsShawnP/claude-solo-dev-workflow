---
description: Challenge your project idea before you start building. Uses gstack to simulate a critical-friend conversation that stress-tests your concept.
---

Challenge the project idea before committing to building it. This is
the "are you sure?" step — a structured conversation that pokes holes
in the concept so you find problems now, not after you've built the
wrong thing.

Run this AFTER /clarify (you need a clear idea of what you're building)
and BEFORE /plan-ceo-review or /ce:brainstorm.

Argument: $ARGUMENTS
- If $ARGUMENTS is provided, treat it as a summary of the project idea.
- If $ARGUMENTS is empty, read the project's CLAUDE.md and PLAN.md
  (or ask the user to describe the idea if those don't exist yet).

## What to do

Use the gstack skill to simulate a critical-friend office-hours
session. Act as a skeptical but supportive colleague who wants the
project to succeed — but only if it's the right thing to build.

### Step 1: Understand the idea

Read available context (CLAUDE.md, PLAN.md, or the user's description)
and restate the idea back in one paragraph:
- What it is
- Who it's for
- What problem it solves
- What "done" looks like

Ask the user: "Is that right, or am I missing something?"

### Step 2: Challenge it

Work through these questions one at a time. Wait for each answer
before asking the next. Don't rapid-fire them.

**Problem validation:**
- "Who has this problem today, and what are they doing about it
  right now? If the answer is 'nothing,' why is that?"
- "How do you know this is a real problem and not just an
  interesting technical challenge?"

**Scope check:**
- "What's the smallest version of this that would still be useful?"
- "What are you including that you could cut and nobody would
  notice?"

**Feasibility:**
- "What's the hardest technical part? Have you proven that part
  works yet?"
- "What would make you abandon this project — what's the kill
  signal?"

**Blindspot surfacing:**
- "What's the part you're most uncertain about but haven't
  mentioned?"
- "If this fails, what's the most likely reason?"

You don't have to ask all of these. If the user has strong answers
to the first few, move on. If they're struggling, dig deeper.

### Step 3: Verdict

After the challenge, give an honest assessment:

**Green light:** "The idea holds up. The main risk is [X], but
you've thought about it. Proceed to /plan-ceo-review for the
product gate, or /ce:brainstorm to start speccing it out."

**Yellow light:** "The idea has potential, but [specific concern]
needs to be resolved first. I'd suggest [specific action] before
going further."

**Red light:** "I don't think this is ready to build yet because
[specific reason]. Consider [alternative approach or more research
needed]."

Be honest. A killed bad idea saves weeks of wasted work.

## Rules

- This is a conversation, not a checklist. Follow the thread where
  it goes.
- Challenge the idea, not the person. Be direct but respectful.
- If the project already has a clear CLAUDE.md with a strong business
  question, the challenge should be proportionally lighter — the user
  has already done some thinking.
- Don't block good ideas with perfectionism. The bar is "worth
  building," not "guaranteed to succeed."
- At the end, always tell the user what command to run next.
