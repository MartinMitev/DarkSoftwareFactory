# Deployment Node

> **Slug:** `deployment-node` | **View:** Deployment View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a specific mapping that binds a deployable [Component](component.md) (software artifact) to a concrete [Infrastructure Resource](infrastructure-resource.md) within a given [Environment](environment.md).
- **Purpose / when used:** the atomic unit of the deployment view; answers "which building block runs on which infrastructure, in which environment".

## 2. Semantics (crisp)

`deployment-node` is the **binding** between a deployable [Component](component.md) (the software artifact/executable) and a concrete [Infrastructure Resource](infrastructure-resource.md), scoped to an [Environment](environment.md) (dev/test/staging/prod/migration-parallel). It carries the artifact reference, mapping notes, and (for distributed systems) the per-environment instance. It is **not** the software building block (→ [Component](component.md)), **not** the physical resource (→ [Infrastructure Resource](infrastructure-resource.md)), **not** the environment (→ [Environment](environment.md)), and **not** the deployment event/increment (→ analysis [Release](../analysis/release.md) — a release *populates* deployment nodes over time). For Brown Field / Modernization, as-is nodes are the legacy deployment; target nodes are the new deployment; transition nodes support dual-running.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. DN-001 |
| component | ref → [Component](component.md) | yes | the deployable building block |
| artifact | string | yes | the deployable artifact (image, jar, binary) |
| infrastructureResource | ref → [Infrastructure Resource](infrastructure-resource.md) | yes | the host |
| environment | ref → [Environment](environment.md) | yes | dev / test / staging / prod / migration-parallel |
| mappingNotes | string | no | placement / sizing / replicas |
| changeType | enum (new / modified / preserved / retired) | no | 🟤🔵 |

## 4. State (as-is / target)

Stateful. As-is deployment (legacy mapping, 🟤🔵) vs target deployment; transition deployment for dual-running.

## 5. Relationships (semantic references)

- **Refers to:** [Component](component.md), [Infrastructure Resource](infrastructure-resource.md), [Environment](environment.md).
- **Referred by:** none (an analysis [Release](../analysis/release.md) populates deployment nodes over time, but the release references the deployment-node conceptually through the environment).

## 6. Lifecycle / status

N/A — static mapping; the deployment event is an analysis [Release](../analysis/release.md).

## 7. Template coverage

- `templates/design/software-architecture.md` §8.1 "Mapping of Building Blocks to Infrastructure" table (Building Block / Infrastructure Element / Environment / Notes)
- `templates/design/software-architecture.md` §8.2 level-2 "Building Blocks Mapped" column, §8.4 Legacy Deployment (current / transition / target state)

## 8. Non-overlap note

The software building block belongs to [Component](component.md); the physical resource belongs to [Infrastructure Resource](infrastructure-resource.md); the environment context belongs to [Environment](environment.md); the deployment event/increment belongs to analysis [Release](../analysis/release.md).
