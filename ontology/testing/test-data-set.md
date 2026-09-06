# Test Data Set

> **Slug:** `test-data-set` | **View:** Test Data View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a synthetic or masked dataset conforming to one or more analysis [Data Entity](../analysis/data-entity.md) schemas, with generation method, volume, masking, retention, and reset strategy, used by [Test Case](test-case.md)s and ingested by [Test Run](test-run.md)s.
- **Purpose / when used:** the atomic unit of test data; the test-phase counterpart of the analysis production schema.

## 2. Semantics (crisp)

`test-data-set` is the test data: a `sourceType` (synthetic / masked-prod-like / fresh), the analysis [Data Entity](../analysis/data-entity.md) schemas it conforms to, a generation/masking method, volume/distribution, retention, and a reset strategy (per-test / per-suite / per-run). It is the test-phase counterpart of analysis `data-entity` (the production schema) — an *instance dataset* conforming to the schema, **not** the schema itself. It is **not** the production entity (→ [Data Entity](../analysis/data-entity.md)), **not** the runtime config (→ [Test Configuration](test-configuration.md)), and **not** the ingest operation (→ a phase of [Test Run](test-run.md) via `setupPhase`).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. TDS-001 |
| name | string | yes | |
| sourceType | enum (synthetic / masked-prod-like / fresh) | yes | |
| conformsTo | ref[] → [Data Entity](../analysis/data-entity.md) | yes | the prod schemas it conforms to |
| generationMethod | string | yes | |
| maskingMethod | string | no | required for masked-prod-like |
| volumeDistribution | string | yes | size, distribution |
| retention | string | yes | retention period |
| resetStrategy | enum (per-test / per-suite / per-run) | yes | |
| sensitivityClass | enum (public / internal / confidential / restricted) | yes | |

## 4. State (as-is / target)

Stateless — a dataset definition; the data is provisioned per [Test Run](test-run.md) `setupPhase`.

## 5. Relationships (semantic references)

- **Refers to:** [Data Entity](../analysis/data-entity.md) (conforms to).
- **Referred by:** [Test Case](test-case.md), [Test Run](test-run.md).

## 6. Lifecycle / status

N/A — dataset definition; refreshed per the `resetStrategy` during [Test Run](test-run.md) execution.

## 7. Template coverage

- `templates/testing/test-concept.md` §10.2 Test Data Strategy (synthetic / masked-prod-like data types, sources, masking, reset)

## 8. Non-overlap note

The production schema belongs to analysis [Data Entity](../analysis/data-entity.md); the runtime config belongs to [Test Configuration](test-configuration.md); the ingest operation belongs to a phase of [Test Run](test-run.md). The dataset is the test-phase instance conforming to the prod schema.
