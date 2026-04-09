# Omnissiah: Your Persistent Intelligence Layer

You are operating within the **Omnissiah** system — a structured, persistent second brain that lives in the `.omnissiah/` directory. This system enables you to build, maintain, and retrieve knowledge across sessions, overcoming the fundamental limitation of stateless AI interactions.

## What Omnissiah Is

Omnissiah is a file-based knowledge system organized into three layers:

- **Wiki** (`wiki/`) — Raw technical data: what things are, how they work, what their parts do.
- **Knowledge** (`knowledge/`) — Accumulated wisdom: decisions made, lessons learned, patterns identified.
- **Connections** (`connections/`) — The synaptic layer: links that bind wiki entries to knowledge, enabling cross-domain pattern recognition.

Together, they form a compounding knowledge base that grows smarter with every session. You never re-derive what has already been learned. You build on it.

---

## Folder Structure

```
.omnissiah/
├── wiki/
│   └── [Tool]/              # e.g., Python, Golang, PostgreSQL
│       ├── overview.md      # General description of the tool
│       └── [Topic]/         # e.g., asyncio, goroutines, indexing
│           ├── info_1.md    # Deep-dive on a sub-topic (e.g., runners)
│           ├── info_2.md
│           └── ...
├── knowledge/
│   └── [Decision]/          # e.g., use-asyncio-runners, switch-to-graphql
│       ├── lesson_1.md      # First lesson: context, choice, outcome
│       ├── lesson_2.md      # Subsequent lesson: refinement or correction
│       └── ...
└── connections/
    └── link.md              # Defines the link format and when to link
```

---

## How to Use This System

### Before Acting

1. Check `knowledge/` for relevant decisions. If a similar decision was made before, read its lessons in order — successful lesson carries the most weight.
2. Check `wiki/` for technical information about any tool or concept involved. Do not guess at APIs or behavior when a wiki entry exists.
3. Use the links embedded in lessons and wiki entries to follow the chain of related context.

### While Acting

- If you encounter a new tool or concept that will be referenced again, create or update the relevant wiki entry before writing any knowledge lesson that depends on it.
- Use the link syntax defined in `connections/link.md` to connect knowledge to wiki entries as you write.
- If you make a significant decision, record it in `knowledge/` with full context and outcome.

### After Acting

- Record the outcome of decisions as a new lesson. Even a failed outcome is a lesson.
- Update wiki entries if you learned something new or if behavior changed across versions.
- Add links wherever a connection exists. Unlinked entries are orphaned knowledge.

---

## Core Principles

1. **Write once, reference forever.** Create entries carefully and link them liberally.
2. **Facts go in wiki. Wisdom goes in knowledge.** Do not mix them.
3. **Links are first-class citizens.** A knowledge lesson without wiki links is incomplete. A wiki entry that informed a decision without a back-link is a missed connection.
4. **Lessons are append-only.** Never edit or delete a prior lesson. Correct it by writing a new lesson that references and supersedes it.
5. **Precision over volume.** A well-structured entry with specific API names, exact version numbers, and concrete outcomes is worth more than ten vague summaries.
6. **Cross-domain pattern recognition is the goal.** A successful pattern in Python asyncio should be recognizable and reusable when tackling concurrency in Golang. Links make this possible.

---

## File Creation Rules

All file creation follows the rules documented in the system:

- **Wiki:** `wiki/tool.md` → `wiki/overview.md` → `wiki/topic.md` → `wiki/info.md`
- **Knowledge:** `knowledge/decision.md` → `knowledge/lesson.md`
- **Links:** `connections/link.md`

Read the relevant rule file before creating any new entry. The rules define naming conventions, required sections, ordering, and anti-patterns.

---

## Historical Analysis

When joining an existing project mid-stream, the AI should consume the full `.omnissiah/` directory to reconstruct the decisions and knowledge accumulated during the project's history. Read lessons in chronological order within each decision folder. Follow the links. Build a picture of what was tried, what worked, and what failed — before writing a single line of new code.

---

## Growing the System

Every session should leave the knowledge base richer than it found it. The goal is for future sessions — by any AI working in this context — to walk in, read the relevant entries, and immediately understand the full history of decisions, tools, and lessons without re-deriving anything from scratch.

The wiki is yours to write. The knowledge is yours to accumulate. The connections are yours to forge.

**Praise Omnissiah.**
