# KPI

> **Slug:** `kpi` | **Layer:** L4 Investment Decision & Viability | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** an ongoing tracked indicator — leading or lagging — with a target, data source, frequency, and RAG thresholds, linked to an objective.
- **Purpose / when used:** monitors project health and value delivery over time; distinct from the one-off success criterion.

## 2. Semantics (crisp)

`kpi` is an **ongoing monitoring indicator** (leading predicts future performance; lagging confirms achieved outcomes) with a target, data source, measurement frequency, and green/amber/red thresholds, linked to an [Objective](objective.md) and a [Success Criterion](success-criterion.md). It is **not** the one-off pass/fail (→ [Success Criterion](success-criterion.md)), **not** the objective (→ [Objective](objective.md)), and **not** a benefit (a value delivered — → [Benefit](benefit.md)). KPIs are tracked post-implementation by [Post-Implementation Review](post-implementation-review.md).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| name | string | yes | |
| type | enum (leading / lagging) | yes | |
| target | string | yes | |
| dataSource | string | yes | |
| frequency | string | yes | measurement frequency |
| ragThresholds | string | yes | green / amber / red |
| relatedObjective | ref → [Objective](objective.md) | yes | |

## 4. State (as-is / target)

Stateless — an indicator.

## 5. Relationships (semantic references)

- **Refers to:** [Objective](objective.md), [Success Criterion](success-criterion.md).
- **Referred by:** [Objective](objective.md), [Post-Implementation Review](post-implementation-review.md), [Success Criterion](success-criterion.md).

## 6. Lifecycle / status

N/A — indicator; tracked over time.

## 7. Template coverage

- `templates/analysis/business-case.md` §4.3 Key Performance Indicators
- `templates/analysis/project-plan.md` §3.3 Key Performance Indicators
- `templates/analysis/business-case.md` §16.1 Benefit Realization Tracking (KPI tracking)

## 8. Non-overlap note

The one-off pass/fail belongs to [Success Criterion](success-criterion.md); the goal belongs to [Objective](objective.md); the value delivered belongs to [Benefit](benefit.md).
