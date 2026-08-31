# Market & Demand

> **Slug:** `market-and-demand` | **Layer:** L2 Business Architecture | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the external market and demand analysis — target users/market, competitive and alternative landscape, and demand-validation evidence.
- **Purpose / when used:** establishes that demand exists for the proposed value proposition; informs viability and the options analysis.

## 2. Semantics (crisp)

`market-and-demand` captures the target users/personas (incl. TAM/SAM/SOM for external products), direct and indirect competitors, the "do nothing" baseline, open-source alternatives, and demand evidence (interviews, surveys, waitlists, market reports, support tickets). It is **not** the value proposition (→ [Business Model](business-model.md)) and **not** the internal capability set (→ [Capability](capability.md)). It is the external evidence base.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| targetUsers | string | yes | personas / market segment |
| tamSamSom | string | no | for external products |
| competitors | table[] | yes | direct + indirect |
| alternatives | table[] | yes | incl. do-nothing, open-source |
| demandEvidence | string | yes | interviews/surveys/data |

## 4. State (as-is / target)

Stateless — an external snapshot.

## 5. Relationships (semantic references)

- **Refers to:** [Business Model](business-model.md).
- **Referred by:** [Business Model](business-model.md), [SWOT Item](swot-item.md).

## 6. Lifecycle / status

N/A — external evidence; refreshed as new data arrives.

## 7. Template coverage

- `templates/analysis/viability-study.md` §4.2 Target Market & Users, §4.3 Competitive & Alternative Landscape, §4.4 Demand Validation
- `templates/analysis/business-case.md` §3.4 Market & Competitive Context
- `templates/analysis/viability-study.md` Appendix B (Market Research Data)

## 8. Non-overlap note

Value proposition and value capture belong to [Business Model](business-model.md). Market & Demand only carries the external evidence.
