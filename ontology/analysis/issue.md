# Issue

> **Slug:** `issue` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** an occurred problem with category, priority, owner, status, resolution, and impact — folding the **defect** discovered in testing (via `defectFacet`) and the **incident** discovered in operations (via `incidentFacet`) as orthogonal variants.
- **Purpose / when used:** the present-tense realised problem/blocker; distinct from a risk (a potential future harm); the single artefact for every occurred problem, including test-discovered defects and ops-discovered incidents.

## 2. Semantics (crisp)

`issue` is an **occurred present problem**: a description, a category (technical, process, resource, dependency, vendor, organizational, migration), a priority (critical/high/medium/low), an owner, a status (open/in-progress/resolved/closed), a resolution, and an impact (budget/schedule/scope/quality). A **defect discovered in testing** is an `issue` with `defectFacet=true`, carrying `defectSeverity` (Critical/High/Medium/Low — the test-defect severity model from the testing templates), `reproducibility` (always/intermittent/one-off), `foundInBuild` (the dev [Build Artifact](../development/build-artifact.md) under test), `foundByTestRun` (the testing [Test Run](../testing/test-run.md)), `foundInEnvironment` (the design [Environment](../design/environment.md) where it was found), and `rootCauseAnalysis` (text — covers defect analysis). A **production incident discovered by operations** is an `issue` with `incidentFacet=true`, carrying `incidentSeverity` (Critical/Major/Minor — ITIL incident severity, distinct from defect severity), `affectedEnvironment` (the design [Environment](../design/environment.md) where the incident occurred), `detectedByAlert` (the maintenance [Monitoring Alert](../maintenance/monitoring-alert.md) that detected it), and `raisedTicket` (the maintenance [Ticket](../maintenance/ticket.md) tracking the incident). The two facets are **orthogonal** — a problem can be both a defect (test-discovered) and an incident (ops-discovered). The defect/incident itself is owned here (no separate testing/maintenance defect/incident artefact); the *fix* is delivered as dev [Code Commit](../development/code-commit.md)/[Pull Request](../development/pull-request.md), the *re-test* is a testing [Test Run](../testing/test-run.md) of a regression [Test Suite](../testing/test-suite.md), and the *approval* is a [Change Request](change-request.md)/[Decision](decision.md). It is **not** a risk (a potential future harm — → [Risk](risk.md)) and **not** a gap (→ [Gap & Contradiction](gap-and-contradiction.md)). For Brown Field / Modernization it includes migration issues (data inconsistency, feature gap, cutover blockers). A risk that materialises becomes an issue.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| description | string | yes | |
| category | string | yes | |
| priority | enum (critical / high / medium / low) | yes | |
| owner | ref → [Stakeholder](stakeholder.md) | yes | |
| status | enum (open / in-progress / resolved / closed) | yes | |
| resolution | string | no | |
| impact | string | yes | budget/schedule/scope/quality |
| defectFacet | bool | no | true = test-discovered defect |
| defectSeverity | enum (Critical / High / Medium / Low) | no | required when defectFacet=true (test-defect severity model) |
| reproducibility | enum (always / intermittent / one-off) | no | required when defectFacet=true |
| foundInBuild | ref → [Build Artifact](../development/build-artifact.md) | no | required when defectFacet=true |
| foundByTestRun | ref → [Test Run](../testing/test-run.md) | no | required when defectFacet=true |
| foundInEnvironment | ref → [Environment](../design/environment.md) | no | required when defectFacet=true |
| rootCauseAnalysis | string | no | defect analysis (4.1); required when defectFacet=true |
| incidentFacet | bool | no | true = ops-discovered production incident |
| incidentSeverity | enum (Critical / Major / Minor) | no | required when incidentFacet=true (ITIL severity, distinct from defect severity) |
| affectedEnvironment | ref → [Environment](../design/environment.md) | no | required when incidentFacet=true |
| detectedByAlert | ref → [Monitoring Alert](../maintenance/monitoring-alert.md) | no | the alert that detected the incident |
| raisedTicket | ref → [Ticket](../maintenance/ticket.md) | no | the ticket tracking the incident |

## 4. State (as-is / target)

Stateless — a present problem.

## 5. Relationships (semantic references)

- **Refers to:** [Stakeholder](stakeholder.md) (owner). When `defectFacet=true`: [Build Artifact](../development/build-artifact.md), [Test Run](../testing/test-run.md), [Environment](../design/environment.md). When `incidentFacet=true`: [Environment](../design/environment.md), maintenance [Monitoring Alert](../maintenance/monitoring-alert.md), maintenance [Ticket](../maintenance/ticket.md).
- **Referred by:** none (analysis); in testing, a [Test Result](../testing/test-result.md) *raises* an issue (defect); in development, a [Static Analysis Finding](../development/static-analysis-finding.md) *triages to* an issue; in maintenance, a [Monitoring Alert](../maintenance/monitoring-alert.md) *detects* (via `detectedByAlert`) and a [Ticket](../maintenance/ticket.md) *links to* (via `linkedIssue`) an issue (incident).

## 6. Lifecycle / status

Status: open → in-progress → resolved → closed. Critical issues escalate immediately. For defects: open → assigned → fixed (dev commit) → verified (regression test run) → closed. For incidents: open → triaged (maintenance [Ticket](../maintenance/ticket.md)) → in-progress → resolved → closed; may reopen.

## 7. Template coverage

- `templates/analysis/project-plan.md` §15 Issue Management (incl. §15.1 process, §15.2 priorities, §15.3 log)
- `templates/testing/test-concept.md` §5.2 Defect Severity and Launch Blocking Rules, §11.1 Defect Triage
- `templates/testing/functional-test-cases.md` §6 Coverage and Traceability, §8 Evidence and Reporting (defects raised)
- `templates/testing/technical-test-cases.md` §7 Quality Gates and Exit Criteria (defect blocking)
- `templates/testing/non-functional-test-cases.md` §5 Quality Gates (security/perf defect thresholds)
- `templates/testing/availability-live-test-cases.md` §8 Quality Gates (live defect handling)
- `templates/testing/documentation-test-cases.md` §3.2 Severity Model, §7 Findings Log and Remediation Workflow
- `templates/testing/project-risk-profile.md` defect-severity and test-impact sections
- User-listed maintenance activities: continuous monitoring → incident issues (incidentFacet)

## 8. Non-overlap note

A potential future harm belongs to [Risk](risk.md); a missing piece of info belongs to [Gap & Contradiction](gap-and-contradiction.md). A **defect** is an `issue` with `defectFacet=true` — no separate defect artefact (would re-claim "occurred problem"). An **incident** is an `issue` with `incidentFacet=true` — no separate incident artefact. The two facets are orthogonal (a problem can be both). A dev [Static Analysis Finding](../development/static-analysis-finding.md) *triages to* an issue; a testing [Test Result](../testing/test-result.md) *raises* an issue (defect); a maintenance [Monitoring Alert](../maintenance/monitoring-alert.md) *detects* and a maintenance [Ticket](../maintenance/ticket.md) *links to* an issue (incident). The fix is a dev [Code Commit](../development/code-commit.md)/[Pull Request](../development/pull-request.md); the re-test is a testing [Test Run](../testing/test-run.md); the approval is a [Change Request](change-request.md)/[Decision](decision.md).
