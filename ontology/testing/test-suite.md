# Test Suite

> **Slug:** `test-suite` | **View:** Test Design View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a named, reusable collection of [Test Case](test-case.md)s for a target/level with a `purpose` (regression / smoke / acceptance / exploratory / live), executed together by a [Test Run](test-run.md).
- **Purpose / when used:** the collection artefact — the regression suite, smoke suite, acceptance suite, exploratory set, live-test set; the unit executed by a [Test Run](test-run.md).

## 2. Semantics (crisp)

`test-suite` is the collection artefact — it groups [Test Case](test-case.md)s, has a `purpose` enum (regression / smoke / acceptance / exploratory / live), targets a design [Component](../design/component.md) / analysis [Application](../analysis/application.md) / [Business Process](../analysis/business-process.md), and is the definition executed by a [Test Run](test-run.md) (Test Suite : Test Run = dev [Pipeline](../development/pipeline.md) : [Build Run](../development/build-run.md) — definition vs instance). **Regression Test (item 4.2)** = a [Test Run](test-run.md) of a Test Suite with `purpose=regression`. It is **not** a test case (→ [Test Case](test-case.md)), **not** the execution (→ [Test Run](test-run.md)), and **not** a quality gate (it may be *gated by* analysis [Quality Gate](../analysis/quality-gate.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. TS-REG-001 |
| name | string | yes | |
| purpose | enum (regression / smoke / acceptance / exploratory / live) | yes | |
| contains | ref[] → [Test Case](test-case.md) | yes | |
| target | ref → [Component](../design/component.md) / [Application](../analysis/application.md) / [Business Process](../analysis/business-process.md) | yes | |
| coverageScope | string | yes | features / states / transitions covered |
| automationTarget | string | no | % automated |
| gatedBy | ref[] → [Quality Gate](../analysis/quality-gate.md) | no | the gate that requires this suite to pass |

## 4. State (as-is / target)

Stateless — a reusable collection; revised via [Change Request](../analysis/change-request.md).

## 5. Relationships (semantic references)

- **Refers to:** [Test Case](test-case.md) (contains), [Component](../design/component.md), [Application](../analysis/application.md), [Business Process](../analysis/business-process.md), [Quality Gate](../analysis/quality-gate.md).
- **Referred by:** [Test Run](test-run.md).

## 6. Lifecycle / status

N/A — collection artefact; status follows hosting document approval. Members added/removed via [Change Request](../analysis/change-request.md).

## 7. Template coverage

- `templates/testing/test-concept.md` §4.4 Automation Strategy (regression suites), §4.5 Risk-Based Prioritization
- `templates/testing/functional-test-cases.md` §2.2 Feature Test Case List, §3.2, §4.2, §5.2 (per-area suite lists)
- `templates/testing/technical-test-cases.md` §3.2 Unit, §4.2 Module, §5.3 Interface, §6.2 CI/CD (per-level suite lists)
- `templates/testing/non-functional-test-cases.md` §2.2 Performance, §3.2 Failover, §4.2 Security (per-NFR suite lists)
- `templates/testing/availability-live-test-cases.md` §4 Smoke, §5 Availability, §6 Runbook, §7 Rollback (live suite lists)
- `templates/testing/documentation-test-cases.md` §5 Test Suites (per-document suite lists)

## 8. Non-overlap note

A test case belongs to [Test Case](test-case.md); the execution belongs to [Test Run](test-run.md); the checkpoint belongs to analysis [Quality Gate](../analysis/quality-gate.md). The suite is the collection.
