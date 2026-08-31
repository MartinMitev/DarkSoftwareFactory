# Transition Strategy

> **Slug:** `transition-strategy` | **Layer:** L5 Scope & Planning | **Applicability:** 🟤🔵

## 1. Identity & definition

- **Definition (one sentence):** the approach to move from as-is to target — big-bang, phased, parallel, geographic, or feature-by-feature — with rollback and data-cutover approaches.
- **Purpose / when used:** defines how the transition is conducted; referenced by the roadmap and the business case.

## 2. Semantics (crisp)

`transition-strategy` is the **transition approach**: the chosen pattern (big-bang cutover, phased rollout, parallel run, geographic rollout, feature-by-feature migration), the rollback strategy (how to revert, maximum rollback window), the data-cutover approach (freeze/migrate/validate/switch), the timeline, and the completion criteria. It is **not** the switchover event (→ [Cutover](cutover.md)), **not** the data movement (→ [Data Migration](data-migration.md)), and **not** the roadmap (→ [Roadmap](roadmap.md)). For Green Field with no migration, mark NOT APPLICABLE.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| approach | enum (big-bang / phased / parallel / geographic / feature-by-feature) | yes | |
| rollbackStrategy | string | yes | |
| dataCutoverApproach | string | yes | freeze/migrate/validate/switch |
| timeline | string | yes | |
| completionCriteria | string | yes | |

## 4. State (as-is / target)

Journey — the transition approach.

## 5. Relationships (semantic references)

- **Refers to:** [Roadmap](roadmap.md), [Cutover](cutover.md), [Data Migration](data-migration.md), [Phase](phase.md).
- **Referred by:** [Cutover](cutover.md), [Roadmap](roadmap.md).

## 6. Lifecycle / status

N/A — strategy; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/business-case.md` §11.4 Transition Strategy
- `templates/analysis/project-plan.md` §17.1 Transition Strategy
- `templates/analysis/project-scope.md` §7.4 Migration Integration Scope

## 8. Non-overlap note

The switchover event belongs to [Cutover](cutover.md); the data movement belongs to [Data Migration](data-migration.md); the master plan belongs to [Roadmap](roadmap.md).
