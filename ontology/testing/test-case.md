# Test Case

> **Slug:** `test-case` | **View:** Test Design View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the atomic test procedure — preconditions, steps, expected results, priority, automation, evidence — that verifies one or more analysis [Acceptance Criterion](../analysis/acceptance-criterion.md)s / [Requirement](../analysis/requirement.md)s against a target, with a `testType` enum covering all nine test entities (document, unit, module, interface, cicd, component, process, usability, non-functional, live).
- **Purpose / when used:** the atomic unit of test design; folded into [Test Suite](test-suite.md)s and executed by [Test Run](test-run.md)s.

## 2. Semantics (crisp)

`test-case` is the **single artefact for every test procedure**. Its `testType` enum is `document / unit / module / interface / cicd / component / process / usability / non-functional / live`, with per-type facets:
- `testType=document` → `documentUnderTest` (analysis [Documentation Inventory](../analysis/documentation-inventory.md) / [Project Understanding](../analysis/project-understanding.md)), `method` (review / checklist / cross-reference) — covers 1.1 Document Review.
- `testType=unit/module` → `componentUnderTest` (dev [Code Unit](../development/code-unit.md) / design [Component](../design/component.md)) — covers 1.2 Module/Unit Test.
- `testType=interface` → `interfaceUnderTest` (analysis [Interface](../analysis/interface.md)), `versioningRules`, `authNAuthZ` — covers 1.3 Interface Test.
- `testType=cicd` → `pipelineStageUnderTest` (dev [Pipeline](../development/pipeline.md)), `trigger` — covers 1.4 CI/CD Test.
- `testType=component` → `componentUnderTest` (design [Component](../design/component.md)) — covers 1.5 Component Test.
- `testType=process` → `processUnderTest` (analysis [Business Process](../analysis/business-process.md)), `stateTransitionModel` (states/transitions/invariants) — covers 1.6 Process Test.
- `testType=usability` → `personaUnderTest` (analysis [Persona](../analysis/persona.md)), `successCriteria`, `taskSuccess` — covers 1.7 Usability Test.
- `testType=non-functional` → `nfrCategory` (performance / stress / failover-recovery / security), `workloadModel` (perf), `failureMode`+`rtoRpo` (failover), `threatCWE` (security) — covers 1.8 Non-functional Test.
- `testType=live` → `liveCategory` (smoke / monitoring / runbook / rollback), `safetyConstraints` (stop conditions / approved windows / data restrictions) — covers 1.9 Live Test incl. availability.

