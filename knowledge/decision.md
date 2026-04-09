# Decision: Creation Rules

A **Decision** is any significant choice made during a project or interaction — a technology selected, an architecture adopted, a pattern preferred over its alternatives. The `knowledge/` directory stores these decisions as folders, each containing the lessons learned from making and living with that choice.

Decisions are not opinions. They are recorded choices with context, reasoning, and observable outcomes.

---

## When to Create a Decision Folder

Create a new decision folder when:

- A non-trivial technical or architectural choice is made (e.g., "use asyncio runners", "switch to GraphQL", "adopt hexagonal architecture")
- A recurring pattern is identified as the preferred approach for this codebase
- An approach is explicitly **rejected** in favor of another — the rejection is itself a decision worth recording
- A user corrects the AI's approach — the correction is a decision
- A prior attempt failed and a new approach was chosen — record both

**Do not** create a decision folder for:

- Trivial implementation details with no lasting architectural relevance
- Pure fact-recording (that belongs in the wiki)
- Temporary workarounds, unless the workaround becomes permanent

---

## Naming Conventions

Decision folder names must be:

- **Kebab-case**: all lowercase, words separated by hyphens
- **Action-oriented**: begin with a verb prefix — `use-`, `prefer-`, `avoid-`, `adopt-`, `switch-to-`, `reject-`
- **Specific**: `use-asyncio-runners` is better than `use-asyncio` when the lesson is specifically about runners
- **Timeless**: the name should make sense regardless of when it is read

### Good Examples

```
knowledge/
├── use-asyncio-runners/
├── prefer-postgres-over-sqlite/
├── adopt-hexagonal-architecture/
├── avoid-global-state/
├── reject-orm-for-complex-queries/
└── switch-to-graphql/
```

### Bad Examples

- `async/` — not action-oriented, too vague
- `the-database-decision/` — verbose, not timeless
- `fix-bug-123/` — this is a task, not a decision

---

## Decision Folder Structure

Each decision folder contains only lesson files:

```
knowledge/[decision-name]/
├── lesson_1.md    # First recorded lesson about this decision
├── lesson_2.md    # Subsequent lesson: refinement, correction, or new context
└── lesson_n.md
```

Lesson files are numbered sequentially. New lessons are always appended — **never edit or delete existing lessons**. Prior lessons are an immutable historical record. Correct a wrong lesson by writing a new lesson that references and supersedes it.

---

## Before Creating a Decision Folder

Always check first:

1. Does a decision folder for this choice already exist in `knowledge/`? If so, add a new lesson to it rather than creating a parallel folder.
2. Does an existing lesson in an adjacent folder cover the same ground? If so, note the connection in the new lesson via a `&knowledge|...|...&` link.
3. Is this truly a decision or is it a fact? Facts belong in `wiki/`. Decisions belong in `knowledge/`.

---

## Relationship to Wiki

Every decision should be grounded in one or more wiki entries. The wiki provides the *what* (technical facts); the knowledge provides the *why* (reasoning and outcome).

When creating a decision folder:

1. Identify which tools and topics are technically foundational to this decision.
2. Ensure those wiki entries exist. If they don't, create them first.
3. When writing lessons, link them to the relevant wiki entries using the format defined in `connections/link.md`.

A decision folder without wiki links is a belief, not a grounded choice.
