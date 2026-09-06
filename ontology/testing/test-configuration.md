# Test Configuration

> **Slug:** `test-configuration` | **View:** Test Data View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the runtime configuration of the System Under Test during a test — the SUT [Build Artifact](../development/build-artifact.md) version, feature flags, mocked external dependencies, test accounts/roles, and environment variables — versioned and frozen as a baseline for a [Test Run](test-run.md).
- **Purpose / when used:** the frozen runtime baseline that makes a [Test Run](test-run.md) reproducible; distinct from the deployment target and the build setup.

## 2. Semantics (crisp)

`test-configuration` is the *runtime* config of the System Under Test *during a test*: the dev [Build Artifact](../development/build-artifact.md) under test, feature-flag state, mocked/stubbed analysis [Interface](../analysis/interface.md)s, test accounts mapped to analysis [Role](../analysis/role.md)/[Persona](../analysis/persona.md)s, environment variables, and observability settings. It runs in a design [Environment](../design/environment.md) (where) and is consumed by a [Test Run](test-run.md). **Configuration Management (item 3.4)** is the *practice* of versioning and recording these baselines (governed by analysis [Governance](../analysis/governance.md)), not a separate artefact. It is **not** the deployment target (→ [Environment](../design/environment.md)), **not** the build setup (→ dev [Build Configuration](../development/build-configuration.md)), **not** the test data (→ [Test Data Set](test-data-set.md)), and **not** a cross-cutting policy (→ design [Crosscutting Concern](../design/crosscutting-concern.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. TC-001 |
| version | string | yes | |
| sutBuildArtifact | ref → [Build Artifact](../development/build-artifact.md) | yes | the SUT under test |
| featureFlags | table (flag / state) | yes | |
| mockedDependencies | ref[] → [Interface](../analysis/interface.md) | no | mocked/stubbed external systems |
| testAccounts | ref[] → [Role](../analysis/role.md) / [Persona](../analysis/persona.md) | yes | |
| environmentVariables | table (var / value) | yes | |
| runsIn | ref → [Environment](../design/environment.md) | yes | |
| frozenAt | datetime | yes | baseline freeze timestamp |

## 4. State (as-is / target)

Stateless — an immutable baseline once frozen. New baselines are new versions.

## 5. Relationships (semantic references)

- **Refers to:** [Build Artifact](../development/build-artifact.md), [Interface](../analysis/interface.md), [Role](../analysis/role.md), [Persona](../analysis/persona.md), [Environment](../design/environment.md).
- **Referred by:** [Test Run](test-run.md), [Test Case](test-case.md).

## 6. Lifecycle / status

Frozen at creation; superseded by a new version. Versioning and recording governed by analysis [Governance](../analysis/governance.md) (configuration management practice).

## 7. Template coverage

- `templates/testing/test-concept.md` §10.1 Environments, §6.2 Test Prerequisites
- `templates/testing/availability-live-test-cases.md` §2 Prerequisites (test accounts, monitoring access, runbooks)
- `templates/testing/non-functional-test-cases.md` §2.1 Environment (perf env details)

## 8. Non-overlap note

The deployment target belongs to design [Environment](../design/environment.md); the build setup belongs to dev [Build Configuration](../development/build-configuration.md); the test data belongs to [Test Data Set](test-data-set.md); the cross-cutting policy belongs to design [Crosscutting Concern](../design/crosscutting-concern.md). Configuration management is a governance practice, not an artefact.
