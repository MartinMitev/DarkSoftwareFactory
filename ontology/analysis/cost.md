# Cost

> **Slug:** `cost` | **Layer:** L4 Investment Decision & Viability | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a cost line item — CapEx, OpEx, or TCO — with amount, confidence, phase, and contingency.
- **Purpose / when used:** the atomic cost figure feeding the financial analysis; referenced by options and financial metrics.

## 2. Semantics (crisp)

`cost` is a **single cost line item** (CapEx one-time, OpEx recurring, TCO combined) with an amount, a confidence level, the phase it belongs to, and a contingency allocation. It is **not** the estimation basis/method (→ [Estimate](estimate.md)) and **not** the computed investment metric (→ [Financial Metric](financial-metric.md)). Cost-avoided (e.g. legacy retired) is modelled as a *negative* cost. Dual-running costs and migration tooling are cost items for Modernization.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| category | enum (capex / opex / tco) | yes | |
| item | string | yes | what the cost is for |
| amount | number | yes | |
| confidence | enum (Low / Medium / High) | yes | |
| phase | ref → [Phase](phase.md) | yes | |
| contingency | string | no | % and rationale |

## 4. State (as-is / target)

Stateless — a cost figure.

## 5. Relationships (semantic references)

- **Refers to:** [Option](option.md), [Phase](phase.md), [Benefit](benefit.md).
- **Referred by:** [Benefit](benefit.md), [Estimate](estimate.md), [Financial Metric](financial-metric.md), [Option](option.md), [Vendor](vendor.md).

## 6. Lifecycle / status

N/A — figure; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/viability-study.md` §7.1 Cost Estimate (TCO)
- `templates/analysis/business-case.md` §8 Cost Estimate (§8.1 CapEx, §8.2 OpEx, §8.3 TCO)
- `templates/analysis/project-plan.md` §8 Budget & Cost Management

## 8. Non-overlap note

The estimation basis/method belongs to [Estimate](estimate.md); the computed NPV/IRR belongs to [Financial Metric](financial-metric.md).
