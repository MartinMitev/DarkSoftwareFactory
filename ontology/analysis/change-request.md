# Change Request

> **Slug:** `change-request` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a request to change scope, requirements, or plan — id, description, impact (budget/schedule/quality/scope), affected items, the decision reference, and the new baseline.
- **Purpose / when used:** the single change-request artefact across scope, SRS, user stories, and project plan.

## 2. Semantics (crisp)

`change-request` is the **request** to change the baselined scope/requirements/plan: a description, the requestor, the impact (budget/schedule/quality/scope), the affected scope items / requirements / work packages, a reference to the [Decision](decision.md) that approves/rejects/defers it, and the new baseline version. It is **not** the recorded decision (→ [Decision](decision.md)) — a change-request *approval* is recorded as a decision — and **not** the governance framework (→ [Governance](governance.md)) that sets the authority. For Brown Field / Modernization it includes parity-impacting changes.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| description | string | yes | |
| requestor | ref → [Stakeholder](stakeholder.md) | yes | |
| impact | table | yes | budget / schedule / quality / scope |
| affectedItems | ref[] → [Scope Item](scope-item.md) / [Requirement](requirement.md) / [Work Package](work-package.md) | yes | |
| decisionRef | ref → [Decision](decision.md) | yes | the approval |
| newBaselineVersion | string | no | |

## 4. State (as-is / target)

Stateless — a request.

## 5. Relationships (semantic references)

- **Refers to:** [Scope Item](scope-item.md), [Requirement](requirement.md), [Work Package](work-package.md), [Decision](decision.md), [Governance](governance.md).
- **Referred by:** [Decision](decision.md), [Governance](governance.md).

## 6. Lifecycle / status

Status: submitted → under-review → approved / rejected / deferred. The approval is a [Decision](decision.md).

## 7. Template coverage

- `templates/analysis/project-scope.md` §14 Scope Change Control (§14.1 process, §14.3 log)
- `templates/analysis/software-requirements-specification.md` §15 Requirement Change Control (§15.1, §15.3 log)
- `templates/analysis/project-plan.md` §14 Scope Change Control (§14.3 log)
- `templates/analysis/user-stories.md` §12 Story Change Control (§12.2, §12.3 log)

## 8. Non-overlap note

The recorded approval belongs to [Decision](decision.md); the authority framework belongs to [Governance](governance.md). Change Request owns the request.