It `verifies` analysis [Acceptance Criterion](../analysis/acceptance-criterion.md)s / [Requirement](../analysis/requirement.md)s / [Use Case](../analysis/use-case.md)s / [Business Process](../analysis/business-process.md)es / design [Quality Scenario](../design/quality-scenario.md)s, runs in a design [Environment](../design/environment.md) (or live = prod), uses [Test Data Set](test-data-set.md)s and [Test Configuration](test-configuration)s, and is grouped into [Test Suite](test-suite.md)s. It is **not** the acceptance condition (→ [Acceptance Criterion](../analysis/acceptance-criterion.md)), **not** the V&V strategy (→ [Verification & Validation](../analysis/verification-validation.md)), **not** the execution (→ [Test Run](test-run.md)), and **not** the result (→ [Test Result](test-result.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. TC-UNIT-001, TC-FEAT-001 |
| title | string | yes | |
| testType | enum (document / unit / module / interface / cicd / component / process / usability / non-functional / live) | yes | folds the 9 test entities |
| target | ref → [Component](../design/component.md) / [Code Unit](../development/code-unit.md) / [Interface](../analysis/interface.md) / [Business Process](../analysis/business-process.md) / [Persona](../analysis/persona.md) / [Documentation Inventory](../analysis/documentation-inventory.md) / [Pipeline](../development/pipeline.md) / [Environment](../design/environment.md) | yes | depends on testType |
| preconditions | string | yes | |
| steps | table (step / action) | yes | numbered |
| expectedResults | string | yes | |
| negativeEdgeCases | string | no | |
| priority | enum (P0 / P1 / P2) | yes | P0 blocks build/deploy |
| automation | enum (manual / automated) | yes | |
| verifies | ref[] → [Acceptance Criterion](../analysis/acceptance-criterion.md) / [Requirement](../analysis/requirement.md) / [Use Case](../analysis/use-case.md) / [Business Process](../analysis/business-process.md) / [Quality Scenario](../design/quality-scenario.md) | yes | |
| usesData | ref[] → [Test Data Set](test-data-set.md) | no | |
| usesConfig | ref → [Test Configuration](test-configuration.md) | no | |
| runsIn | ref → [Environment](../design/environment.md) | yes | prod for live tests |
| documentUnderTest | ref → [Documentation Inventory](../analysis/documentation-inventory.md) / [Project Understanding](../analysis/project-understanding.md) | no | required when testType=document |
| method | enum (review / checklist / cross-reference / sampling) | no | required when testType=document |
| componentUnderTest | ref → [Component](../design/component.md) / [Code Unit](../development/code-unit.md) | no | required when testType=unit/module/component |
| interfaceUnderTest | ref → [Interface](../analysis/interface.md) | no | required when testType=interface |
| versioningRules | string | no | required when testType=interface |
| authNAuthZ | string | no | required when testType=interface |
| pipelineStageUnderTest | ref → [Pipeline](../development/pipeline.md) | no | required when testType=cicd |
| trigger | enum (push / PR / schedule / manual) | no | required when testType=cicd |
| processUnderTest | ref → [Business Process](../analysis/business-process.md) | no | required when testType=process |
| stateTransitionModel | table (state / transition / invariant / invalidTransition) | no | required when testType=process |
| personaUnderTest | ref → [Persona](../analysis/persona.md) | no | required when testType=usability |
| successCriteria | string | no | required when testType=usability |
| taskSuccess | string | no | required when testType=usability |
| nfrCategory | enum (performance / stress / failover-recovery / security) | no | required when testType=non-functional |
| workloadModel | string | no | required when testType=non-functional, nfrCategory=performance/stress |
| failureMode | string | no | required when testType=non-functional, nfrCategory=failover-recovery |
| rtoRpo | string | no | required when testType=non-functional, nfrCategory=failover-recovery |
| threatCWE | string | no | required when testType=non-functional, nfrCategory=security |
| liveCategory | enum (smoke / monitoring / runbook / rollback) | no | required when testType=live |
| safetyConstraints | table (stopConditions / approvedWindows / dataRestrictions / onCallStakeholders) | no | required when testType=live |

## 4. State (as-is / target)

Stateless — a test procedure; lifecycle is design → reviewed → approved → executed (status lives on [Test Result](test-result.md)).

## 5. Relationships (semantic references)

- **Refers to:** [Acceptance Criterion](../analysis/acceptance-criterion.md), [Requirement](../analysis/requirement.md), [Use Case](../analysis/use-case.md), [Business Process](../analysis/business-process.md), [Quality Scenario](../design/quality-scenario.md), [Component](../design/component.md), [Code Unit](../development/code-unit.md), [Interface](../analysis/interface.md), [Persona](../analysis/persona.md), [Pipeline](../development/pipeline.md), [Documentation Inventory](../analysis/documentation-inventory.md), [Environment](../design/environment.md), [Test Data Set](test-data-set.md), [Test Configuration](test-configuration.md).
- **Referred by:** [Test Suite](test-suite.md), [Test Result](test-result.md), rollout [Deployment Runbook](../rollout/deployment-runbook.md) (postDeploymentVerification).

## 6. Lifecycle / status

Status: Draft → Reviewed → Approved. Changes via [Change Request](../analysis/change-request.md). Execution status lives on [Test Result](test-result.md).

## 7. Template coverage

- `templates/testing/functional-test-cases.md` §2 Feature Tests, §3 Business Component Tests, §4 Business Process Tests, §5 Usability Tests (feature/component/process/usability testType)
- `templates/testing/technical-test-cases.md` §3 Unit, §4 Module, §5 Interface/Service, §6 CI/CD (unit/module/interface/cicd testType)
- `templates/testing/non-functional-test-cases.md` §2 Performance/Stress, §3 Failover/Recovery, §4 Security (non-functional testType + nfrCategory)
- `templates/testing/availability-live-test-cases.md` §4 Smoke, §5 Availability/Monitoring, §6 Runbook, §7 Rollback (live testType + liveCategory)
- `templates/testing/documentation-test-cases.md` §4 Documentation Test Case Format, §5 Test Suites, §6 Cross-Document Consistency (document testType)
- `templates/testing/test-concept.md` §7.3 Functional Test Case Template, §8.4 Lifecycle Test Case Template (component/process testType)

## 8. Non-overlap note

The acceptance condition belongs to [Acceptance Criterion](../analysis/acceptance-criterion.md); the V&V strategy belongs to [Verification & Validation](../analysis/verification-validation.md); the execution belongs to [Test Run](test-run.md); the verdict belongs to [Test Result](test-result.md). The 9 test entities are folded via `testType` enum — no separate per-type artefact.
