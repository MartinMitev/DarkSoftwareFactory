# Phase

> **Slug:** `phase` | **Layer:** L5 Scope & Planning | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a delivery phase — a time span with start/end, key deliverables, a go/no-go gate, and dependencies on preceding phases.
- **Purpose / when used:** the temporal container of work; ordered in the roadmap; Modernization includes transition and legacy-decommission phases.

## 2. Semantics (crisp)

`phase` is a **time span of work** (e.g. Discovery, Sprint 0/Inception, Build, Test, Transition/Cutover, Legacy Decommission, Hypercare) with start/end dates, key deliverables, a go/no-go gate between phases, and dependencies. It is **not** a point-in-time gate (→ [Milestone](milestone.md)), **not** a deployment event (→ [Release](release.md)), and **not** the stage-gate review (→ [Stage Gate](stage-gate.md)). Phases are ordered in the [Roadmap](roadmap.md).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| name | string | yes | |
| description | string | yes | |
| start | date | yes | |
| end | date | yes | |
| keyDeliverables | ref[] → [Deliverable](deliverable.md) | yes | |
| goNoGoGate | ref → [Milestone](milestone.md) | yes | gate at phase end |
| dependencies | ref[] → [Phase](phase.md) | no | predecessor phases |

## 4. State (as-is / target)

Journey — a phase is inherently part of the as-is→target delivery path.

## 5. Relationships (semantic references)

- **Refers to:** [Scope Item](scope-item.md), [Milestone](milestone.md), [Deliverable](deliverable.md), [Phase](phase.md) (predecessor).
- **Referred by:** [Cost](cost.md), [Deliverable](deliverable.md), [Estimate](estimate.md), [Milestone](milestone.md), [Phase](phase.md), [Release](release.md), [Roadmap](roadmap.md), [Scope Item](scope-item.md), [Stage Gate](stage-gate.md), [Transition Strategy](transition-strategy.md).

## 6. Lifecycle / status

N/A — span; status follows phase execution (not started / in progress / complete).

## 7. Template coverage

- `templates/analysis/business-case.md` §11.1 Delivery Phases
- `templates/analysis/project-scope.md` §4.3 Scope by Phase
- `templates/analysis/project-plan.md` §7.1 Delivery Phases
- `templates/analysis/business-case.md` §11.2 Key Milestones (phase gates)

## 8. Non-overlap note

The point-in-time gate belongs to [Milestone](milestone.md); the deployment event belongs to [Release](release.md); the review belongs to [Stage Gate](stage-gate.md).
