# Deliverable

> **Slug:** `deliverable` | **Layer:** L5 Scope & Planning | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a tangible product, documentation, or migration deliverable with type, acceptance criteria, delivery phase, and trace to a scope item.
- **Purpose / when used:** what the project produces; referenced by scope items and work packages.

## 2. Semantics (crisp)

`deliverable` is the **produced artefact** — a product deliverable (working software, UI, API), a documentation deliverable (architecture docs, API docs, runbooks), or a migration deliverable (migrated data, validation reports, rollback plan). It carries acceptance criteria, a delivery phase, and a trace to a [Scope Item](scope-item.md). It is **not** the work package (the work — → [Work Package](work-package.md)) and **not** the scope item (the unit of scope — → [Scope Item](scope-item.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| type | enum (product / documentation / migration) | yes | |
| acceptanceCriteria | string | yes | |
| deliveryPhase | ref → [Phase](phase.md) | yes | |
| tracesToScopeItem | ref → [Scope Item](scope-item.md) | yes | |

## 4. State (as-is / target)

Stateful. As-is deliverables (existing artifacts) vs target deliverables.

## 5. Relationships (semantic references)

- **Refers to:** [Scope Item](scope-item.md), [Phase](phase.md), [Acceptance Criterion](acceptance-criterion.md).
- **Referred by:** [Milestone](milestone.md), [Phase](phase.md), [Scope Item](scope-item.md), [Work Package](work-package.md).

## 6. Lifecycle / status

N/A — produced artefact; acceptance verified at delivery.

## 7. Template coverage

- `templates/analysis/project-scope.md` §9 Deliverables (§9.1 product, §9.2 documentation, §9.3 migration)
- `templates/analysis/project-plan.md` §4.2 Major Deliverables

## 8. Non-overlap note

The work decomposition belongs to [Work Package](work-package.md); the unit of scope belongs to [Scope Item](scope-item.md).
