# Seed Data Setup

> **Slug:** `seed-data-setup` | **View:** Data Setup View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the initial / master / reference data loaded into a fresh [Environment](../design/environment.md) before go-live — admin accounts, lookup tables, default configurations, reference data — conforming to analysis [Data Entity](../analysis/data-entity.md) schemas.
- **Purpose / when used:** the one-time initial data for a new deployment; distinct from bulk legacy data movement and from synthetic test data.

## 2. Semantics (crisp)

`seed-data-setup` is the **initial data** for a new deployment: default admin / tenant accounts, reference / lookup data (country codes, currency codes, tax rates), default configuration records, and master data. It conforms to analysis [Data Entity](../analysis/data-entity.md) schemas and is loaded into a design [Environment](../design/environment.md) via a dev [Code Unit](../development/code-unit.md) load script. It is the rollout counterpart of the testing [Test Data Set](../testing/test-data-set.md) (synthetic / masked test data) and is distinct from analysis [Data Migration](../analysis/data-migration.md) (moving EXISTING bulk records from a legacy as-is system to the target). Seed data is loaded ONCE into a fresh environment; data-migration moves BULK records from a legacy system. It is **not** test data (→ [Test Data Set](../testing/test-data-set.md)), **not** data migration (→ [Data Migration](../analysis/data-migration.md)), **not** the schema (→ [Data Entity](../analysis/data-entity.md)), and **not** the runtime config (→ [Runtime Configuration](runtime-configuration.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. SD-001 |
| name | string | yes | |
| environment | ref → [Environment](../design/environment.md) | yes | the target environment |
| conformsTo | ref[] → [Data Entity](../analysis/data-entity.md) | yes | the prod schemas it conforms to |
| dataType | enum (admin-accounts / reference-data / default-config / master-data) | yes | |
| loadOrder | int | yes | dependencies between seed data sets (lower = earlier) |
| loadScript | ref → [Code Unit](../development/code-unit.md) | yes | the script that loads the data |
| volume | string | yes | size / row count |
| resetStrategy | enum (per-deployment / per-environment / one-time) | yes | |

## 4. State (as-is / target)

Stateless — a dataset definition; the data is loaded per [Deployment Execution](deployment-execution.md).

## 5. Relationships (semantic references)

- **Refers to:** [Environment](../design/environment.md) (loaded into), [Data Entity](../analysis/data-entity.md) (conforms to), [Code Unit](../development/code-unit.md) (load script).
- **Referred by:** [Deployment Runbook](deployment-runbook.md), [Deployment Execution](deployment-execution.md).

## 6. Lifecycle / status

N/A — dataset definition; loaded per the `resetStrategy` during a [Deployment Execution](deployment-execution.md).

## 7. Template coverage

- `skills/rollout/shipping-and-launch/SKILL.md` Infrastructure (database migrations applied or ready to apply; initial data setup)

## 8. Non-overlap note

The test data belongs to testing [Test Data Set](../testing/test-data-set.md); the bulk legacy data movement belongs to analysis [Data Migration](../analysis/data-migration.md); the schema belongs to analysis [Data Entity](../analysis/data-entity.md); the runtime settings belong to [Runtime Configuration](runtime-configuration.md). The seed data is the one-time initial data for a fresh environment.
