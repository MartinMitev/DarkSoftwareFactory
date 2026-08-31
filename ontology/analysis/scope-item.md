# Scope Item

> **Slug:** `scope-item` | **Layer:** L5 Scope & Planning | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a unit of scope — in-scope or explicitly out-of-scope — with category, MoSCoW priority, and traces to objective, requirement, deliverable, and work package.
- **Purpose / when used:** the authoritative scope atom; out-of-scope items use `in_scope=false` with a rationale, folding exclusions, adjacent-systems-not-in-scope, and org-changes-not-in-scope into one artefact.

## 2. Semantics (crisp)

`scope-item` is the **authoritative scope unit**. In-scope items carry a category, MoSCoW priority, the objective they trace to, and the delivery phase. **Out-of-scope items are the same artefact with `in_scope=false`** plus an `exclusionRationale` and `deferredTo` — this folds the three exclusion categories (explicit out-of-scope, adjacent systems not in scope, organizational changes not in scope) into a single artefact instead of three. It is **not** the requirement (→ [Requirement](requirement.md)), **not** the deliverable (→ [Deliverable](deliverable.md)), and **not** the work (→ [Work Package](work-package.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| inScope | bool | yes | false = out-of-scope (folds exclusions) |
| category | string | yes | feature area / component / work stream / adjacent-system / org-change |
| MoSCoW | enum (Must / Should / Could / Won't) | yes | |
| tracesToObjective | ref → [Objective](objective.md) | no | for in-scope |
| deliveryPhase | ref → [Phase](phase.md) | no | for in-scope |
| exclusionRationale | string | no | required when inScope=false |
| deferredTo | string | no | future phase/release |

## 4. State (as-is / target)

Stateful. As-is scope (current boundaries) vs target scope. Change type marks new/modified/preserved.

## 5. Relationships (semantic references)

- **Refers to:** [Objective](objective.md), [Requirement](requirement.md), [Deliverable](deliverable.md), [Work Package](work-package.md), [Phase](phase.md).
- **Referred by:** [Change Request](change-request.md), [Deliverable](deliverable.md), [Objective](objective.md), [Phase](phase.md), [Release](release.md), [Requirement](requirement.md), [User Story](user-story.md), [Work Package](work-package.md).

## 6. Lifecycle / status

N/A — scope unit; changes via [Change Request](change-request.md).

## 7. Template coverage

- `templates/analysis/project-scope.md` §4.2 In-Scope Items, §12 Scope Exclusions (§12.1–12.3)
- `templates/analysis/project-plan.md` §4 Project Scope Summary, §4.3 Scope Prioritization
- `templates/analysis/project-scope.md` §10.3 Scope Traceability Matrix

## 8. Non-overlap note

Out-of-scope is folded via `in_scope=false` — no separate exclusion artefact. The requirement belongs to [Requirement](requirement.md); the work belongs to [Work Package](work-package.md).
