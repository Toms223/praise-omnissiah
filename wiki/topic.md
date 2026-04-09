# Topic: Creation Rules

A **Topic** is a specific feature, concept, sub-system, or pattern within a tool. Topics are the second level of the wiki hierarchy, living inside tool folders and containing one or more `info` entries that dive into the details of that sub-area.

Topics are how the AI navigates from "I need to know about Python" to "I need to know about Python's asyncio runners" in two steps instead of searching through unstructured text.

---

## When to Create a Topic

Create a new topic subfolder when:

- A specific feature or concept within a tool is relevant to the current task and worth recording for future reference
- A core concept listed in the tool's `overview.md` needs its own dedicated space with multiple info entries
- Multiple distinct pieces of information about the same sub-area need to be organized together

**Do not** create a topic for:

- A single, self-contained fact — that is an `info` entry within an existing topic, not a new topic
- A concept so broad it applies to the whole tool — that belongs in `overview.md`
- A topic that already exists under a slightly different name — check the tool folder first and prefer extending an existing topic

---

## Naming Conventions

Topic folder names must be:

- **Kebab-case**: all lowercase, words separated by hyphens
- **Noun or noun-phrase**: describes *what* the topic is, not what you do with it
- **Specific enough** to distinguish from other topics in the same tool without being redundant
- **Stable**: the name should still be unambiguous a year from now

### Examples

```
wiki/Python/
├── asyncio/
├── type-hints/
└── decorators/

wiki/PostgreSQL/
├── indexing/
├── replication/
└── full-text-search/

wiki/Golang/
├── goroutines/
├── channels/
└── error-handling/
```

---

## Topic Folder Structure

```
wiki/[Tool]/[Topic]/
├── info_1.md    # First info entry for this topic
├── info_2.md    # Second info entry
└── ...
```

There is no index or README inside a topic folder. The tool's `overview.md` serves as the index. The topic name itself provides the orientation. Info entries are the substance.

---

## Topic vs. Info: The Distinction

Use this rule of thumb:

- If the sub-area has **multiple distinct facets** that each require their own explanation → create a **topic** with multiple info files
- If the sub-area is a **single, self-contained concept** → it is likely one info entry within an existing topic

**Example**: `asyncio` is a topic (it has coroutines, runners, event loops, tasks — multiple facets). `asyncio.Runner` is a single mechanism → one info entry within the `asyncio` topic, not its own topic.

---

## After Creating a Topic

1. Add the topic to the **Topics in This Wiki** section of the tool's `overview.md`
2. Create at least one `info` entry immediately — an empty topic folder carries no information and should not exist
3. Check whether any existing knowledge lessons reference this sub-area and add wiki links pointing to the new topic's info entries

---

## Topic Maintenance

A topic should be updated when:

- A new info entry is added (no structural change needed, but `overview.md` links may need updating)
- The sub-area is renamed in a new tool version (add a version note to existing info entries; do not rename the folder, as that breaks existing links)
- A cross-tool relationship is discovered — note the connection in the relevant info entries via a `&wiki|...|...&` link
