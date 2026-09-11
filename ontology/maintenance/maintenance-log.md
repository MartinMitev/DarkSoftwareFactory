# Maintenance Log

> **Slug:** `maintenance-log` | **View:** Operations Documentation View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the chronological record of maintenance activities performed on a running [Environment](../design/environment.md) — patch applications, configuration changes, restarts, failovers, manual interventions — for audit, handover, and post-incident review.
- **Purpose / when used:** the audit/handover artefact for "maintenance activity documentation"; the operational counterpart of the development [Code Commit](../development/code-commit.md) (source history) and the rollout [Deployment Execution](../rollout/deployment-execution.md) (deployment history).

## 2. Semantics (crisp)

`maintenance-log` is the **operational history record**: a timestamped, append-only log of maintenance activities (patch applied / config changed / service restarted / failover triggered / manual intervention / health-check restored / scaling event), the analysis [Role](../analysis/role.md) who performed it, the design [Environment](../design/environment.md) affected, the design [Component](../design/component.md) / rollout [Runtime Configuration](../rollout/runtime-configuration.md) touched, and links to the [Ticket](ticket.md) it resolves, the rollout [Deployment Execution](../rollout/deployment-execution.md) it was part of, and the analysis [Decision](../analysis/decision.md) (if the activity required approval). It records **operational actions on the running system**, not source changes or deployments. It is the maintenance counterpart of development [Code Commit](../development/code-commit.md) (source history) and rollout [Deployment Execution](../rollout/deployment-execution.md) (deployment history). It is **not** a ticket (→ [Ticket](ticket.md) — it *resolves* one), **not** a deployment execution (→ [Deployment Execution](../rollout/deployment-execution.md) — that records a deployment; this records operational maintenance, which may include non-deployment actions like restarts/failovers), **not** a commit (→ [Code Commit](../development/code-commit.md) — that records a source change), and **not** a decision (→ analysis [Decision](../analysis/decision.md) — it *references* one if the action was approved).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. LOG-001 |
| timestamp | datetime | yes | |
| activityType | enum (patch-applied / config-changed / service-restarted / failover-triggered / manual-intervention / health-check-restored / scaling-event) | yes | |
| performedBy | ref → [Role](../analysis/role.md) | yes | |
| environment | ref → [Environment](../design/environment.md) | yes | |
| affectedComponent | ref → [Component](../design/component.md) | no | |
| runtimeConfigurationChanged | ref → [Runtime Configuration](../rollout/runtime-configuration.md) | no | when activityType=config-changed |
| resolvesTicket | ref → [Ticket](ticket.md) | no | |
| partOfDeployment | ref → [Deployment Execution](../rollout/deployment-execution.md) | no | when the action was a deployment |
| approvedBy | ref → [Decision](../analysis/decision.md) | no | if the action required approval |
| description | string | yes | |
| outcome | enum (success / partial / failed) | yes | |

## 4. State (as-is / target)

Stateless — an append-only history record; immutable once written.

## 5. Relationships (semantic references)

- **Refers to:** [Role](../analysis/role.md), [Environment](../design/environment.md), [Component](../design/component.md), [Runtime Configuration](../rollout/runtime-configuration.md), [Ticket](ticket.md), [Deployment Execution](../rollout/deployment-execution.md), [Decision](../analysis/decision.md).
- **Referred by:** none.

## 6. Lifecycle / status

N/A — append-only record. Corrections are new entries (never mutate).

## 7. Template coverage

- User-listed "maintenance activity documentation".
- A future `templates/maintenance/*.md` operations-log section.

## 8. Non-overlap note

The operational wrapper belongs to [Ticket](ticket.md); the deployment history belongs to rollout [Deployment Execution](../rollout/deployment-execution.md); the source history belongs to development [Code Commit](../development/code-commit.md); the approval belongs to analysis [Decision](../analysis/decision.md). The maintenance log is the operational action history on the running system.
