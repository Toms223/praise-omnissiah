# 🌌 Praise Omnissiah

> **Empowering AI to learn, remember, and evolve through structured contextual knowledge.**

## 🎯 Overview

The **Praise Omnissiah** project addresses a fundamental limitation in current AI tooling: the lack of persistent memory and true experiential learning. While models can remember basic user preferences (like a favorite IDE or language), they don't truly "learn" from their mistakes or successes in a way that shifts their future behavior—their underlying weights remain static.

This project bridges that gap by enabling the AI to behave like a **diligent digital apprentice**. It meticulously takes notes and builds a persistent "second brain"—much like an Obsidian notebook—to leverage past context for smarter, more informed decision-making.

---

## 📚 Wiki: The Information Hub

The **Wiki** is the central repository for raw data. It serves as the project's memory bank, where the AI stores technical information it needs to recall later.

*   **Role:** Capturing "absolute raw data" from documentation, existing codebases, or project requirements.
*   **Process:** When an AI encounters new libraries or tools, it filters out the noise and saves only the relevant data to the corresponding wiki files.
*   **Organization:**
    *   **Wiki/**
        *   **[Tool]/ ** (e.g., *Python*)
            *   **Overview.md:** General information about the tool.
            *   **Topic.md:** Specific features or concepts (e.g., *asyncio*).
                *   *Info 1, Info 2, ... Info n:* Deep-dives into sub-topics (e.g., *runners*).

---

## 🧠 Knowledge: The Decision Engine

While the Wiki stores *data*, **Knowledge** stores *wisdom*. This section tracks the logic and outcomes behind every choice the AI makes.

*   **Learning from Experience:** Every decision is recorded along with its outcome (success or failure) and the underlying reasoning.
*   **Continuous Improvement:** Before acting, the AI reviews relevant lesson files to see if similar decisions were made previously, adjusting its approach based on past success or user corrections.
*   **Historical Analysis:** The AI can consume an entire existing project to "re-learn" the decisions made during its development, identifying both good practices and mistakes to avoid.
*   **Organization:**
    *   **Knowledge/**
        *   **[Decision]/ ** (e.g., *Use asyncio*)
            *   **Lesson_1.md, Lesson_2.md...** (e.g., *Failed using simple awaitables; Succeeded using Runners.*)

---

## 🔗 Links: The Connectivity Layer

**Links** are the "synapses" of the system. Rather than standalone files, they are a specific formatting convention used across all entries to connect the Wiki and Knowledge bases.

*   **Contextual Rationale:** Links explicitly tell the AI: *"This decision was made because of this specific wiki entry."*
*   **Pattern Recognition:** By leveraging the indexing power of RAGs (Retrieval-Augmented Generation), the AI can link similar decisions across different domains.
*   **Cross-Pollination:** For example, a successful pattern found in **Python's** asyncio runners might be linked and repurposed when the AI is tasked with implementing concurrent functions in **Golang**.
