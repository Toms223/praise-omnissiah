# Tool: Creation Rules

A **Tool** is any library, language, framework, runtime, protocol, or external service that the AI interacts with and needs to remember. In the Omnissiah system, each tool gets its own folder in `wiki/`, acting as the root of all knowledge about that tool.

The tool folder is the address of a tool's knowledge. Everything the AI has ever learned about a tool lives under it.

---

## When to Create a Tool Folder

Create a new tool folder when:

- A new library, language, or framework is introduced to the project
- The AI needs to record specific technical facts about a tool for future reference
- A tool is used in a decision that must be recorded in `knowledge/` and there is no existing wiki entry for it

**Do not** create a tool folder for:

- One-off internal helpers or scripts with no external documentation
- Pure concepts with no concrete implementation (e.g., "concurrency" as a concept — instead, create a topic within the relevant language tool)
- A tool that is a variant of one that already has a folder — use the canonical name

---

## Naming Conventions

Tool folder names must use the official, canonical name of the tool:

- **PascalCase** for proper nouns and branded tools: `Python`, `Golang`, `PostgreSQL`, `React`, `FastAPI`
- **Lowercase** for generic protocols or formats: `rest`, `grpc`, `oauth2`, `json`
- **No aliases or nicknames**: use `Golang` not `Go`, use `PostgreSQL` not `Postgres`

### Examples

```
wiki/
├── Python/
├── Golang/
├── PostgreSQL/
├── React/
├── FastAPI/
├── Docker/
└── grpc/
```

---

## Tool Folder Structure

```
wiki/[Tool]/
├── overview.md         # Required: created immediately when the folder is created
└── [Topic]/            # Added as the AI encounters relevant sub-areas
    ├── info_1.md
    ├── info_2.md
    └── ...
```

The **only required file** when creating a new tool folder is `overview.md`. Topics and info entries are added progressively as the AI encounters relevant sub-areas during real work.

---

## Creating a Tool Folder: Checklist

1. Confirm no folder for this tool already exists in `wiki/` under any spelling or alias
2. Create the folder: `wiki/[ToolName]/`
3. Create `overview.md` following the rules in `wiki/overview.md` — this file must exist before any topic is created
4. Identify the first topic relevant to the current task. If a topic is immediately needed, create the topic subfolder and its first info entry
5. Update any knowledge lessons that reference this tool by adding wiki links to the newly created entries

---

## Relationship to Knowledge

Tool wiki entries are the factual substrate that knowledge lessons draw upon. When a decision is recorded in `knowledge/`, the wiki entries providing technical support for that decision must exist and be linked.

If the required wiki entries do not exist at the time of writing a lesson:

1. Create the tool folder and `overview.md` first
2. Create the relevant topic subfolder and info entry
3. Then write the knowledge lesson, linking to the newly created wiki entries

This order ensures no dangling links exist in the knowledge base.

---

## Tool Maintenance

A tool folder should be updated when:

- A new version introduces behavior changes relevant to recorded decisions
- An info entry becomes outdated (note the version change, do not delete — see `wiki/info.md`)
- A new topic within the tool becomes relevant to the project
- A cross-tool link is established (update the `Links` section in the relevant info or overview)

The wiki is a living document. A tool folder that has not been updated in a long time may contain stale information — flag it with a version note rather than leaving it silently incorrect.
