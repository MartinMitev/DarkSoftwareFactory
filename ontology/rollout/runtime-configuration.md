# Runtime Configuration

> **Slug:** `runtime-configuration` | **View:** Runtime Configuration View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the environment-specific production runtime configuration — encrypted secret references, connection strings, environment variables, feature flags, resource limits, and monitoring/alert rules — deployed WITH a [Build Artifact](../development/build-artifact.md) to a design [Environment](../design/environment.md).
- **Purpose / when used:** the frozen runtime baseline that makes a production deployment reproducible; the production counterpart of the testing [Test Configuration](../testing/test-configuration.md) (which uses mocked deps).

## 2. Semantics (crisp)

`runtime-configuration` is the *runtime* config of the running system in a *real* environment: encrypted secret **references** (not the raw secrets — the vault is an analysis [Technology](../analysis/technology.md) / design [Infrastructure Resource](../design/infrastructure-resource.md)), connection strings to real databases/services, environment variables, feature-flag states, resource limits (CPU / memory / replicas), and monitoring/alert configuration. It configures a dev [Build Artifact](../development/build-artifact.md) deployed into a design [Environment](../design/environment.md), and is versioned and frozen per [Deployment Execution](deployment-execution.md). It is the **production counterpart** of the testing [Test Configuration](../testing/test-configuration.md) (test-time SUT config with mocked dependencies); it is distinct from dev [Build Configuration](../development/build-configuration.md) (build-time setup) and from design [Environment](../design/environment.md) (the deployment target context). It is **not** the test-time config (→ [Test Configuration](../testing/test-configuration.md)), **not** the build setup (→ [Build Configuration](../development/build-configuration.md)), **not** the deployment target (→ [Environment](../design/environment.md)), and **not** the artifact (→ [Build Artifact](../development/build-artifact.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. RC-prod-001 |
| version | string | yes | |
| environment | ref → [Environment](../design/environment.md) | yes | the target environment |
| configuresArtifact | ref → [Build Artifact](../development/build-artifact.md) | yes | the artifact this configures |
| secrets | table (key / vaultRef) | yes | references to a secrets vault, not raw secrets |
| connectionStrings | table (service / connectionString) | yes | real databases / external services |
| environmentVariables | table (var / value) | yes | |
| featureFlags | table (flag / state) | yes | runtime flag states |
| resourceLimits | table (resource / limit) | yes | CPU / memory / replicas |
| monitoringConfig | string | yes | alert rules / dashboards / log destinations |
| frozenAt | datetime | yes | baseline freeze timestamp |

## 4. State (as-is / target)

Stateless — an immutable baseline once frozen. New baselines are new versions.

## 5. Relationships (semantic references)

- **Refers to:** [Environment](../design/environment.md), [Build Artifact](../development/build-artifact.md).
- **Referred by:** [Deployment Runbook](deployment-runbook.md), [Deployment Execution](deployment-execution.md), maintenance [Monitoring Alert](../maintenance/monitoring-alert.md), maintenance [Maintenance Log](../maintenance/maintenance-log.md).

## 6. Lifecycle / status

Frozen at creation; superseded by a new version. Versioning governed by analysis [Governance](../analysis/governance.md) (configuration management practice).

## 7. Template coverage

- `skills/rollout/ci-cd-and-automation/SKILL.md` Environment Management (secrets in vault, not in code)
- `skills/rollout/shipping-and-launch/SKILL.md` Infrastructure (env vars set in production, logging and error reporting configured), Monitoring and Observability
- `skills/rollout/documentation-and-adrs/SKILL.md` (environment config conventions)

## 8. Non-overlap note

The test-time config belongs to testing [Test Configuration](../testing/test-configuration.md); the build setup belongs to development [Build Configuration](../development/build-configuration.md); the deployment target belongs to design [Environment](../design/environment.md); the compiled artifact belongs to development [Build Artifact](../development/build-artifact.md). The runtime configuration is the production runtime settings baseline.
