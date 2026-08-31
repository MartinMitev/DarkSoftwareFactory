# Design Pattern

> **Slug:** `design-pattern` | **View:** Software Design View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a standardized structural or behavioral solution (e.g. Repository, Factory, Adapter, CQRS, Strategy, Saga) — with problem, solution, consequences, and the [Component](component.md)s it is applied within — applied as a tactical implementation choice.
- **Purpose / when used:** the atomic unit of tactical design choices; documents reusable patterns that give the architecture conceptual integrity and that [Crosscutting Concern](crosscutting-concern.md)s may mandate.

## 2. Semantics (crisp)

`design-pattern` is a **reusable design solution** applied within one or more [Component](component.md)s: a name, a category (creational / structural / behavioral / architectural), the problem it solves, the solution structure, the consequences (trade-offs), and related patterns. It is a tactical/structural choice at the component level — e.g. Repository, Factory, Adapter, Strategy, CQRS, Event Sourcing, Saga, BFF, Sidecar. It is **not** a system-wide policy (→ [Crosscutting Concern](crosscutting-concern.md) — a concern may *mandate* a pattern, but the pattern is the tactical solution), **not** the component itself (→ [Component](component.md)), **not** an architecture decision (→ [Decision](../analysis/decision.md) — a decision may *select* a pattern), and **not** the technology (→ [Technology](../analysis/technology.md)). Selection of a pattern as architecturally significant is recorded as an ADR (analysis [Decision](../analysis/decision.md), type=architecture).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. DP-001 |
| name | string | yes | e.g. Repository, CQRS |
| category | enum (creational / structural / behavioral / architectural) | yes | |
| problem | string | yes | what it solves |
| solution | string | yes | structure / how it works |
| consequences | string | yes | trade-offs |
| appliedIn | ref[] → [Component](component.md) | yes | where it is applied |
| mandatedBy | ref[] → [Crosscutting Concern](crosscutting-concern.md) | no | when a concern mandates this pattern |
| relatedPatterns | string | no | |
| justifiedBy | ref → [Decision](../analysis/decision.md) | no | ADR selecting this pattern |

## 4. State (as-is / target)

Stateful. As-is patterns (existing tactical choices, 🟤🔵) vs target patterns. Change type marks new/modified/preserved/retired.

## 5. Relationships (semantic references)

- **Refers to:** [Component](component.md), [Crosscutting Concern](crosscutting-concern.md), [Decision](../analysis/decision.md) (justified by).
- **Referred by:** [Component](component.md), [Crosscutting Concern](crosscutting-concern.md), [Quality Scenario](quality-scenario.md), [Decision](../analysis/decision.md).

## 6. Lifecycle / status

N/A — structural choice; status follows hosting document approval.

## 7. Template coverage

- `templates/design/software-architecture.md` §9 Cross-cutting Concepts (patterns applied across building blocks, e.g. data-access patterns, integration patterns, DDD patterns)
- `templates/design/software-architecture.md` §6 Building Block View (patterns within whitebox descriptions)

## 8. Non-overlap note

A system-wide policy belongs to [Crosscutting Concern](crosscutting-concern.md); the building block belongs to [Component](component.md); the recorded selection belongs to [Decision](../analysis/decision.md); the technology choice belongs to [Technology](../analysis/technology.md).
