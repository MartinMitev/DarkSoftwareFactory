# Deployment Execution

> **Slug:** `deployment-execution` | **View:** Deployment Execution View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the record of a specific deployment to a specific environment — which artifacts, which runtime config, which seed data, the result (success / failure / rolled-back), and the triggering build run or manual trigger.
- **Purpose / when used:** the per-deployment execution record; the deployment counterpart of a development [Build Run](../development/build-run.md) and a testing [Test Run](../testing/test-run.md).

## 2. Semantics (crisp)

`deployment-execution` is the **deployment-specific execution record**: the [Deployment Runbook](deployment-runbook.md) executed, the dev [Build Artifact](../development/build-artifact.md)s deployed, the [Runtime Configuration](runtime-configuration.md) applied, the [Seed Data Setup](seed-data-setup.md) loaded, the design [Environment](../design/environment.md) deployed to, a trigger (dev [Build Run](../development/build-run.md) / manual / scheduled / rollback / emergency), a `direction` (forward / rollback), a status (running / success / failed / rolled-back), logs, and the testing [Test Run](../testing/test-run.md) used for post-deployment verification. It is the deployment counterpart of dev [Build Run](../development/build-run.md) (build execution) and testing [Test Run](../testing/test-run.md) (test execution). A `build-run` may TRIGGER a deployment-execution (when the pipeline reaches the deploy stage), but a deployment-execution can also be manual, scheduled, or a rollback — independent of a build-run. **Rollback is folded** via `direction=rollback` — there is no separate rollback artefact. It is **not** the build execution (→ [Build Run](../development/build-run.md)), **not** the business release event (→ analysis [Release](../analysis/release.md)), **not** the runbook (→ [Deployment Runbook](deployment-runbook.md) — definition vs execution), and **not** the test execution (→ [Test Run](../testing/test-run.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. DE-001 |
| executes | ref → [Deployment Runbook](deployment-runbook.md) | yes | |
| deployedArtifacts | ref[] → [Build Artifact](../development/build-artifact.md) | yes | |
| appliedConfiguration | ref → [Runtime Configuration](runtime-configuration.md) | yes | |
| loadedSeedData | ref[] → [Seed Data Setup](seed-data-setup.md) | no | |
| targetEnvironment | ref → [Environment](../design/environment.md) | yes | |
| trigger | enum (build-run / manual / scheduled / rollback / emergency) | yes | |
| triggeredByBuildRun | ref → [Build Run](../development/build-run.md) | no | set when trigger=build-run |
| direction | enum (forward / rollback) | yes | rollback is folded here |
| status | enum (running / success / failed / rolled-back) | yes | |
| verificationTestRun | ref → [Test Run](../testing/test-run.md) | no | post-deploy smoke / verification |
| logsLocation | string | yes | |
| duration | string | yes | |
| timestamp | datetime | yes | |
| approvedBy | ref → [Decision](../analysis/decision.md) | no | the go/no-go decision |

## 4. State (as-is / target)

Stateless — a single execution record; immutable once finished.

## 5. Relationships (semantic references)

- **Refers to:** [Deployment Runbook](deployment-runbook.md) (executes), [Build Artifact](../development/build-artifact.md) (deployed), [Runtime Configuration](runtime-configuration.md) (applied), [Seed Data Setup](seed-data-setup.md) (loaded), [Environment](../design/environment.md) (target), [Build Run](../development/build-run.md) (triggered by), [Test Run](../testing/test-run.md) (verification), [Decision](../analysis/decision.md) (approved by).
- **Referred by:** none.

## 6. Lifecycle / status

running → success / failed / rolled-back. A failed deployment may be followed by a rollback deployment-execution (direction=rollback). Retries are new Deployment Executions.

## 7. Template coverage

- `skills/rollout/shipping-and-launch/SKILL.md` Post-Launch Verification, Rollback execution, Staged Rollout execution
- `skills/rollout/ci-cd-and-automation/SKILL.md` staged rollout execution, rollback workflow

## 8. Non-overlap note

The build execution belongs to development [Build Run](../development/build-run.md); the business go-live event belongs to analysis [Release](../analysis/release.md); the runbook belongs to [Deployment Runbook](deployment-runbook.md); the test execution belongs to testing [Test Run](../testing/test-run.md). Rollback is folded via `direction=rollback`. The deployment execution is the per-deployment record.
