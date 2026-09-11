# Pipeline

> **Slug:** `pipeline` | **View:** Pipeline View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the CI/CD pipeline definition — ordered stages, jobs, triggers, and the quality gates it enforces — that automates build, test, and delivery.
- **Purpose / when used:** the reusable automation definition; its executions are [Build Run](build-run.md)s.

## 2. Semantics (crisp)

`pipeline` is the reusable automation definition: ordered stages (build / test / package / deploy), jobs per stage, triggers (push / PR / schedule / manual), and the analysis [Quality Gate](../analysis/quality-gate.md)s it enforces (e.g. "all tests green", "no critical findings", "N approvals"). It is configured per design [Environment](../design/environment.md) (a pipeline may have dev / CI / prod variants). It is the definition-vs-instance counterpart of [Build Run](build-run.md). It is **not** the execution (→ [Build Run](build-run.md)), **not** a work package (→ analysis [Work Package](../analysis/work-package.md)), **not** a quality gate (it *enforces* gates), and **not** the build configuration (→ [Build Configuration](build-configuration.md) — a pipeline stage *invokes* a build configuration). Architecturally significant pipeline decisions are ADRs (analysis [Decision](../analysis/decision.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. PL-001 |
| name | string | yes | |
| stages | table (stage / jobs / triggers) | yes | ordered |
| enforcesGates | ref[] → [Quality Gate](../analysis/quality-gate.md) | yes | DoR / DoD / release-readiness |
| perEnvironment | ref[] → [Environment](../design/environment.md) | yes | dev / CI / staging / prod variants |
| definitionFile | string | yes | e.g. .github/workflows/ci.yml, Jenkinsfile |
| justifiedBy | ref → [Decision](../analysis/decision.md) | no | ADR for architecturally significant pipeline choices |

## 4. State (as-is / target)

Stateful. As-is pipeline (existing CI/CD, 🟤🔵) vs target pipeline. Change type marks new / modified / preserved / retired.

## 5. Relationships (semantic references)

- **Refers to:** [Quality Gate](../analysis/quality-gate.md) (enforces), [Environment](../design/environment.md) (per-environment variants), [Decision](../analysis/decision.md) (justified by).
- **Referred by:** [Build Run](build-run.md), rollout [Deployment Runbook](../rollout/deployment-runbook.md) (automatedByPipeline).

## 6. Lifecycle / status

N/A — declarative definition; revised via [Code Commit](code-commit.md). Status follows the repository's VCS state.

## 7. Template coverage

- A future `templates/development/*.md` CI/CD pipeline section.
- Automates the analysis [Quality Gate](../analysis/quality-gate.md) checks for `templates/design/software-architecture.md` §8.3 Environments promotion.

## 8. Non-overlap note

The execution belongs to [Build Run](build-run.md); the work belongs to analysis [Work Package](../analysis/work-package.md); the gate belongs to analysis [Quality Gate](../analysis/quality-gate.md); the build configuration belongs to [Build Configuration](build-configuration.md); the architecturally significant choice belongs to analysis [Decision](../analysis/decision.md). The pipeline is the reusable definition.
