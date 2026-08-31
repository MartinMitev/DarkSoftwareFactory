# Objective

> **Slug:** `objective` | **Layer:** L4 Investment Decision & Viability | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a SMART business or project goal — primary or secondary, with a timeframe, priority, and trace to strategy.
- **Purpose / when used:** the goal the project must achieve; traces to the business model and to scope items, requirements, success criteria, and KPIs.

## 2. Semantics (crisp)

`objective` is a **goal** stated in SMART form (Specific, Measurable, Achievable, Relevant, Time-bound), distinguished as primary or secondary, with a timeframe and a link to the strategic objective it supports. It is **not** the measure of success (→ [Success Criterion](success-criterion.md)), **not** the ongoing indicator (→ [KPI](kpi.md)), and **not** a requirement (→ [Requirement](requirement.md)). Objectives trace to the [Business Model](business-model.md) and are realised by scope items and requirements.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| statement | string | yes | the goal |
| smartMeasure | string | yes | the measurable part |
| timeframe | string | yes | short / medium / long |
| priority | enum (primary / secondary) | yes | |
| linkedStrategy | string | yes | strategic objective |

## 4. State (as-is / target)

Stateless — a goal.

## 5. Relationships (semantic references)

- **Refers to:** [Business Model](business-model.md), [Scope Item](scope-item.md), [Requirement](requirement.md), [Success Criterion](success-criterion.md), [KPI](kpi.md).
- **Referred by:** [Benefit](benefit.md), [Business Model](business-model.md), [KPI](kpi.md), [Option](option.md), [Post-Implementation Review](post-implementation-review.md), [Requirement](requirement.md), [Scope Item](scope-item.md), [Success Criterion](success-criterion.md).

## 6. Lifecycle / status

N/A — goal; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/business-case.md` §4.1 Business Objectives
- `templates/analysis/project-scope.md` §3.2 Project Objectives
- `templates/analysis/project-plan.md` §3.1 Business Objectives

## 8. Non-overlap note

The one-off pass/fail measure belongs to [Success Criterion](success-criterion.md); the ongoing indicator belongs to [KPI](kpi.md).
