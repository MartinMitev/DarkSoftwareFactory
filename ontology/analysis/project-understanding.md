# Project Understanding

> **Slug:** `project-understanding` | **Layer:** L1 Intake & Understanding | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the synthesized, user-confirmed statement of the project concept, key stakeholders, scope boundaries, and project-type classification derived from the documentation inventory.
- **Purpose / when used:** produced in Stage 2 of the analysis phase; the confirmed baseline understanding against which later stages refine and resolve gaps.

## 2. Semantics (crisp)

`project-understanding` is the **confirmed understanding** of what the project is about — one-paragraph concept, key stakeholders and their implied interests, project-type classification, and initial scope boundaries. It is **not** a source list (→ [Documentation Inventory](documentation-inventory.md)), **not** a gap register (→ [Gap & Contradiction](gap-and-contradiction.md)), and **not** the stress-tested concept (→ [Refined Project Concept](refined-project-concept.md)). It must be presented to the user and explicitly confirmed (Quality Gate 2).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| summary | string | yes | one-paragraph concept statement |
| keyStakeholders | ref[] → [Stakeholder](stakeholder.md) | yes | implied interests |
| scopeBoundaries | string | yes | initial in/out of scope |
| typeClassification | enum (🟢 / 🟤 / 🔵) | yes | mirrors [Project](project.md).type |
| documentLandscape | string | yes | well / partially / undocumented aspects |

## 4. State (as-is / target)

Stateless — a synthesis at a point in time.

## 5. Relationships (semantic references)

- **Refers to:** [Documentation Inventory](documentation-inventory.md), [Project](project.md), [Stakeholder](stakeholder.md).
- **Referred by:** [Gap & Contradiction](gap-and-contradiction.md), [Refined Project Concept](refined-project-concept.md).

## 6. Lifecycle / status

N/A — a confirmed statement; updated when backtracking occurs (per the execute-analysis-phase skill).

## 7. Template coverage

- No template (analysis-phase only). Produced by `skills/analysis/execute-analysis-phase/SKILL.md` Stage 2: Deep Documentation Analysis.

## 8. Non-overlap note

States **understanding**. Gaps and contradictions belong in [Gap & Contradiction](gap-and-contradiction.md); the stress-tested refinement belongs in [Refined Project Concept](refined-project-concept.md).
