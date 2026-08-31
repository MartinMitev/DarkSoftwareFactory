# Benefit

> **Slug:** `benefit` | **Layer:** L4 Investment Decision & Viability | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a tangible, intangible, or dis-benefit with annual value, confidence, assumption, and a realisation timeline triggered by a milestone.
- **Purpose / when used:** the atomic value-delivery unit feeding the financial analysis and post-implementation tracking.

## 2. Semantics (crisp)

`benefit` is a **single value-delivery item**: tangible (quantified annual value), intangible (qualitative High/Medium/Low), or **dis-benefit** (a negative consequence modelled as a benefit with negative value). It carries a confidence level, the assumption underlying the estimate, a realisation timeline, and the milestone that triggers it. It is **not** a KPI (an ongoing indicator — → [KPI](kpi.md)), **not** a success criterion (→ [Success Criterion](success-criterion.md)), and **not** a cost-avoided (modelled as negative [Cost](cost.md)). Legacy-retired savings are benefits; dual-running costs are negative benefits or costs depending on framing (here: cost).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| type | enum (tangible / intangible / dis-benefit) | yes | |
| annualValue | number | yes | negative for dis-benefits |
| confidence | enum (Low / Medium / High) | yes | |
| assumption | string | yes | |
| realizationTimeline | table | yes | year-by-year and cumulative |
| triggerMilestone | ref → [Milestone](milestone.md) | yes | |

## 4. State (as-is / target)

Stateless — a value item.

## 5. Relationships (semantic references)

- **Refers to:** [Objective](objective.md), [Cost](cost.md), [Milestone](milestone.md).
- **Referred by:** [Cost](cost.md), [Financial Metric](financial-metric.md), [Option](option.md), [Post-Implementation Review](post-implementation-review.md), [SWOT Item](swot-item.md).

## 6. Lifecycle / status

N/A — value item; tracked by [Post-Implementation Review](post-implementation-review.md).

## 7. Template coverage

- `templates/analysis/viability-study.md` §7.2 Revenue / Benefit Model
- `templates/analysis/business-case.md` §7 Benefits & Value Proposition (incl. §7.1 tangible, §7.2 intangible, §7.3 timeline, §7.4 dis-benefits)
- `templates/analysis/business-case.md` §16.1 Benefit Realization Tracking

## 8. Non-overlap note

The ongoing indicator belongs to [KPI](kpi.md); the cost-avoided is a negative [Cost](cost.md); the one-off pass/fail belongs to [Success Criterion](success-criterion.md).
