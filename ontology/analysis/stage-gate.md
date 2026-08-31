# Stage Gate

> **Slug:** `stage-gate` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a phase-level review gate — the phase completed, review criteria, reviewers, possible outcomes, and reporting requirements.
- **Purpose / when used:** the governance checkpoint at a phase end; the review process that occurs at a milestone.

## 2. Semantics (crisp)

`stage-gate` is the **phase-level governance review**: the gate name, the phase completed, the review criteria (scope, quality, budget, schedule, risk), the reviewers, the possible outcomes (proceed / conditional proceed / pivot / halt), and the reporting requirements. It is the *review process* that occurs at a [Milestone](milestone.md) (the milestone is the *when*). It is **not** the work-item pass/fail (→ [Quality Gate](quality-gate.md)), **not** the milestone point (→ [Milestone](milestone.md)), and **not** the recorded decision (→ [Decision](decision.md)) — the gate produces a decision. For Modernization it includes the migration-readiness gate.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| gate | string | yes | gate name |
| phaseCompleted | ref → [Phase](phase.md) | yes | |
| reviewCriteria | string | yes | scope/quality/budget/schedule/risk |
| reviewers | ref[] → [Stakeholder](stakeholder.md) | yes | |
| possibleOutcomes | enum (proceed / conditional / pivot / halt) | yes | |
| reportingRequirements | string | yes | |

## 4. State (as-is / target)

Journey — a checkpoint on the delivery path.

## 5. Relationships (semantic references)

- **Refers to:** [Phase](phase.md), [Milestone](milestone.md), [Governance](governance.md), [Decision](decision.md).
- **Referred by:** [Decision](decision.md), [Milestone](milestone.md).

## 6. Lifecycle / status

N/A — review; outcome recorded as a [Decision](decision.md).

## 7. Template coverage

- `templates/analysis/business-case.md` §15.2 Stage-Gate Reviews
- `templates/analysis/project-plan.md` §5.3 Stage-Gate Reviews
- `templates/analysis/project-scope.md` §4.3 go/no-go gates

## 8. Non-overlap note

Work-item pass/fail belongs to [Quality Gate](quality-gate.md); the point in time belongs to [Milestone](milestone.md); the recorded outcome belongs to [Decision](decision.md).
