# Lesson: Creation and Referencing Rules

A **Lesson** is the unit of experiential knowledge in the Omnissiah system. Each lesson records a single instance of a decision being made, tested, corrected, or refined. Lessons are what the AI reads before making a choice — the distilled experience that prevents repeating mistakes and reinforces what works.

Lessons are the memory. Everything else in the system exists to make lessons findable and trustworthy.

---

## When to Create a Lesson

Create a new lesson when:

- A decision is first made and applied (even if the outcome is not yet confirmed)
- A previous approach **fails** — record precisely why it failed and what was tried next
- A previous approach **succeeds** — record precisely why it worked and what confirmed it
- A user provides feedback that revises the AI's approach — the revision is itself a lesson
- The same decision is revisited in a new context with a meaningfully different outcome

---

## Lesson File Format

Every lesson file follows this structure:

```markdown
# Lesson [N]: [Brief Title]

## Context
[What was being built or solved. What problem triggered this decision. What constraints or requirements existed. One to three paragraphs.]

## Decision
[The specific choice made. Be precise — not "we used async" but "we used asyncio.Runner instead of asyncio.run() to manage the event loop lifecycle explicitly."]

## Reasoning
[Why this choice was made over the alternatives considered. What technical facts supported it. Reference wiki entries here.]

## Outcome
[What happened. Success, partial success, or failure. What evidence confirmed the outcome — test results, user feedback, observed behavior. If the outcome is not yet known, write "Pending — to be updated in lesson_[N+1]".]

## Links
[All wiki and knowledge links relevant to this lesson. At minimum, one wiki link grounding the decision in technical fact.]

## References
[Optional. Links to prior lessons in this decision folder that this lesson corrects, builds on, or supersedes.]
```

---

## Required Fields

| Field | Required | Notes |
|-------|----------|-------|
| Context | Always | Without context, a lesson cannot be reused intelligently |
| Decision | Always | The specific action taken, as precisely as possible |
| Reasoning | Always | Explain the "why" — this is where wisdom lives |
| Outcome | Required when known | Mark as `Pending` if session ended before outcome was clear |
| Links | Always | At least one wiki link. Create the wiki entry first if it doesn't exist |
| References | When applicable | Required when correcting or building on a prior lesson |

---

## Lesson Numbering

Lessons are numbered sequentially within their decision folder: `lesson_1.md`, `lesson_2.md`, etc. The number reflects chronological order, not importance. **Never renumber existing lessons.** The sequence is the historical record.

---

## Referencing Lessons

### Inline in any Omnissiah file

```
&knowledge|use-asyncio-runners/lesson_2&
```

### In a lesson's References section

```markdown
## References
- Corrects: &knowledge|use-asyncio-runners/lesson_1& — naive await blocked the main thread
- Builds on: &knowledge|use-asyncio-runners/lesson_2& — confirmed the runner pattern under load
- See also: &knowledge|use-goroutine-groups/lesson_1& — same structural pattern in Golang
```

---

## Before Making a Decision

The AI must always:

1. Check whether a decision folder for this choice exists in `knowledge/`
2. If it exists, read all lessons in chronological order
3. Weight the most recent successful lesson most heavily
4. If the current context differs significantly from prior lessons, note the difference explicitly in the new lesson
5. If no relevant decision folder exists, check adjacent decisions — a lesson about `use-asyncio-runners` may still be informative when evaluating `use-goroutine-groups` in Golang

---

## Lesson Lifecycle

```
New session
    ↓
Check knowledge/ for relevant decisions
    ↓
Read lessons in order → inform current decision
    ↓
Apply decision → observe outcome
    ↓
Write lesson_n.md with full context, decision, reasoning, and outcome
    ↓
If outcome confirms or contradicts a prior lesson → write lesson_n+1.md referencing it
```

---

## Anti-Patterns to Avoid

- **Vague outcomes**: "It worked" is not an outcome. "The event loop completed without blocking the main thread across three integration tests under concurrent load" is an outcome.
- **Missing links**: A lesson without wiki links severs the connection between wisdom and data. Always link the technical facts that grounded the decision.
- **Editing prior lessons**: Prior lessons are historical record. If a lesson was wrong, write a new lesson that says so and references the wrong one. Do not rewrite history.
- **Duplicate decision folders**: If a lesson for this exact decision already exists in another folder name, add a cross-reference link rather than creating a parallel folder with a different name.
- **Pending outcomes left forever**: If a lesson was written with `Pending` outcome, revisit it in the next session. A lesson with a permanent `Pending` outcome is a gap in the knowledge base.
