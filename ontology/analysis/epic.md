# Epic

> **Slug:** `epic` | **Layer:** L3 Requirements | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a body of work spanning multiple sprints that groups related user stories delivering a cohesive capability.
- **Purpose / when used:** groups user stories aligned with a capability; the planning unit above the story.

## 2. Semantics (crisp)

`epic` **groups** related [User Story](user-story.md) artefacts that together deliver a [Capability](capability.md). It carries business value, MoSCoW priority, story count, risk/complexity, dependencies on other epics, and (for Brown Field / Modernization) a parity-epic indicator and the legacy feature it replaces. It is **not** the capability itself (→ [Capability](capability.md)), **not** a story (→ [User Story](user-story.md)), and **not** a phase (→ [Phase](phase.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. EP-01 |
| name | string | yes | |
| description | string | yes | |
| businessValue | string | yes | |
| MoSCoW | enum (Must / Should / Could) | yes | |
| storyCount | int | yes | |
| parityEpic | bool | no | 🟤🔵 — replaces a legacy feature |
| realizes | ref → [Capability](capability.md) | yes | |
| srsTrace | ref[] → [Requirement](requirement.md) | yes | |

## 4. State (as-is / target)

Journey — delivered incrementally across sprints.

## 5. Relationships (semantic references)

- **Refers to:** [Capability](capability.md), [User Story](user-story.md), [Requirement](requirement.md).
- **Referred by:** [Release](release.md), [User Story](user-story.md).

## 6. Lifecycle / status

N/A — planning artefact; status follows backlog workflow.

## 7. Template coverage

- `templates/analysis/user-stories.md` §3 Epics (incl. §3.1 registry, §3.2 details)
- `templates/analysis/project-scope.md` §5.2 User Stories / Epics

## 8. Non-overlap note

The capability delivered belongs to [Capability](capability.md); the individual increments belong to [User Story](user-story.md).
