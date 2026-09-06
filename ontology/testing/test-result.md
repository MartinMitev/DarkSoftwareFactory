# Test Result

> **Slug:** `test-result` | **View:** Test Execution View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the per-[Test Case](test-case.md) outcome of a [Test Run](test-run.md) — pass / fail / blocked, actual vs expected, evidence, and the [Issue](../analysis/issue.md) (defect) raised on failure.
- **Purpose / when used:** the individual verdict; the thing a [Test Run](test-run.md) produces and that raises a defect on failure.

## 2. Semantics (crisp)

`test-result` is the individual verdict: the [Test Case](test-case.md) executed, the [Test Run](test-run.md) it belongs to, a verdict (pass / fail / blocked / skipped / flaky), actual results vs expected, evidence (logs / screenshots / reports), and on failure a `raisesDefect` link to an analysis [Issue](../analysis/issue.md) (with `defectFacet=true`). It is the test counterpart of dev [Build Artifact](../development/build-artifact.md) (Build Run produces Build Artifacts; Test Run produces Test Results). It is **not** the test case (→ [Test Case](test-case.md)), **not** the run (→ [Test Run](test-run.md)), **not** the defect itself (→ [Issue](../analysis/issue.md) — it *raises* one), and **not** a static-analysis finding (→ dev [Static Analysis Finding](../development/static-analysis-finding.md) — that is pre-execution tool output, not a test verdict).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. TR-001-001 |
| testCase | ref → [Test Case](test-case.md) | yes | |
| testRun | ref → [Test Run](test-run.md) | yes | |
| verdict | enum (pass / fail / blocked / skipped / flaky) | yes | |
| actualResults | string | yes | |
| evidence | table (type / location / link) | yes | logs / screenshots / reports |
| duration | string | yes | |
| raisesDefect | ref → [Issue](../analysis/issue.md) | no | set when verdict=fail (defect with defectFacet=true) |
| timestamp | datetime | yes | |

## 4. State (as-is / target)

Stateless — a recorded verdict; immutable once produced.

## 5. Relationships (semantic references)

- **Refers to:** [Test Case](test-case.md), [Test Run](test-run.md), [Issue](../analysis/issue.md) (raises defect).
- **Referred by:** none.

## 6. Lifecycle / status

Immutable once produced. A re-test after a fix is a new [Test Run](test-run.md) producing new Test Results. A flaky verdict may be auto-requeued.

## 7. Template coverage

- `templates/testing/test-concept.md` §9.2 Gate-to-Evidence Traceability, §11.2 Metrics (pass rate, flaky rate)
- All case templates' "Evidence and Reporting" sections + per-case status columns (Pass/Fail, Status)
- `templates/testing/availability-live-test-cases.md` §3 Pass/Fail, §9 Evidence and Reporting

## 8. Non-overlap note

The test procedure belongs to [Test Case](test-case.md); the execution belongs to [Test Run](test-run.md); the defect belongs to analysis [Issue](../analysis/issue.md); the pre-execution tool finding belongs to dev [Static Analysis Finding](../development/static-analysis-finding.md). The test result is the per-case verdict.
