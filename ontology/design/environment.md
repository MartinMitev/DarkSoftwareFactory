# Environment

> **Slug:** `environment` | **View:** Deployment View (Environments) | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a deployment target context — development, test, staging, pre-production, production, or a migration-specific parallel-run environment — with purpose, infrastructure, data, access, provisioning, and a promotion process.
- **Purpose / when used:** the atomic unit for the environments view; scopes [Deployment Node](deployment-node.md)s and houses [Infrastructure Resource](infrastructure-resource.md)s; defines how code moves from dev to production.

## 2. Semantics (crisp)

`environment` is a **named deployment context** (dev / test / staging / pre-prod / prod / migration-parallel / migration-test) distinguished by purpose, the [Infrastructure Resource](infrastructure-resource.md)s it contains, the data it holds, who can access it, who provisions it, and the promotion process to the next environment (typically realised by analysis [Release](../analysis/release.md)s). It is **not** a project phase (→ analysis [Phase](../analysis/phase.md) — a span of project work), **not** a release (→ [Release](../analysis/release.md) — the deployment event), **not** an infrastructure resource (→ [Infrastructure Resource](infrastructure-resource.md) — the resources live *in* the environment), and **not** a deployment mapping (→ [Deployment Node](deployment-node.md)). For Modernization, additional environments (migration-test, parallel-run) carry a `migrationFacet`.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. ENV-prod |
| name | enum (dev / test / staging / pre-prod / prod / migration-test / parallel-run) | yes | |
| purpose | string | yes | |
| contains | ref[] → [Infrastructure Resource](infrastructure-resource.md) | yes | |
| data | string | yes | data profile / sensitivity |
| access | string | yes | who can access |
| provisionedBy | ref → [Role](../analysis/role.md) / [Vendor](../analysis/vendor.md) | yes | |
| promotionProcess | string | yes | how code moves to the next environment |
| migrationFacet | bool | no | 🔵🟤 true for migration-specific environments |
| changeType | enum (new / modified / preserved / retired) | no | 🟤🔵 |

## 4. State (as-is / target)

Stateful. As-is environments (existing deployment targets, 🟤🔵) vs target environments; migration environments exist only during the transition journey.

## 5. Relationships (semantic references)

- **Refers to:** [Infrastructure Resource](infrastructure-resource.md) (contains), [Release](../analysis/release.md) (promotion path), [Role](../analysis/role.md), [Vendor](../analysis/vendor.md).
- **Referred by:** [Infrastructure Resource](infrastructure-resource.md), [Deployment Node](deployment-node.md), rollout [Runtime Configuration](../rollout/runtime-configuration.md), rollout [Seed Data Setup](../rollout/seed-data-setup.md), rollout [Deployment Runbook](../rollout/deployment-runbook.md), rollout [Deployment Execution](../rollout/deployment-execution.md).

## 6. Lifecycle / status

N/A — deployment context; status follows hosting document approval. Provisioning tracked by [Work Package](../analysis/work-package.md).

## 7. Template coverage

- `templates/design/software-architecture.md` §8.3 Environments (Environment / Purpose / Infrastructure / Data / Access / Provisioned By)
- `templates/design/software-architecture.md` §8.4 Legacy Deployment 🔵🟤 (additional migration environments)

## 8. Non-overlap note

A project phase belongs to analysis [Phase](../analysis/phase.md); the deployment event belongs to [Release](../analysis/release.md); the physical resource belongs to [Infrastructure Resource](infrastructure-resource.md); the software-to-infrastructure mapping belongs to [Deployment Node](deployment-node.md).
