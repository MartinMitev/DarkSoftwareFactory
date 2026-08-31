# Governance

> **Slug:** `governance` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the governance bodies, composition, cadence, decision-authority matrix per change type, escalation path, and authority levels.
- **Purpose / when used:** the who-decides-what framework; referenced by decisions, stage-gates, and change requests.

## 2. Semantics (crisp)

`governance` is the **decision-making framework**: governance bodies (steering committee, project board), their composition and meeting cadence, the decision-authority matrix per change type (scope, budget, timeline, architecture, team, vendor, cutover, rollback), the escalation path, and the authority levels (minor / moderate / major). It is **not** a recorded decision (→ [Decision](decision.md)), **not** a phase-gate review (→ [Stage Gate](stage-gate.md)), and **not** a change request (→ [Change Request](change-request.md)). For Brown Field / Modernization it includes cutover/rollback governance.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| body | string | yes | steering committee / project board |
| composition | string | yes | who sits on it |
| cadence | string | yes | meeting frequency |
| decisionAuthorityMatrix | table | yes | change type → authority |
| escalationPath | string | yes | |
| authorityLevels | table | yes | minor / moderate / major |

## 4. State (as-is / target)

Stateless — a framework.

## 5. Relationships (semantic references)

- **Refers to:** [Stakeholder](stakeholder.md), [Role](role.md), [Decision](decision.md), [Change Request](change-request.md).
- **Referred by:** [Change Request](change-request.md), [Communication Plan](communication-plan.md), [Stage Gate](stage-gate.md).

## 6. Lifecycle / status

N/A — framework; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/business-case.md` §13.3 Governance & Decision Rights, §15 Governance & Approval
- `templates/analysis/project-plan.md` §5 Project Organization & Governance
- `templates/analysis/project-scope.md` §14 Scope Change Control (authority levels)
- `templates/analysis/software-requirements-specification.md` §16.1 Requirements Approval (approval authority)

## 8. Non-overlap note

A recorded decision belongs to [Decision](decision.md); a phase-gate review belongs to [Stage Gate](stage-gate.md); a change request belongs to [Change Request](change-request.md). Governance owns the framework.
