# Data Migration

> **Slug:** `data-migration` | **Layer:** L5 Scope & Planning | **Applicability:** 🔵🟤

## 1. Identity & definition

- **Definition (one sentence):** the movement of data from as-is to target — sources, approach (big-bang/phased/parallel/trickle), field mapping/transformation, validation/reconciliation, downtime/rollback, and volume.
- **Purpose / when used:** the data-movement mechanics of modernization/enhancement; referenced by the roadmap and transition strategy.

## 2. Semantics (crisp)

`data-migration` is the **data movement mechanics**: data sources (and volumes), the migration approach (big-bang, phased, parallel run, trickle), source-to-target field mapping and transformation rules, data-integrity validation and reconciliation, the downtime window and rollback strategy, and historical-data scope (migrate vs archive). It is **not** the data model (→ [Data Entity](data-entity.md)), **not** the cutover event (→ [Cutover](cutover.md)), and **not** the transition approach (→ [Transition Strategy](transition-strategy.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| sources | table[] | yes | source / volume |
| approach | enum (big-bang / phased / parallel / trickle) | yes | |
| fieldMapping | table[] | yes | source field → target field |
| transformation | string | yes | type conversions, value mappings |
| validation | string | yes | integrity checks |
| reconciliation | string | yes | completeness/correctness checks |
| downtimeWindow | string | yes | |
| rollback | string | yes | |
| volume | string | yes | |

## 4. State (as-is / target)

Journey — the data movement between as-is and target.

## 5. Relationships (semantic references)

- **Refers to:** [Data Entity](data-entity.md), [Cutover](cutover.md), [Legacy Decommission](legacy-decommission.md), [Interface](interface.md).
- **Referred by:** [Cutover](cutover.md), [Data Entity](data-entity.md), [Dependency](dependency.md), [Legacy Decommission](legacy-decommission.md), [Transition Strategy](transition-strategy.md).

## 6. Lifecycle / status

N/A — plan; status: profiling / cleansing / transformation / migration / validation / reconciliation.

## 7. Template coverage

- `templates/analysis/viability-study.md` §5.4 Data Migration Strategy
- `templates/analysis/project-scope.md` §8.2 Data Migration Scope
- `templates/analysis/software-requirements-specification.md` §7.6 Data Migration Requirements, §11.2 Transition Workflow Requirements
- `templates/analysis/project-plan.md` §17.2 Data Migration Plan
- `templates/analysis/user-stories.md` §11.2 Data Migration Stories

## 8. Non-overlap note

The data structure belongs to [Data Entity](data-entity.md); the switchover event belongs to [Cutover](cutover.md); the transition approach belongs to [Transition Strategy](transition-strategy.md).
