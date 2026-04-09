# Links: The Connectivity Layer

Links are the synaptic connections of the Omnissiah system. They bind knowledge lessons to wiki entries, trace *why* a decision was made back to *what* technical facts supported it, and enable the AI to recognize when a pattern from one domain applies to another entirely.

A knowledge base without links is a pile of files. Links are what make it a brain.

---

## Link Format

A link is written inline in any Omnissiah file using the following syntax:

```
&wiki|ToolName/TopicName/InfoName&
&knowledge|DecisionName/LessonName&
```

The path inside the link maps directly to the filesystem under `.omnissiah/`:

| Link | Resolves to |
|------|-------------|
| `&wiki|Python/asyncio/runners&` | `.omnissiah/wiki/Python/asyncio/info_runners.md` |
| `&wiki|Golang/goroutines/channels&` | `.omnissiah/wiki/Golang/goroutines/info_channels.md` |
| `&knowledge|use-asyncio-runners/lesson_2&` | `.omnissiah/knowledge/use-asyncio-runners/lesson_2.md` |

### Wiki Link

Points to a specific info entry within a tool's topic folder:

```
&wiki|Python/asyncio/runners&
&wiki|PostgreSQL/indexing/partial-indexes&
&wiki|React/hooks/use-effect&
```

### Knowledge Link

Points to a specific lesson within a decision folder:

```
&knowledge|use-asyncio-runners/lesson_1&
&knowledge|switch-to-graphql/lesson_3&
&knowledge|avoid-global-state/lesson_2&
```

---

## When to Create Links

### Mandatory: In Knowledge Lessons → Wiki

Every knowledge lesson must link to the wiki entries that technically ground the decision. A lesson without at least one wiki link is incomplete.

```markdown
We chose `asyncio.Runner` over plain `asyncio.run()` for lifecycle control.
&wiki|Python/asyncio/runners&
```

### Mandatory: In Knowledge Lessons → Prior Lessons

When a lesson corrects, builds on, or directly follows from a prior lesson in the same decision folder, link to it in the `References` section.

```markdown
## References
- Corrects: &knowledge|use-asyncio-runners/lesson_1& — naive await blocked the thread
- Confirms: &knowledge|use-asyncio-runners/lesson_2& — runner pattern held under load
```

### Recommended: In Wiki Info Entries → Knowledge

When a wiki info entry has been used to justify a recorded decision, link back to that decision. This makes the info entry traceable — you can see which choices it influenced.

```markdown
## Links
- &knowledge|use-asyncio-runners/lesson_2& — decision that adopted this pattern
```

### Recommended: In Wiki Info Entries → Other Wiki Entries

When a concept in one tool's wiki directly mirrors or depends on a concept in another tool's wiki, link them. This is the foundation of cross-domain pattern recognition.

```markdown
The event loop concept here mirrors &wiki|Golang/goroutines/scheduler& in Go's runtime.
```

---

## How the AI Accesses Links

When reading a file that contains links, the AI must:

1. **Recognize** any `&...|...&` pattern as a link to a connected Omnissiah entry.
2. **Resolve** the link to its path: `&wiki|Python/asyncio/runners&` → `.omnissiah/wiki/Python/asyncio/info_runners.md`
3. **Fetch** the linked file when the current task requires that additional context.
4. **Follow chains**: a knowledge lesson may link to a wiki entry that links back to another decision. Follow the chain as deep as the current task requires.

The AI does not need to resolve every link on every read — only the links that are relevant to the task at hand.

---

## Cross-Domain Pattern Recognition

The compounding power of links emerges when patterns cross domains. Example chain:

1. `&wiki|Python/asyncio/runners&` is created to record how Python manages concurrent I/O.
2. `&knowledge|use-asyncio-runners/lesson_2&` links to it — the decision to adopt runners succeeded.
3. Later, working in Golang, the AI recognizes the same structural pattern in `errgroup`.
4. `&wiki|Golang/goroutines/errgroup&` is created, linking back to the Python equivalent.
5. `&knowledge|use-goroutine-groups/lesson_1&` links to both wiki entries, making the cross-domain insight explicit and reusable.

This is how the system compounds across languages, frameworks, and domains over time.

---

## Rules

- **Links must resolve to existing files.** Do not write a link to a file that does not yet exist. Create the file first.
- **Use the shortest unambiguous path.** Do not repeat the tool name unnecessarily.
- **An info entry with no inbound knowledge links** is a signal: has the decision that used this fact been recorded? If not, record it.
- **A knowledge lesson with no wiki links** is incomplete. Identify the technical facts that supported the decision and link them.
- **Do not embed links in headings.** Place links inline in body text or in a dedicated `Links` section.
