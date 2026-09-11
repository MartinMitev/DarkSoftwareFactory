# Build Run

> **Slug:** `build-run` | **View:** Build View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a single execution of a [Pipeline](pipeline.md) that compiles / tests / packages [Code Unit](code-unit.md)s, with status, logs, duration, and the [Build Artifact](build-artifact.md)s it produces.
- **Purpose / when used:** the instance of a build/CI execution; the provenance record for each produced artifact.

## 2. Semantics (crisp)

`build-run` is the *instance* of a [Pipeline](pipeline.md) execution: a trigger (a [Pull Request](pull-request.md) / [Code Commit](code-commit.md) / schedule / manual), a status (running / success / failed / cancelled), logs, duration, and the [Build Artifact](build-artifact.md)s it produced. It executes in a design [Environment](../design/environment.md) (dev / CI / staging). It is the definition-vs-instance counterpart of [Pipeline](pipeline.md) (as analysis [Technology](../analysis/technology.md) is to design [Infrastructure Resource](../design/infrastructure-resource.md)). It is **not** the pipeline definition (→ [Pipeline](pipeline.md)), **not** the artifact (→ [Build Artifact](build-artifact.md) — it *produces* artifacts), **not** the deployment event (→ analysis [Release](../analysis/release.md)), and **not** the build configuration (→ [Build Configuration](build-configuration.md) — it *consumes* a configuration).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. BR-001 |
| executes | ref → [Pipeline](pipeline.md) | yes | |
| trigger | ref → [Pull Request](pull-request.md) / [Code Commit](code-commit.md) / schedule / manual | yes | |
| status | enum (running / success / failed / cancelled) | yes | |
| logsLocation | string | yes | |
| duration | string | yes | |
| producedArtifacts | ref[] → [Build Artifact](build-artifact.md) | no | empty if failed before packaging |
| ranIn | ref → [Environment](../design/environment.md) | yes | dev / CI / staging |
| timestamp | datetime | yes | |

## 4. State (as-is / target)

Stateless — a single execution record; immutable once finished.

## 5. Relationships (semantic references)

- **Refers to:** [Pipeline](pipeline.md) (executes), [Pull Request](pull-request.md), [Code Commit](code-commit.md), [Build Artifact](build-artifact.md) (produces), [Environment](../design/environment.md) (runs in).
- **Referred by:** [Build Artifact](build-artifact.md) (provenance), rollout [Deployment Execution](../rollout/deployment-execution.md) (triggeredByBuildRun).

## 6. Lifecycle / status

running → success / failed / cancelled. A failed run produces no artifacts. Retries are new Build Runs.

## 7. Template coverage

- A future `templates/development/*.md` CI / build-run history section.
- The execution record for `templates/design/software-architecture.md` §8.3 Environments (CI environment).

## 8. Non-overlap note

The pipeline definition belongs to [Pipeline](pipeline.md); the artifact belongs to [Build Artifact](build-artifact.md); the deployment event belongs to analysis [Release](../analysis/release.md); the build configuration belongs to [Build Configuration](build-configuration.md). The build run is the execution instance.
