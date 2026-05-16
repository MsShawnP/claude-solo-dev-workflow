---
description: QA testing — uses gstack headless browser to test your project in a real browser. Checks that things actually work, not just that the code compiles.
---

QA testing pass. Uses the gstack headless browser to open your
project, click through it, and verify that things actually work
the way they should.

Run this AFTER /ce:work (you've built something) or AFTER /improve
(you've fixed things) and BEFORE /ce:compound or shipping.

Argument: $ARGUMENTS
- If $ARGUMENTS is provided, treat it as what to focus testing on
  (e.g., "the login flow" or "the new chart").
- If $ARGUMENTS is empty, test the main user flows.

## Step 1: Figure out what to test

Read PLAN.md to understand what was built or changed. Identify:

1. **Golden path:** The main thing a user does with this project.
   If it's a web app, that's the primary user flow. If it's a
   report, that's opening and reading it. If it's an API, that's
   the main endpoint.

2. **Recent changes:** What was built or fixed in the current arc
   or improvement pass? These need testing because they're new.

3. **Edge cases:** Based on the golden path, what could go wrong?
   Empty states, bad input, missing data, very long content,
   mobile viewport.

Tell the user what you plan to test before starting:
> "Here's what I'm going to test:
> 1. [golden path]
> 2. [recent change]
> 3. [edge case]
> Anything else you want me to check?"

## Step 2: Start the project

Figure out how to run the project:
- Check CLAUDE.md for the entry point
- Look for common start commands (npm start, python app.py,
  quarto preview, etc.)
- Check package.json scripts, Makefile, or README for run
  instructions

If you can't figure out how to start it, ask the user.

Use the gstack skill to start a headless browser and navigate to
the project.

## Step 3: Test the golden path

Walk through the primary user flow step by step:

1. Take a screenshot at each major step
2. Verify the page loaded correctly (no error messages, no
   missing content, no broken layouts)
3. Interact with elements (click buttons, fill forms, navigate)
4. Check that the result of each action is what you'd expect

Report each step as you go:
> "Step 1: Opened the homepage — looks good, all sections loaded."
> "Step 2: Clicked 'Get Started' — form appeared, all fields present."
> "Step 3: Submitted the form — got an error: [screenshot]"

## Step 4: Test recent changes

For each thing that was built or fixed in this arc:
- Navigate to it
- Verify it works as described in PLAN.md
- Take a screenshot showing it working (or not)

## Step 5: Test edge cases

Based on the project type, check relevant edge cases:

**Web apps / UI:**
- Empty states (no data yet, new user)
- Long content (does it overflow or truncate properly?)
- Mobile viewport (resize to 375px width)
- Error states (what happens when something fails?)
- Loading states (is there feedback while things load?)

**Reports / dashboards:**
- Do charts display correctly?
- Do numbers match their labels?
- Does the layout work at different zoom levels?

**APIs / data pipelines:**
- Invalid input (empty, wrong type, too large)
- Missing required fields
- Concurrent requests (if applicable)

You don't have to test everything — pick the 3-4 most likely
failure points.

## Step 6: Report

Present findings in this format:

```
QA RESULTS — [date]
Tested: [what was tested]
Environment: [browser, viewport, etc.]

PASSED:
- [thing that worked] ✓
- [thing that worked] ✓

FAILED:
- [thing that didn't work] ✗
  What happened: [description]
  Expected: [what should have happened]
  Screenshot: [reference to screenshot]

NOT TESTED:
- [thing skipped and why]
```

After the report:
- If everything passed → "QA looks good. Ready for /ce:compound
  to capture learnings, then ship."
- If there are failures → "Found [N] issues. Want to fix them now?
  After fixing, run /qa again to verify."

## Rules

- Test behavior, not code. You're checking what the user sees and
  experiences, not whether the code is clean.
- Take screenshots. A screenshot of a bug is worth more than a
  description of a bug.
- Don't test things that can't be tested in a browser (internal
  functions, database queries, etc.). Those are /ce:review's job.
- If the project can't be tested in a browser (pure library, CLI
  tool, data pipeline), say so and suggest alternative verification
  approaches instead.
- If gstack can't start or the project won't run, report the
  specific error. Don't skip QA silently.
- Always end with what command to run next.
