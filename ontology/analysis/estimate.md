# Estimate

> **Slug:** `estimate` | **Layer:** L4 Investment Decision & Viability | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the estimation basis, method, and confidence — for effort, cost, velocity, or schedule — at confidence level Rough Order of Magnitude / Budget / Definitive.
- **Purpose / when used:** documents how a figure was derived; referenced by costs, work packages, and user stories.

## 2. Semantics (crisp)

`estimate` is the **basis/method/confidence** behind a figure: methodology (expert judgment, analogous, parametric, bottom-up, Planning Poker, T-shirt sizing), confidence (ROM / Budget / Definitive, or Rough / Budget / Committed), the assumptions, and the reference basis (e.g. the 1-point reference story). It is **not** the figure itself (the cost line → [Cost](cost.md); the work-package effort → [Work Package](work-package.md); the story points → [User Story](user-story.md)). It explains *how* a number was produced.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| type | enum (effort / cost / velocity / schedule) | yes | |
| methodology | string | yes | |
| confidence | enum (ROM / Budget / Definitive / Rough / Committed) | yes | |
| assumptions | string | yes | |
| referenceBasis | string | no | e.g. 1-point reference story |

## 4. State (as-is / target)

Stateless — a basis.

## 5. Relationships (semantic references)

- **Refers to:** [Work Package](work-package.md), [User Story](user-story.md), [Phase](phase.md), [Cost](cost.md).
- **Referred by:** [Work Package](work-package.md).

## 6. Lifecycle / status

N/A — basis; revised as figures are refined.

## 7. Template coverage

- `templates/analysis/viability-study.md` §5.7 Development Effort Estimate
- `templates/analysis/business-case.md` §8.4 Estimation Assumptions & Confidence
- `templates/analysis/user-stories.md` §8 Estimation & Velocity (incl. §8.2 estimation basis)
- `templates/analysis/project-plan.md` §7.4 Sprint Cadence & Capacity, §8.4 Financial Assumptions
- `templates/analysis/project-scope.md` §10 Work Breakdown Structure (effort column)

## 8. Non-overlap note

The cost line belongs to [Cost](cost.md); the work belongs to [Work Package](work-package.md); the story points belong to [User Story](user-story.md). Estimate is the *how*.
