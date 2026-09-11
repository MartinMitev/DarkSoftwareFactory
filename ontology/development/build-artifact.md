# Build Artifact

> **Slug:** `build-artifact` | **View:** Build View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the compiled / assembled output of a [Build Run](build-run.md) — JAR, container image, binary, bundle — identified by a digest and version.
- **Purpose / when used:** the immutable, deployable unit; the thing an analysis [Release](../analysis/release.md) deploys onto a design [Deployment Node](../design/deployment-node.md).

## 2. Semantics (crisp)

`build-artifact` is the produced, immutable output: a `kind` (library / container-image / binary / bundle / package), a version, a digest/hash, and provenance (which [Build Run](build-run.md) produced it). It packages one or more [Code Unit](code-unit.md)s, realises an analysis [Release](../analysis/release.md) (a release deploys one or more build artifacts), and is the deployable mapped onto a design [Deployment Node](../design/deployment-node.md). It is **not** the build execution (→ [Build Run](build-run.md)), **not** the release event (→ [Release](../analysis/release.md) — the release is the *deployment* event; the artifact is *what* is deployed), **not** the deployment mapping (→ [Deployment Node](../design/deployment-node.md)), and **not** the source (→ [Code Unit](code-unit.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. BA-001 |
| kind | enum (library / container-image / binary / bundle / package) | yes | |
| version | string | yes | semantic / build number |
| digest | string | yes | sha256 / content hash — immutability proof |
| producedBy | ref → [Build Run](build-run.md) | yes | provenance |
| packagesCodeUnits | ref[] → [Code Unit](code-unit.md) | yes | the sources it bundles |
| dependsOnArtifacts | ref[] → [Build Artifact](build-artifact.md) | no | other artifacts this one depends on (e.g. WAR → JAR, image → base image) |
| realisesRelease | ref → [Release](../analysis/release.md) | no | the release that deploys it |
| deploysTo | ref → [Deployment Node](../design/deployment-node.md) | no | the static mapping target |

## 4. State (as-is / target)

Stateless — an immutable output. Versions supersede, not mutate. Retired artifacts are unmapped from future releases.

## 5. Relationships (semantic references)

- **Refers to:** [Build Run](build-run.md) (produced by), [Code Unit](code-unit.md) (packages), [Release](../analysis/release.md) (realises), [Deployment Node](../design/deployment-node.md) (deploys to), [Build Artifact](build-artifact.md) (dependsOnArtifacts).
- **Referred by:** [Build Run](build-run.md), [Build Artifact](build-artifact.md) (dependsOnArtifacts), [Deployment Node](../design/deployment-node.md), rollout [Runtime Configuration](../rollout/runtime-configuration.md) (configuresArtifact), rollout [Deployment Runbook](../rollout/deployment-runbook.md) (deployment steps), rollout [Deployment Execution](../rollout/deployment-execution.md) (deployedArtifacts), analysis [Release](../analysis/release.md) (buildArtifacts), maintenance [Vulnerability Finding](../maintenance/vulnerability-finding.md) (affectedArtifacts).

## 6. Lifecycle / status

Immutable once produced. Superseded by a new version (new artifact). Retention governed by policy (analysis [Constraint](../analysis/constraint.md)).

## 7. Template coverage

- A future `templates/development/*.md` build-output / artifact-management section.
- The concrete deployable for `templates/design/software-architecture.md` §8 Deployment View (Building Block → Infrastructure mapping uses build artifacts).

## 8. Non-overlap note

The build execution belongs to [Build Run](build-run.md); the deployment event belongs to analysis [Release](../analysis/release.md); the software-to-infrastructure mapping belongs to [Deployment Node](../design/deployment-node.md); the source belongs to [Code Unit](code-unit.md). The artifact is the immutable output.
