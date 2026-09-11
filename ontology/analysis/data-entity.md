# Data Entity

> **Slug:** `data-entity` | **Layer:** L3 Requirements | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a core data entity with attributes, relationships, ownership (source of truth), lifecycle, retention, and migration status.
- **Purpose / when used:** the atomic unit of the data model; referenced by requirements, interfaces, and the data-migration plan.

## 2. Semantics (crisp)

`data-entity` is a **data-model atom** — an entity with attributes, primary key, relationships, source of truth, lifecycle (create/update/archive/delete), retention policy, and (for migration) a change type and volume/growth. It is **not** an interface payload (→ [Interface](interface.md)), **not** a requirement (→ [Requirement](requirement.md)), and **not** the migration mechanics (→ [Data Migration](data-migration.md)). Data-protection/retention obligations imposed by regulation live as [Compliance Requirement](compliance-requirement.md) references.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| name | string | yes | |
| attributes | table | yes | name, type, length, mandatory, default, validation |
| primaryKey | string | yes | |
| relationships | table | yes | FK + referential integrity |
| sourceOfTruth | string | yes | owning system |
| lifecycle | table | yes | create / update / archive / delete rules |
| retention | string | no | retention period, compliance driver |
| changeType | enum (new / modified / preserved / retired) | no | 🟤🔵 |
| volumeGrowth | table | no | initial / daily / 1y / 3y / 5y |

## 4. State (as-is / target)

Stateful. As-is entities (current schema) vs target entities. Attribute-level change type for Brown Field / Modernization.

## 5. Relationships (semantic references)

- **Refers to:** [Requirement](requirement.md), [Interface](interface.md), [Compliance Requirement](compliance-requirement.md), [Data Migration](data-migration.md).
- **Referred by:** [Compliance Requirement](compliance-requirement.md), [Current System](current-system.md), [Data Migration](data-migration.md), [Interface](interface.md), [Requirement](requirement.md), rollout [Seed Data Setup](../rollout/seed-data-setup.md) (conformsTo).

## 6. Lifecycle / status

N/A — structural artefact; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/software-requirements-specification.md` §7 Data Requirements (incl. §7.4 lifecycle, §7.5 reference data)
- `templates/analysis/project-scope.md` §8.1 Data Entities & Models, §8.3 Data Retention & Archival, §8.4 Data Security & Privacy
- `templates/analysis/software-requirements-specification.md` Appendix C (Data Model & Schema)

## 8. Non-overlap note

Migration mechanics belong to [Data Migration](data-migration.md); interface payloads belong to [Interface](interface.md); regulatory obligations on data belong to [Compliance Requirement](compliance-requirement.md).
