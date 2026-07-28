# Meta Phase Guide (Cross-Cutting)

The `meta` directory holds cross-cutting skills that are not specific to any single SDLC phase. These skills apply across the entire lifecycle and are invoked whenever their concern is relevant, regardless of which phase you are in.

---

## Phase Overview

| Component | Count | Details |
|-----------|------:|---------|
| Utilities | 1 | `context-engineering` |
| Templates | 0 | Meta skills are workflow-based |

> Per the factory rules, `meta` is **not an SDLC phase** — it is a directory for cross-cutting, non-phase-specific skills. Meta skills are listed separately from the SDLC phase pipeline.

---

## The Context Engineering Workflow

The `context-engineering` skill optimizes agent context setup. It curates what an agent sees in its context window deliberately, following a strict hierarchy: rules files → specs → source files → error output → conversation history. When context is too large, it applies packing strategies (summarize, prune, progressive disclosure) and leverages MCP integrations.

---

## Context Engineering Workflow Diagram

```mermaid
flowchart TD
    Start([Start: new session or<br/>context quality degrading]) --> Trigger{"Why invoke<br/>context engineering?"}

    Trigger -- "Starting a new session" --> Plan["Plan the context hierarchy"]
    Trigger -- "Output quality degrading" --> Diagnose["Diagnose: what's in context?<br/>Is the right information loaded?"]
    Trigger -- "Switching between tasks" --> Diagnose

    Diagnose --> Confused{"Agent confused or<br/>output degrading?"}
    Confused -- Yes --> Manage["Confusion management:<br/>reduce context, reload from source,<br/>restate the goal"]
    Confused -- "No — just optimizing" --> Plan

    Manage --> Plan
    Plan --> Hierarchy["Build the context hierarchy<br/>(top = highest priority, loaded first)"]

    Hierarchy --> L1["1. Rules files<br/>AGENTS.md, project standards,<br/>coding conventions"]
    L1 --> L2["2. Specs & requirements<br/>SRS, user stories, relevant docs"]
    L2 --> L3["3. Source files<br/>Code relevant to the current task"]
    L3 --> L4["4. Error output<br/>If debugging — the actual error"]
    L4 --> L5["5. Conversation history<br/>Minimal, relevant only"]

    L5 --> TooLarge{"Context too<br/>large for the model?"}
    TooLarge -- Yes --> Pack["Context packing strategies:<br/>• Summarize completed work<br/>• Prune irrelevant history<br/>• Progressive disclosure<br/>(load on demand)<br/>• MCP integrations for<br/>external data"]
    TooLarge -- "No — fits within limits" --> Trust

    Pack --> Trust["Assign trust levels:<br/>• Rules files = high trust<br/>• Specs = high trust<br/>• Source = ground truth<br/>• Conversation = low trust"]
    Trust --> Ready([Context ready:<br/>agent can work effectively])

    style Ready fill:#9f9,stroke:#060,stroke-width:2px
```

---

## Skill

### context-engineering (Utility, Cross-Cutting)

| Field | Value |
|-------|-------|
| Type | Utility |
| Path | `skills/meta/context-engineering/` |

Optimizes agent context setup by curating what the agent sees deliberately. The context hierarchy (in priority order):
1. **Rules files** — `AGENTS.md`, project standards, coding conventions (highest trust)
2. **Specs & requirements** — SRS, user stories, relevant documentation
3. **Source files** — code relevant to the current task (ground truth)
4. **Error output** — when debugging, the actual error output
5. **Conversation history** — minimal, relevant only (lowest trust)

Context packing strategies: summarize completed work, prune irrelevant history, progressive disclosure (load references on demand), and MCP integrations for external data. Confusion management: when the agent is confused or output degrades, reduce context, reload from source, and restate the goal.

**When to use:** Starting a new session, when agent output quality degrades, when switching between tasks, or when you need to configure rules files and context for a project. Cross-cutting — applies to all SDLC phases.

---

## How Meta Skills Relate to the SDLC

```mermaid
flowchart LR
    META["Meta: context-engineering<br/>(cross-cutting, all phases)"]

    META -.->|"configures context for"| Analysis
    META -.->|"configures context for"| Design
    META -.->|"configures context for"| Development
    META -.->|"configures context for"| Testing
    META -.->|"configures context for"| Deployment

    subgraph SDLC
        Analysis[Analysis] --> Design[Design] --> Development[Development] --> Testing[Testing] --> Deployment[Deployment]
    end
```

Context engineering is invoked at the **start of any session** or whenever output quality degrades during **any phase**. It is not part of the linear SDLC pipeline — it wraps around it, ensuring the agent always has the right information loaded for the task at hand.
