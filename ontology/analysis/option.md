# Option

> **Slug:** `option` | **Layer:** L4 Investment Decision & Viability | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a viable investment alternative — including "Do Nothing" — with key characteristics, criteria scores, and financial and risk profile.
- **Purpose / when used:** the unit of options/alternatives analysis; the recommended option is recorded as a [Decision](decision.md).

## 2. Semantics (crisp)

`option` is **one alternative** in the options/alternatives analysis: a name, description, key characteristics, scores against weighted criteria, a financial profile, and an overall risk rating. It always includes Option 0 "Do Nothing" as the reference baseline. It is **not** the recommendation (→ [Decision](decision.md)), **not** a technology (→ [Technology](technology.md)), and **not** the cost/benefit themselves (→ [Cost](cost.md) / [Benefit](benefit.md)). Green Field options are build/buy/open-source/partner; Brown Field are incremental-refactor/partial-rewrite/wrap-and-extend/replace; Modernization are re-host/re-platform/re-architect/rebuild/replace-COTS.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. Option 0/1/2/3 |
| name | string | yes | |
| description | string | yes | |
| characteristics | string | yes | |
| criteriaScores | table | yes | criterion / weight / score / weighted |
| financialProfile | ref[] → [Cost](cost.md), [Benefit](benefit.md), [Financial Metric](financial-metric.md) | yes | |
| riskRating | enum (Low / Medium / High) | yes | |

## 4. State (as-is / target)

Stateless — an evaluated alternative.

## 5. Relationships (semantic references)

- **Refers to:** [Objective](objective.md), [Cost](cost.md), [Benefit](benefit.md), [Risk](risk.md), [Technology](technology.md), [Financial Metric](financial-metric.md).
- **Referred by:** [Cost](cost.md), [Decision](decision.md), [Financial Metric](financial-metric.md), [Proof of Concept](proof-of-concept.md), [Technology](technology.md).

## 6. Lifecycle / status

N/A — evaluation artefact; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/viability-study.md` §13 Alternatives Analysis (§13.1 identified, §13.2 comparative, §13.3 recommended)
- `templates/analysis/business-case.md` §5 Options Analysis (§5.1–5.4)

## 8. Non-overlap note

The recommendation/selection belongs to [Decision](decision.md); the cost/benefit figures belong to [Cost](cost.md)/[Benefit](benefit.md).
