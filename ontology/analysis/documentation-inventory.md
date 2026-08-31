# Documentation Inventory

> **Slug:** `documentation-inventory` | **Layer:** L1 Intake & Understanding | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a catalog of all source material available before analysis begins, with type, relevance, and trust level per source.
- **Purpose / when used:** produced in Stage 1 of the analysis phase to guarantee the agent has the right inputs before any analysis; it is an inventory of sources, **not** analysis output.

## 2. Semantics (crisp)

`documentation-inventory` is an **input register**: each entry is a source document (brief, spec, RFC, code, market analysis, meeting notes) tagged by relevance and trust. It is **not** understanding of the project (→ [Project Understanding](project-understanding.md)) and **not** a gap (→ [Gap & Contradiction](gap-and-contradiction.md)) — it merely states what material exists and how authoritative it is.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| source | string | yes | document name / URL / file |
| type | enum (brief / spec / RFC / code / market-analysis / meeting-notes / other) | yes | |
| relevance | enum (high / medium / low) | yes | to this engagement |
| trust | enum (authoritative / draft / unofficial / external-unverified) | yes | |
| location | string | no | where it lives |

## 4. State (as-is / target)

Stateless — a snapshot of available sources at intake.

## 5. Relationships (semantic references)

- **Refers to:** [Project](project.md).
- **Referred by:** [Gap & Contradiction](gap-and-contradiction.md), [Project Understanding](project-understanding.md).

## 6. Lifecycle / status

N/A — inventory snapshot. Entries may be added as new sources surface.

## 7. Template coverage

- No template (analysis-phase only). Produced by `skills/analysis/execute-analysis-phase/SKILL.md` Stage 1: Documentation Check & Intake.

## 8. Non-overlap note

Lists **sources only**. The understanding derived from them lives in [Project Understanding](project-understanding.md); the missing/conflicting content lives in [Gap & Contradiction](gap-and-contradiction.md).
