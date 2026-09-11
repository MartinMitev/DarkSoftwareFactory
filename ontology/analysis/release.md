# Release

> **Slug:** `release` | **Layer:** L5 Scope & Planning | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a deployment event with a scope subset, release type (major/minor/patch/hotfix), deployment approach, and a readiness gate.
- **Purpose / when used:** a go-live event that ships a subset of scope to users; maps epics/stories and (for Modernization) the legacy features retired.

## 2. Semantics (crisp)

`release` is a **deployment event** — a named release with a target date, the scope summary (which epics/stories ship), the release type, the deployment approach (blue-green, canary, feature flags, big bang), a readiness gate ([Quality Gate](quality-gate.md)), the compiled dev [Build Artifact](../development/build-artifact.md)s it deploys, and the rollout [Deployment Runbook](../rollout/deployment-runbook.md) that operationalises it. It is **not** a phase (a span — → [Phase](phase.md)) and **not** a milestone (a point in time — → [Milestone](milestone.md)). For Modernization, a release records which legacy features it retires (strangler-fig routing).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| name | string | yes | e.g. R1/MVP, R2 |
| targetDate | date | yes | |
| scopeSummary | string | yes | which scope ships |
| releaseType | enum (major / minor / patch / hotfix) | yes | |
| deploymentApproach | string | yes | blue-green / canary / feature flags / big bang |
| readinessGate | ref → [Quality Gate](quality-gate.md) | yes | release-readiness |
| legacyRetired | string | no | 🟤🔵 legacy features this release replaces |
| epics | ref[] → [Epic](epic.md) | yes | |
| buildArtifacts | ref[] → [Build Artifact](../development/build-artifact.md) | no | the compiled artifacts this release deploys |
| deploymentRunbook | ref → [Deployment Runbook](../rollout/deployment-runbook.md) | no | the operational procedure for this release |

## 4. State (as-is / target)

Journey — a release is a step in the as-is→target delivery.

## 5. Relationships (semantic references)

- **Refers to:** [Scope Item](scope-item.md), [Phase](phase.md), [User Story](user-story.md), [Epic](epic.md), [Milestone](milestone.md), [Quality Gate](quality-gate.md), [Build Artifact](../development/build-artifact.md), [Deployment Runbook](../rollout/deployment-runbook.md).
- **Referred by:** [Quality Gate](quality-gate.md), rollout [Deployment Runbook](../rollout/deployment-runbook.md), rollout [Deployment Execution](../rollout/deployment-execution.md).

## 6. Lifecycle / status

N/A — event; status: planned / in progress / shipped / rolled-back.

## 7. Template coverage

- `templates/analysis/user-stories.md` §2.2 Release-Aligned Story Map
- `templates/analysis/project-plan.md` §7.3 Release Plan, §18 Deployment & Release Strategy
- `skills/rollout/shipping-and-launch/SKILL.md` (release = go-live event; pre-launch checklist)
- `skills/rollout/ci-cd-and-automation/SKILL.md` (release pipeline stage, deployment strategies)

## 8. Non-overlap note

The phase span belongs to [Phase](phase.md); the point-in-time gate belongs to [Milestone](milestone.md). The compiled deployable belongs to development [Build Artifact](../development/build-artifact.md); the operational procedure belongs to rollout [Deployment Runbook](../rollout/deployment-runbook.md); the deployment execution record belongs to rollout [Deployment Execution](../rollout/deployment-execution.md).
