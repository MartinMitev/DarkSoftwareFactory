# Cutover

> **Slug:** `cutover` | **Layer:** L5 Scope & Planning | **Applicability:** 🟤🔵

## 1. Identity & definition

- **Definition (one sentence):** the switchover event with a timed runbook, rollback triggers, and cutover team roles.
- **Purpose / when used:** the actual execution of the switch from legacy to new system; the operational detail of the transition.

## 2. Semantics (crisp)

`cutover` is the **switchover event**: a step-by-step runbook with exact timings (T-2h, T0, T+15min, …), the responsible party per step, verification steps, rollback triggers, the rollback window, and the cutover team roles. It is **not** the transition strategy (→ [Transition Strategy](transition-strategy.md)) and **not** the data movement (→ [Data Migration](data-migration.md)). For Green Field, mark NOT APPLICABLE.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| runbookSteps | table[] | yes | time / activity / responsible / verification / rollbackTrigger |
| rollbackWindow | string | yes | maximum rollback window |
| teamRoles | ref[] → [Role](role.md) | yes | cutover team |

## 4. State (as-is / target)

Journey — the switchover event.

## 5. Relationships (semantic references)

- **Refers to:** [Transition Strategy](transition-strategy.md), [Data Migration](data-migration.md), [Milestone](milestone.md), [Decision](decision.md) (go/no-go, rollback), [Role](role.md).
- **Referred by:** [Data Migration](data-migration.md), [Decision](decision.md), [Legacy Decommission](legacy-decommission.md), [Quality Gate](quality-gate.md), [Roadmap](roadmap.md), [Transition Strategy](transition-strategy.md), rollout [Deployment Runbook](../rollout/deployment-runbook.md) (cutoverRef).

## 6. Lifecycle / status

N/A — event; status: planned / executed / rolled-back.

## 7. Template coverage

- `templates/analysis/project-plan.md` §17.5 Cutover Runbook
- `templates/analysis/project-plan.md` §18 Deployment & Release Strategy (cutover aspects)

## 8. Non-overlap note

The transition approach belongs to [Transition Strategy](transition-strategy.md); the data movement belongs to [Data Migration](data-migration.md).
