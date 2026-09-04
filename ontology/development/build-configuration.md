# Build Configuration

> **Slug:** `build-configuration` | **View:** Build View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the concrete build / dependency configuration — build files, package manifests, toolchain config (Maven / Gradle / npm / Dockerfile / Makefile) — that compiles and assembles [Code Unit](code-unit.md)s into [Build Artifact](build-artifact.md)s.
- **Purpose / when used:** the declarative build setup; consumed by a [Build Run](build-run.md) execution.

## 2. Semantics (crisp)

`build-configuration` is the declarative build setup: a build tool, the declared dependencies (analysis [Technology](../analysis/technology.md) instances with versions), build steps/targets, and the design [Environment](../design/environment.md) it targets. It configures the build of [Code Unit](code-unit.md)s and is consumed by a [Build Run](build-run.md). Architecturally significant build/toolchain choices are recorded as ADRs (analysis [Decision](../analysis/decision.md)); this artefact holds the *concrete configuration*, not the decision. It is **not** the technology choice (→ [Technology](../analysis/technology.md)), **not** the build execution (→ [Build Run](build-run.md)), **not** the output (→ [Build Artifact](build-artifact.md)), and **not** the pipeline (→ [Pipeline](pipeline.md) — a pipeline *invokes* build runs; the build configuration is *what* is built).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. BC-001 |
| tool | enum (maven / gradle / npm / pip / docker / make / bazel / …) | yes | |
| declaresDependencies | ref[] → [Technology](../analysis/technology.md) | yes | with pinned versions |
| buildsCodeUnits | ref[] → [Code Unit](code-unit.md) | yes | the sources it compiles/assembles |
| targetsEnvironment | ref → [Environment](../design/environment.md) | yes | dev / CI / staging build target |
| buildSteps | table (step / command / output) | yes | |
| fileLocation | string | yes | e.g. pom.xml, package.json, Dockerfile |
| justifiedBy | ref → [Decision](../analysis/decision.md) | no | ADR for architecturally significant build choices |

## 4. State (as-is / target)

Stateful. As-is build config (existing toolchain, 🟤🔵) vs target build config. Change type marks new / modified / preserved / retired.

## 5. Relationships (semantic references)

- **Refers to:** [Technology](../analysis/technology.md) (declared dependencies), [Code Unit](code-unit.md) (builds), [Environment](../design/environment.md) (targets), [Decision](../analysis/decision.md) (justified by).
- **Referred by:** [Build Run](build-run.md).

## 6. Lifecycle / status

N/A — declarative configuration; revised via [Code Commit](code-commit.md). Status follows the repository's VCS state.

## 7. Template coverage

- A future `templates/development/*.md` build / toolchain configuration section.
- Maps the concrete realisation of `templates/design/software-architecture.md` §5.1 Technology Decisions and §8.3 Environments.

## 8. Non-overlap note

The technology choice belongs to [Technology](../analysis/technology.md); the build execution belongs to [Build Run](build-run.md); the output belongs to [Build Artifact](build-artifact.md); the pipeline belongs to [Pipeline](pipeline.md); the architecturally significant choice belongs to analysis [Decision](../analysis/decision.md).
