# Financial Metric

> **Slug:** `financial-metric` | **Layer:** L4 Investment Decision & Viability | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a computed investment metric — NPV, IRR, payback, BCR, or a sensitivity scenario — with value, threshold, and pass/fail.
- **Purpose / when used:** the derived financial figure computed from costs and benefits; the decision input for the investment recommendation.

## 2. Semantics (crisp)

`financial-metric` is a **computed figure** derived from [Cost](cost.md) and [Benefit](benefit.md): NPV (with discount rate and rationale), IRR, payback (simple and discounted), BCR, or a sensitivity scenario (best/expected/worst, cost +20%, benefits delayed, etc.) with a break-even analysis. It is **not** the raw cost (→ [Cost](cost.md)) or benefit (→ [Benefit](benefit.md)) and **not** the recommendation (→ [Decision](decision.md)). It supplies the financial summary verdict (pass/conditional/fail against thresholds).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| metric | enum (npv / irr / payback / bcr / sensitivity / break-even) | yes | |
| scenario | enum (best / expected / worst / cost+20% / benefits-delayed / discount+3%) | no | for sensitivity |
| value | number | yes | |
| threshold | string | yes | pass threshold |
| pass | bool | yes | |
| discountRate | string | no | for NPV |

## 4. State (as-is / target)

Stateless — a computed figure.

## 5. Relationships (semantic references)

- **Refers to:** [Cost](cost.md), [Benefit](benefit.md), [Option](option.md).
- **Referred by:** [Option](option.md).

## 6. Lifecycle / status

N/A — computed figure; recomputed on cost/benefit changes.

## 7. Template coverage

- `templates/analysis/viability-study.md` §7.3 Return on Investment (NPV/IRR/BCR/sensitivity)
- `templates/analysis/business-case.md` §9 Financial Analysis (§9.1–9.7 incl. NPV, IRR, payback, BCR, sensitivity, financial summary)
- `templates/analysis/viability-study.md` Appendix A, `templates/analysis/business-case.md` Appendix A (Detailed Financial Model)

## 8. Non-overlap note

The inputs belong to [Cost](cost.md) and [Benefit](benefit.md); the recommendation belongs to [Decision](decision.md).
