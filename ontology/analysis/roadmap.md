# Roadmap

> **Slug:** `roadmap` | **Layer:** L5 Scope & Planning | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the ordered as-is→target journey — phases, milestones, transition, cutover, and decommission — linking the current-system snapshot to target capability/requirement/application instances.
- **Purpose / when used:** the master transition plan; the optional roadmap between as-is and target that the ontology may define.

## 2. Semantics (crisp)

`roadmap` is the **master transition plan** that orders the journey from as-is to target: a timeline, the ordered [Phase](phase.md) artefacts, the [Milestone](milestone.md) artefacts, and references to both the as-is [Current System](current-system.md) snapshot and the target instances of [Capability](capability.md) / [Requirement](requirement.md) / [Application](application.md) / [Data Entity](data-entity.md). It references the journey artefacts ([Transition Strategy](transition-strategy.md), [Cutover](cutover.md), [Legacy Decommission](legacy-decommission.md), [Data Migration](data-migration.md)). It is **not** a single phase, **not** the transition approach (→ [Transition Strategy](transition-strategy.md)), and **not** the cutover event (→ [Cutover](cutover.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| timeline | string | yes | overall span |
| phases | ref[] → [Phase](phase.md) | yes | ordered |
| milestones | ref[] → [Milestone](milestone.md) | yes | |
| asIsRef | ref → [Current System](current-system.md) | no | 🟤🔵 |
| targetRef | ref[] → [Capability](capability.md) / [Requirement](requirement.md) / [Application](application.md) | yes | target instances |

## 4. State (as-is / target)

Journey — inherently the as-is→target path.

## 5. Relationships (semantic references)

- **Refers to:** [Current System](current-system.md), [Phase](phase.md), [Milestone](milestone.md), [Transition Strategy](transition-strategy.md), [Cutover](cutover.md), [Legacy Decommission](legacy-decommission.md), [Capability](capability.md) (target).
- **Referred by:** [Transition Strategy](transition-strategy.md).

## 6. Lifecycle / status

N/A — master plan; revised as phases complete.

## 7. Template coverage

- `templates/analysis/business-case.md` §11 Implementation Plan
- `templates/analysis/project-plan.md` §7 Schedule & Timeline
- `templates/analysis/project-scope.md` §3.4 Target State Vision

## 8. Non-overlap note

Per-phase detail belongs to [Phase](phase.md); the transition approach belongs to [Transition Strategy](transition-strategy.md); the switchover event belongs to [Cutover](cutover.md).
