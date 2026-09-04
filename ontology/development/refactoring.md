# Refactoring

> **Slug:** `refactoring` | **View:** Code Quality View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a deliberate restructuring of [Code Unit](code-unit.md)s that improves internal quality without changing external behaviour, motivated by debt or findings and optionally applying a [Design Pattern](../design/design-pattern.md).
- **Purpose / when used:** the improvement activity; resolves [Static Analysis Finding](static-analysis-finding.md)s and pays down analysis [Technical Debt Item](../analysis/technical-debt-item.md)s.

## 2. Semantics (crisp)

`refactoring` is the improvement activity: a scope (the [Code Unit](code-unit.md)s it touches), a motivation (resolve [Static Analysis Finding](static-analysis-finding.md)s / pay down analysis [Technical Debt Item](../analysis/technical-debt-item.md)s / improve a quality attribute), the [Design Pattern](../design/design-pattern.md) introduced/applied, and a status (proposed / in-progress / done). It is delivered as [Code Commit](code-commit.md)s (often via a [Pull Request](pull-request.md)). It is **not** a change request (→ analysis [Change Request](../analysis/change-request.md) — a request may *trigger* a refactoring), **not** a new feature (→ [User Story](../analysis/user-story.md)), **not** the debt itself (→ [Technical Debt Item](../analysis/technical-debt-item.md) — it *resolves* debt), and **not** the design pattern (→ [Design Pattern](../design/design-pattern.md) — it *applies* one).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. RF-001 |
| scope | ref[] → [Code Unit](code-unit.md) | yes | the units touched |
| motivation | string | yes | debt / findings / quality attribute |
| resolvesFindings | ref[] → [Static Analysis Finding](static-analysis-finding.md) | no | |
| paysDownDebt | ref[] → [Technical Debt Item](../analysis/technical-debt-item.md) | no | |
| appliesPattern | ref → [Design Pattern](../design/design-pattern.md) | no | the pattern introduced/applied |
| deliveredAs | ref[] → [Code Commit](code-commit.md) | no | commits implementing the refactoring |
| status | enum (proposed / in-progress / done) | yes | |

## 4. State (as-is / target)

Stateless — an improvement activity; lifecycle proposed → in-progress → done.

## 5. Relationships (semantic references)

- **Refers to:** [Code Unit](code-unit.md) (scope), [Static Analysis Finding](static-analysis-finding.md) (resolves), [Technical Debt Item](../analysis/technical-debt-item.md) (pays down), [Design Pattern](../design/design-pattern.md) (applies), [Code Commit](code-commit.md) (delivered as).
- **Referred by:** [Static Analysis Finding](static-analysis-finding.md) (resolved by).

## 6. Lifecycle / status

proposed → in-progress → done. A refactoring is "done" when its commits are merged (via a [Pull Request](pull-request.md)) and the findings/debt items it targets are closed.

## 7. Template coverage

- A future `templates/development/*.md` refactoring / debt-remediation section.
- Pays down debt tracked in `templates/design/software-architecture.md` §12.2 Technical Debts and `templates/analysis/viability-study.md` §3.3 Technical Debt Assessment.

## 8. Non-overlap note

The change request belongs to analysis [Change Request](../analysis/change-request.md); the new feature belongs to [User Story](../analysis/user-story.md); the debt belongs to analysis [Technical Debt Item](../analysis/technical-debt-item.md); the design pattern belongs to [Design Pattern](../design/design-pattern.md). The refactoring is the improvement activity that ties them together.
