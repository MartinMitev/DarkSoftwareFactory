# Test Run

> **Slug:** `test-run` | **View:** Test Execution View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a single execution of a [Test Suite](test-suite.md) (or set of [Test Case](test-case.md)s) against a frozen configuration baseline, with a data-ingest setup phase, status, logs, and the [Test Result](test-result.md)s it produces.
- **Purpose / when used:** the execution instance; the provenance record for each produced test result.

## 2. Semantics (crisp)

`test-run` is the *execution instance* (dev [Build Run](../development/build-run.md) is to [Pipeline](../development/pipeline.md) as Test Run is to [Test Suite](test-suite.md)). It has a `trigger` (dev [Pull Request](../development/pull-request.md) / [Code Commit](../development/code-commit.md) / analysis [Release](../analysis/release.md) / schedule / manual), a `configurationBaseline` (the frozen [Test Configuration](test-configuration.md) + [Test Data Set](test-data-set.md)s + design [Environment](../design/environment.md) + dev [Build Artifact](../development/build-artifact.md)), a **data-ingest setup phase** (loads/masks/resets test data — covers **3.1 Test Data Ingest** as a `setupPhase` table, not a separate artefact), a status (running / success / failed / cancelled), logs, and the [Test Result](test-result.md)s produced. It may be *triggered by* a dev [Build Run](../development/build-run.md) (CI-executed tests) — the Build Run owns build + package; the Test Run owns test verdicts. **Configuration Management (item 3.4)** is captured by the immutable `configurationBaseline` (a practice governed by analysis [Governance](../analysis/governance.md)). It is **not** the suite definition (→ [Test Suite](test-suite.md)), **not** the per-case outcome (→ [Test Result](test-result.md)), **not** the build execution (→ [Build Run](../development/build-run.md)), and **not** the deployment event (→ [Release](../analysis/release.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. TR-001 |
| executes | ref → [Test Suite](test-suite.md) | yes | |
| trigger | ref → [Pull Request](../development/pull-request.md) / [Code Commit](../development/code-commit.md) / [Release](../analysis/release.md) / schedule / manual | yes | |
| configurationBaseline | table (testConfig → [Test Configuration](test-configuration.md) / dataSets → [Test Data Set](test-data-set.md)[] / environment → [Environment](../design/environment.md) / buildArtifact → [Build Artifact](../development/build-artifact.md)) | yes | the frozen baseline — configuration management |
| setupPhase | table (provisioningMethod / validation / reset) | yes | covers 3.1 Test Data Ingest |
| status | enum (running / success / failed / cancelled) | yes | |
| logsLocation | string | yes | |
| duration | string | yes | |
| producedResults | ref[] → [Test Result](test-result.md) | no | empty if cancelled before completion |
| triggeredByBuildRun | ref → [Build Run](../development/build-run.md) | no | for CI-executed tests |
| timestamp | datetime | yes | |

## 4. State (as-is / target)

Stateless — a single execution record; immutable once finished.

## 5. Relationships (semantic references)

- **Refers to:** [Test Suite](test-suite.md), [Test Configuration](test-configuration.md), [Test Data Set](test-data-set.md), [Environment](../design/environment.md), [Build Artifact](../development/build-artifact.md), [Pull Request](../development/pull-request.md), [Code Commit](../development/code-commit.md), [Release](../analysis/release.md), [Build Run](../development/build-run.md), [Test Result](test-result.md).
- **Referred by:** [Test Result](test-result.md), analysis [Issue](../analysis/issue.md) (defect facet `foundByTestRun`).

## 6. Lifecycle / status

running → success / failed / cancelled. A failed run still produces [Test Result](test-result.md)s for executed cases. Retries are new Test Runs.

## 7. Template coverage

- `templates/testing/test-concept.md` §11.1 Test Cycles / Regression Runs (execution cadence), §11.2 Metrics (pass rate, flaky rate)
- `templates/testing/availability-live-test-cases.md` §3 Live Test Case Format (execution + observed results + timestamp + evidence)
- All case templates' "Evidence and Reporting" sections (execution log, dashboard links)

## 8. Non-overlap note

The suite definition belongs to [Test Suite](test-suite.md); the per-case verdict belongs to [Test Result](test-result.md); the build execution belongs to dev [Build Run](../development/build-run.md); the deployment event belongs to analysis [Release](../analysis/release.md). The test run is the test-execution instance.
