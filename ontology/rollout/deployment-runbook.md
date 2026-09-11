# Deployment Runbook

> **Slug:** `deployment-runbook` | **View:** Deployment Procedure View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the operational procedure for a specific deployment — pre-deployment steps, deployment steps, post-deployment verification, and rollback steps — referencing the artifacts, configs, seed data, and gates involved.
- **Purpose / when used:** the reusable definition executed by [Deployment Execution](deployment-execution.md)s; the general procedure for all project types (modernization references the analysis [Cutover](../analysis/cutover.md) switchover).

## 2. Semantics (crisp)

`deployment-runbook` is the **human-readable operational procedure**: ordered pre-deployment steps (infrastructure provisioning via dev [Code Unit](../development/code-unit.md) scripts, schema migrations via dev [Code Unit](../development/code-unit.md) scripts, [Seed Data Setup](seed-data-setup.md) loading, [Runtime Configuration](runtime-configuration.md) preparation), deployment steps (dev [Build Artifact](../development/build-artifact.md) push, config apply, traffic switch), post-deployment verification (smoke tests → testing [Test Case](../testing/test-case.md) testType=live, health checks, monitoring), and rollback steps (traffic revert, config revert, schema rollback). It references the dev [Pipeline](../development/pipeline.md) that automates it, the analysis [Quality Gate](../analysis/quality-gate.md)s enforced, and — for modernization — the analysis [Cutover](../analysis/cutover.md) switchover steps. It is the general procedure for ALL project types; `cutover` is the modernization-specific switchover with timed steps and legacy shutdown — the runbook REFERENCES cutover via `cutoverRef`, it does not re-define it. It is the definition-vs-instance counterpart of [Deployment Execution](deployment-execution.md) (as dev [Pipeline](../development/pipeline.md) is to [Build Run](../development/build-run.md)). It is **not** the pipeline (→ [Pipeline](../development/pipeline.md) — automation), **not** the release event (→ analysis [Release](../analysis/release.md) — business go-live), **not** the cutover (→ [Cutover](../analysis/cutover.md) — modernization switchover; the runbook references it), and **not** the execution record (→ [Deployment Execution](deployment-execution.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. DR-001 |
| name | string | yes | |
| release | ref → [Release](../analysis/release.md) | yes | the business release this runbook serves |
| targetEnvironments | ref[] → [Environment](../design/environment.md) | yes | dev / staging / prod |
| preDeploymentSteps | table (step / action / artifact / config / seedData / scriptCodeUnit) | yes | infra provisioning, schema migration, seed data, config prep |
| deploymentSteps | table (step / action / artifact / environment) | yes | artifact push, config apply, traffic switch |
| postDeploymentVerification | table (step / testCase → [Test Case](../testing/test-case.md) / healthCheck / monitoringCheck) | yes | smoke tests, health checks, monitoring |
| rollbackSteps | table (step / action / targetState) | yes | traffic revert, config revert, schema rollback |
| automatedByPipeline | ref → [Pipeline](../development/pipeline.md) | no | the pipeline that automates this runbook |
| enforcesGates | ref[] → [Quality Gate](../analysis/quality-gate.md) | yes | DoR / DoD / release-readiness |
| cutoverRef | ref → [Cutover](../analysis/cutover.md) | no | 🟤🔵 modernization switchover steps |
| justifiedBy | ref → [Decision](../analysis/decision.md) | no | ADR justifying the deployment approach |

## 4. State (as-is / target)

Stateful. As-is runbook (existing deployment procedure, 🟤🔵) vs target runbook. Change type marks new / modified / preserved / retired.

## 5. Relationships (semantic references)

- **Refers to:** [Release](../analysis/release.md), [Environment](../design/environment.md), [Build Artifact](../development/build-artifact.md), [Runtime Configuration](runtime-configuration.md), [Seed Data Setup](seed-data-setup.md), [Pipeline](../development/pipeline.md), [Cutover](../analysis/cutover.md), [Quality Gate](../analysis/quality-gate.md), [Test Case](../testing/test-case.md), [Decision](../analysis/decision.md), [Code Unit](../development/code-unit.md) (pre-deploy scripts).
- **Referred by:** [Deployment Execution](deployment-execution.md), analysis [Release](../analysis/release.md) (deploymentRunbook attribute).

## 6. Lifecycle / status

N/A — definition; status follows hosting document approval. Revised via analysis [Change Request](../analysis/change-request.md).

## 7. Template coverage

- `skills/rollout/shipping-and-launch/SKILL.md` Rollback Plan, Rollout Strategy, Staged Rollout
- `skills/rollout/ci-cd-and-automation/SKILL.md` Deployment Strategies, Rollback Plan, Staged Rollouts
- `templates/analysis/project-plan.md` §17.5 Cutover Runbook (modernization-specific, referenced via cutoverRef)

## 8. Non-overlap note

The pipeline automation belongs to development [Pipeline](../development/pipeline.md); the business go-live event belongs to analysis [Release](../analysis/release.md); the modernization switchover belongs to analysis [Cutover](../analysis/cutover.md); the execution record belongs to [Deployment Execution](deployment-execution.md). The runbook is the reusable procedure.
