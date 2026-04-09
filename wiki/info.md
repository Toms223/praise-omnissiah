# Info: Creation Rules

An **Info** entry is the atomic unit of knowledge in the wiki. Each `info_n.md` file captures one specific, self-contained piece of technical information about a topic within a tool. Info entries are what the AI reads when it needs precise, actionable facts — API names, behavior descriptions, version-specific details, known pitfalls.

Info entries answer: *exactly how does this work, and when do I use it?*

---

## When to Create an Info Entry

Create a new info entry when:

- A specific mechanism, API, pattern, or behavior needs to be recorded for future use
- Existing info entries in the topic do not cover this facet
- The AI learned something concrete and precise about a tool that it will need to recall

**Do not** create an info entry for:

- High-level summaries of a tool (those belong in `overview.md`)
- Broad conceptual introductions to a sub-area (those belong in the tool's `overview.md` Core Concepts section)
- Information that duplicates an existing entry — extend the existing entry with a new section instead

---

## Info File Format

```markdown
# [Descriptive Title — specific enough to be unambiguous without the folder context]

## Summary
[One to two sentences: what this entry captures. Precise enough that the AI can decide whether to read further or skip, based on the summary alone.]

## Details
[The actual technical content: API signatures, behavior descriptions, configuration options, version-specific notes, interactions with related mechanisms. Dense with signal.]

## When to Use
[Conditions under which this specific approach, mechanism, or API is the right choice.]

## When Not to Use / Pitfalls
[Known failure modes, constraints, version incompatibilities, or situations where this does not apply.]

## Example
[A minimal, illustrative code snippet or configuration. Should be complete enough to be copy-paste useful.]

## Links
[Cross-references to related wiki entries and knowledge decisions that use this info.]
```

---

## Naming Info Files

Info files are numbered sequentially within their topic folder: `info_1.md`, `info_2.md`, etc. The number is purely ordinal. The descriptive title lives inside the file.

If the topic grows large enough that ordinal numbering becomes confusing, use descriptive slugs: `info_runners.md`, `info_event-loop.md`, `info_tasks.md`. Choose one naming convention within a topic and use it consistently.

---

## Writing Guidelines

### Summary

The summary must be precise enough for the AI to decide — based on the summary alone — whether this entry is relevant to the current task. Compare:

- **Weak**: "This is about asyncio runners."
- **Strong**: "`asyncio.Runner` (Python 3.11+) is the recommended top-level entry point for running coroutines, providing explicit event loop lifecycle control that `asyncio.run()` does not offer."

### Details

- Specify version numbers when behavior differs across versions
- Include actual API names and signatures, not paraphrases
- Note interactions with related mechanisms explicitly
- Flag known bugs, gotchas, or non-obvious behaviors with a clear marker (e.g., **⚠ Pitfall:**)

### Example

Always include an example if the concept has a non-obvious usage pattern. The example should be minimal but complete — something the AI could reproduce without additional lookup.

### Links

Every info entry that has been used to justify a recorded decision must link to that decision. This makes the info entry traceable:

```markdown
## Links
- &knowledge|use-asyncio-runners/lesson_2& — decision that adopted this pattern
- &wiki|Python/asyncio/event-loop& — underlying mechanism this API manages
```

---

## Info Entry Lifecycle

1. **Created**: when a relevant technical fact is first encountered during real work
2. **Extended**: when new details are learned about the same mechanism — add to `Details`, do not create a duplicate entry
3. **Linked**: when a knowledge decision references this entry, add the link to the `Links` section
4. **Versioned**: if the information becomes outdated due to an API change, add a version note at the top (e.g., *"⚠ Deprecated in Python 3.12 — see `info_n+1.md`"*) and create a new entry for the current behavior. **Keep the old entry** — historical accuracy matters for lessons that reference it.

---

## Example Info Entry

```markdown
# asyncio.Runner — Top-Level Coroutine Lifecycle Management

## Summary
`asyncio.Runner` (Python 3.11+) is the recommended way to manage the event loop at the top level of an application. It provides explicit lifecycle control that `asyncio.run()` does not, including running multiple coroutines on the same event loop in sequence.

## Details
`asyncio.Runner` is a context manager that creates, runs, and closes an event loop:

```python
import asyncio

async def main():
    await asyncio.sleep(1)

with asyncio.Runner() as runner:
    runner.run(main())
```

Unlike `asyncio.run()`, `Runner` allows:
- Multiple coroutines to share the same event loop in sequence via `runner.run()`
- Explicit `close()` control for teardown ordering
- Custom event loop implementations via `loop_factory`

**⚠ Pitfall:** Do not use `asyncio.Runner` inside an already-running event loop — it raises `RuntimeError`. Use `await` directly instead.

## When to Use
- Any application that runs multiple coroutines sequentially at the top level
- When event loop lifecycle must be managed explicitly (e.g., setup → main → teardown)
- When integrating with frameworks that expect a long-lived event loop

## When Not to Use / Pitfalls
- Not available before Python 3.11; fall back to `asyncio.run()` for earlier versions
- Do not nest inside a running event loop

## Example
```python
async def setup(): ...
async def main(): ...
async def teardown(): ...

with asyncio.Runner() as runner:
    runner.run(setup())
    runner.run(main())
    runner.run(teardown())
```

## Links
- &knowledge|use-asyncio-runners/lesson_2& — decision that adopted this pattern over asyncio.run()
- &wiki|Python/asyncio/event-loop& — the event loop mechanism this API manages
```
