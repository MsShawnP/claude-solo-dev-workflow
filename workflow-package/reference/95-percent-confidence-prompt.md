# 95% Confidence Prompt

Use at the start of every new project and at the start of every new
arc within an existing project. Run in chat (not Code) before any
coding begins.

The output of this conversation feeds into PLAN.md.

---

## The prompt

```
I'm about to start this project: [BRIEF DESCRIPTION].

Before anything else, tell me back what business question or business
case this project is answering, in one sentence. If you can't articulate
that clearly from my description, your first job is to ask me until you
can.

Then interview me until you have 95% confidence about what I actually
want, not what I think I should want. Challenge my assumptions. Ask
about edge cases I haven't considered. Ask one question at a time and
wait for my answer before moving on.

Throughout the interview, when you propose options or directions,
present at least two alternatives with tradeoffs rather than a single
suggestion.
```

---

## Why each piece is there

- **"Tell me back the business question"** — anchors the project on
  business value, not on the tool or skill being showcased
- **"Interview me until 95% confidence"** — flips the dynamic so the
  model asks instead of you prompting
- **"Not what I think I should want"** — surfaces the gap between the
  performative version of the project and the real one
- **"Challenge my assumptions"** — gives explicit permission to push
  back
- **"Edge cases I haven't considered"** — surfaces gaps in your
  thinking, not just gaps in the spec
- **"One question at a time"** — without this, you get a wall of
  questions and can't think carefully about any
- **"At least two alternatives with tradeoffs"** — addresses the
  failure mode where the model proposes the easy path without
  considering whether it's the right path
