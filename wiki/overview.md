# Overview: Creation Rules

The `overview.md` file is the entry point for every tool in the wiki. It is the first file an AI reads when encountering a tool — its job is to provide immediate orientation: what the tool is, what problem it solves, when to use it, when not to, and how this wiki organizes its knowledge about it.

A good overview makes every subsequent navigation decision faster.

---

## When to Write an Overview

An `overview.md` must be written:

- When a new tool folder is created (always — it is the first and only required file)
- When the tool's positioning changes significantly (new major version, paradigm shift, deprecated status)

Update the overview in place. The overview is a living summary, not an immutable record — unlike lessons, it is meant to reflect the current state of the AI's understanding.

---

## Overview File Format

```markdown
# [Tool Name]

## What It Is
[One to three sentences: what the tool is and what specific problem it solves. No filler, no marketing language. The AI already knows what's popular.]

## Primary Use Cases
[Bullet list of the main scenarios where this tool is the right choice for this project or context.]

## Core Concepts
[The 3–7 fundamental concepts needed to understand this tool. Each concept should eventually correspond to a topic subfolder.]

- **[Concept]**: [One-line definition precise enough to distinguish it from similar concepts in other tools]
- **[Concept]**: [One-line definition]

## When Not to Use
[Explicit trade-offs and scenarios where a different tool is preferable. This section prevents the AI from defaulting to a familiar tool when another is superior.]

## Topics in This Wiki
[A manually maintained index of topic subfolders. Updated every time a new topic is created.]

- [topic-folder-name]: [One-line description of what this topic covers]

## Links
[Knowledge decisions that reference this tool. Updated when a new lesson links to this tool's wiki.]

- &knowledge|decision-name/lesson_n&
```

---

## Writing Guidelines

### What It Is

Be precise about what distinguishes this tool from its nearest alternatives. "asyncio is Python's built-in cooperative concurrency framework using an event loop" is useful. "asyncio is a popular async library" is not.

### Core Concepts

These must correspond to real topic subfolders, or be a signal that a topic subfolder should be created. If you write a core concept in the overview but no topic subfolder exists for it yet, that gap is intentional — it marks work to be done when the concept becomes relevant.

### When Not to Use

This section is mandatory and must be honest. Every tool has trade-offs. Recording them prevents the AI from defaulting to familiarity over fitness.

```markdown
## When Not to Use
- CPU-bound parallelism at scale: Python's GIL limits true thread-level parallelism; use Golang or multiprocessing instead.
- Sub-millisecond latency requirements: GC pauses and interpreter overhead are constraints.
```

### Topics in This Wiki

Update this list every time a new topic subfolder is created under this tool. It serves as a fast index — the AI reads this to decide which topic to navigate to without listing the filesystem.

---

## Length and Detail

An overview should be:

- **Scannable in under 30 seconds** — it is an orientation document, not a tutorial
- **Dense with signal** — every line should tell the AI something it can act on
- **Free of repetition** — if a concept needs more than one line, it belongs in a topic entry

Typical length: 150–400 words.

---

## Example

```markdown
# Python

## What It Is
A dynamically typed, interpreted, general-purpose language optimized for developer productivity and ecosystem breadth. CPython is the reference implementation; PyPy provides JIT compilation as an alternative.

## Primary Use Cases
- Data science, ML, and numerical computation (NumPy, PyTorch, pandas)
- Web backends (FastAPI, Django, Flask)
- Automation, scripting, and CLI tooling
- Glue code between systems with heterogeneous APIs

## Core Concepts
- **GIL (Global Interpreter Lock)**: Prevents true thread-level CPU parallelism in CPython; all threads share one OS thread at the bytecode level.
- **asyncio**: Cooperative multitasking via a single-threaded event loop; suited for I/O-bound concurrency, not CPU-bound.
- **Decorators**: First-class function wrappers enabling meta-programming patterns.
- **Type Hints**: Optional static typing via the `typing` module, enforced by mypy or pyright at check time, ignored at runtime.

## When Not to Use
- CPU-bound parallelism at scale: prefer Golang or Rust; Python's GIL is a hard constraint.
- Sub-millisecond latency requirements: GC pauses and interpreter overhead are measurable.
- Mobile or embedded targets: CPython has limited runtime support.

## Topics in This Wiki
- asyncio: Cooperative concurrency via event loop, coroutines, and runners.
- type-hints: Static typing system, typing module, and enforcement tooling.

## Links
- &knowledge|use-asyncio-runners/lesson_2&
```
