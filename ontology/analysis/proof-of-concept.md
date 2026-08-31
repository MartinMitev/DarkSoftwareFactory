# Proof of Concept

> **Slug:** `proof-of-concept` | **Layer:** L4 Investment Decision & Viability | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a technical experiment or prototype — objective, methodology, scope, results, limitations, and recommendations — that de-risks feasibility.
- **Purpose / when used:** validates a technology or approach before commitment; informs the options analysis and viability.

## 2. Semantics (crisp)

`proof-of-concept` is a **de-risking experiment**: an objective, methodology, scope, results, limitations, and recommendations from the findings. It is **not** a requirement (→ [Requirement](requirement.md)), **not** the final design (that belongs to the design phase), and **not** an option (→ [Option](option.md)) — it *informs* an option by validating a [Technology](technology.md) or approach.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| objective | string | yes | what the PoC validates |
| methodology | string | yes | |
| scope | string | yes | |
| results | string | yes | findings |
| limitations | string | yes | what the PoC does not prove |
| recommendations | string | yes | from findings |

## 4. State (as-is / target)

Stateless — an experiment.

## 5. Relationships (semantic references)

- **Refers to:** [Technology](technology.md), [Option](option.md), [Requirement](requirement.md).
- **Referred by:** none.

## 6. Lifecycle / status

N/A — experiment; documented as an appendix.

## 7. Template coverage

- `templates/analysis/viability-study.md` Appendix C Technical Proof-of-Concept Results
- `templates/analysis/business-case.md` Appendix D Technical Proof-of-Concept Results
- `templates/analysis/viability-study.md` §5.3 Technical Readiness (PoC validation status)

## 8. Non-overlap note

The production design belongs to the design phase; the investment alternative belongs to [Option](option.md); the contract belongs to [Requirement](requirement.md).
