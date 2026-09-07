# Milestone

> **Slug:** `milestone` | **Layer:** L5 Scope & Planning | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a point-in-time gate with a target date, the gate decision, success criteria, and the decision maker.
- **Purpose / when used:** a checkpoint in time; references the stage-gate review that occurs at it; triggers benefit realisation.

## 2. Semantics (crisp)

`milestone` is a **point-in-time checkpoint** with a target date, the phase it belongs to, the gate decision associated with it, success criteria, and the decision maker. It references the [Stage Gate](stage-gate.md) review that occurs at it (the milestone is the *when*, the stage-gate is the *review process*). It is **not** the gate definition (→ [Stage Gate](stage-gate.md)), **not** a phase (→ [Phase](phase.md)), and **not** a release (→ [Release](release.md)). For Modernization, migration cutover and legacy-decommission milestones carry specific rollback/sign-off criteria.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. M1 |
| name | string | yes | |
| targetDate | date | yes | |
| predecessorMilestones | ref[] → [Milestone](milestone.md) | no | milestones that must be reached first (critical path) |
| phase | ref → [Phase](phase.md) | yes | |
| gateDecision | ref → [Stage Gate](stage-gate.md) | yes | |
| successCriteria | string | yes | |
| decisionMaker | ref → [Stakeholder](stakeholder.md) | yes | |

## 4. State (as-is / target)

Journey — a checkpoint on the as-is→target path.

## 5. Relationships (semantic references)

- **Refers to:** [Phase](phase.md), [Decision](decision.md), [Stage Gate](stage-gate.md), [Deliverable](deliverable.md), [Stakeholder](stakeholder.md), [Milestone](milestone.md) (predecessorMilestones).
- **Referred by:** [Benefit](benefit.md), [Cutover](cutover.md), [Decision](decision.md), [Legacy Decommission](legacy-decommission.md), [Milestone](milestone.md) (predecessorMilestones), [Phase](phase.md), [Post-Implementation Review](post-implementation-review.md), [Release](release.md), [Roadmap](roadmap.md), [Stage Gate](stage-gate.md).

## 6. Lifecycle / status

N/A — checkpoint; status: planned / reached / missed.

## 7. Template coverage

- `templates/analysis/business-case.md` §11.2 Key Milestones
- `templates/analysis/project-plan.md` §7.2 Key Milestones
- `templates/analysis/user-stories.md` §2.2 release targets (milestone dates)

## 8. Non-overlap note

The review process belongs to [Stage Gate](stage-gate.md); the phase span belongs to [Phase](phase.md); the deployment event belongs to [Release](release.md).
