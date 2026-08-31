# Legacy Decommission

> **Slug:** `legacy-decommission` | **Layer:** L5 Scope & Planning | **Applicability:** 🔵🟤

## 1. Identity & definition

- **Definition (one sentence):** the retirement of the legacy system — prerequisites, decommission phases (announcement/soft/hard), archival, contract termination, savings, and sign-off.
- **Purpose / when used:** the end-of-life of the as-is system; referenced by the roadmap and transition strategy.

## 2. Semantics (crisp)

`legacy-decommission` is the **retirement** of the [Current System](current-system.md): prerequisites (all users migrated, all data migrated, all integrations switched, no remaining dependencies), decommission phases (announcement, soft decommission, hard decommission), data archival, contract termination/renegotiation with legacy vendors, cost savings (when they start), risks of premature decommission, and sign-off requirements. It is **not** the migration (→ [Data Migration](data-migration.md)) and **not** the cutover (→ [Cutover](cutover.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| prerequisites | string | yes | all migrated, no dependencies |
| decommissionPhases | table[] | yes | announcement / soft / hard |
| archival | string | yes | what is archived, where, how long |
| contractTermination | string | yes | vendor notices, exit clauses |
| costSavings | string | yes | when savings start |
| signOff | string | yes | sign-off requirements |

## 4. State (as-is / target)

Journey — the retirement path.

## 5. Relationships (semantic references)

- **Refers to:** [Current System](current-system.md), [Data Migration](data-migration.md), [Cutover](cutover.md), [Milestone](milestone.md), [Vendor](vendor.md).
- **Referred by:** [Data Migration](data-migration.md), [Roadmap](roadmap.md), [Vendor](vendor.md).

## 6. Lifecycle / status

N/A — plan; status follows decommission phases.

## 7. Template coverage

- `templates/analysis/project-plan.md` §17.4 Legacy Decommission Plan
- `templates/analysis/software-requirements-specification.md` §11.3 Legacy Decommission Requirements
- `templates/analysis/project-scope.md` §9.3 Migration Deliverables (decommission docs)
- `templates/analysis/user-stories.md` §11.4 Legacy Decommission Stories

## 8. Non-overlap note

The data movement belongs to [Data Migration](data-migration.md); the switchover event belongs to [Cutover](cutover.md).
