# Success Criterion

> **Slug:** `success-criterion` | **Layer:** L4 Investment Decision & Viability | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a measurable pass/fail criterion — with baseline, target, method, and when measured — that confirms an objective was met.
- **Purpose / when used:** defines what counts as success for an objective; distinct from the ongoing KPI.

## 2. Semantics (crisp)

`success-criterion` is a **one-off, measurable pass/fail condition** for an [Objective](objective.md): a measure, a baseline, a target, a measurement method, and when measured (e.g. go-live, 3 months, 12 months). It is **not** the objective (the goal — → [Objective](objective.md)) and **not** the ongoing indicator (→ [KPI](kpi.md)). For Brown Field / Modernization it includes migration success criteria (zero data loss, feature parity ≥95%, zero-downtime cutover).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| measure | string | yes | what is measured |
| baseline | string | yes | current value |
| target | string | yes | target value |
| method | string | yes | measurement method |
| whenMeasured | string | yes | when success is checked |

## 4. State (as-is / target)

Stateless — a pass/fail condition.

## 5. Relationships (semantic references)

- **Refers to:** [Objective](objective.md), [KPI](kpi.md).
- **Referred by:** [KPI](kpi.md), [Objective](objective.md).

## 6. Lifecycle / status

N/A — condition; verified at the measurement point.

## 7. Template coverage

- `templates/analysis/business-case.md` §4.2 Success Criteria
- `templates/analysis/project-plan.md` §3.2 Project Success Criteria

## 8. Non-overlap note

The goal belongs to [Objective](objective.md); the ongoing indicator belongs to [KPI](kpi.md).
