# Ticket

> **Slug:** `ticket` | **View:** Ticket Management View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the operational work item that tracks a maintenance action end-to-end — incident, service request, problem, change task, or vulnerability remediation task — linked to the analysis [Issue](../analysis/issue.md) (if a defect/problem) or [Risk](../analysis/risk.md) (if a vulnerability), assigned to a [Role](../analysis/role.md), with SLA, status, and resolution references.
- **Purpose / when used:** the operational wrapper that links upstream atoms (issue, risk, change-request, pull-request, test-run, deployment-execution) into a single tracked work item with SLA and assignment; the centrepiece of the maintenance phase.

## 2. Semantics (crisp)

`ticket` is the **operational tracking record** of a maintenance action: a type (incident / service-request / problem / change-task / vulnerability-remediation / monitoring-task), a subject, a reporter, an assignee (analysis [Role](../analysis/role.md)), an SLA (response + resolution targets), a priority (P1–P4), a status (new / triaged / in-progress / resolved / closed / reopened), and links to the upstream artefacts it operationalises — analysis [Issue](../analysis/issue.md) (the occurred problem/defect, with `incidentFacet` for ops-discovered), analysis [Risk](../analysis/risk.md) (the vulnerability before it materialises), development [Static Analysis Finding](../development/static-analysis-finding.md) (the scanner output that prompted it), analysis [Change Request](../analysis/change-request.md) (if it requires a scope/requirements change), development [Pull Request](../development/pull-request.md) (the code fix), testing [Test Run](../testing/test-run.md) (the regression verification), and rollout [Deployment Execution](../rollout/deployment-execution.md) (the patch deployment). It is the **operational wrapper** around the upstream atoms — it does not re-define the problem (→ [Issue](../analysis/issue.md)), the vulnerability (→ [Risk](../analysis/risk.md)), the change (→ [Change Request](../analysis/change-request.md)), or the fix (→ [Pull Request](../development/pull-request.md)). It carries the SLA, assignment, and lifecycle tracking that none of those upstream atoms have. It is **not** the problem (→ Issue), **not** the risk (→ Risk), **not** the change request (→ Change Request), **not** the code fix (→ Pull Request), and **not** a test result (→ Test Run).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. INC-001, SR-001, PROB-001, VULN-001 |
| type | enum (incident / service-request / problem / change-task / vulnerability-remediation / monitoring-task) | yes | |
| subject | string | yes | |
| reporter | ref → [Stakeholder](../analysis/stakeholder.md) | yes | |
| assignee | ref → [Role](../analysis/role.md) | yes | |
| priority | enum (P1 / P2 / P3 / P4) | yes | P1 = critical / immediate |
| sla | table (responseTarget / resolutionTarget) | yes | SLA windows |
| status | enum (new / triaged / in-progress / resolved / closed / reopened) | yes | |
| linkedIssue | ref → [Issue](../analysis/issue.md) | no | the occurred problem/defect (with incidentFacet for ops-discovered) |
| linkedRisk | ref → [Risk](../analysis/risk.md) | no | the vulnerability (before materialisation) |
| linkedFinding | ref → [Static Analysis Finding](../development/static-analysis-finding.md) | no | the scanner output that prompted it |
| linkedChangeRequest | ref → [Change Request](../analysis/change-request.md) | no | if it requires a scope/requirements change |
| resolvedByPullRequest | ref → [Pull Request](../development/pull-request.md) | no | the code fix |
| verifiedByTestRun | ref → [Test Run](../testing/test-run.md) | no | the regression verification |
| deployedBy | ref → [Deployment Execution](../rollout/deployment-execution.md) | no | the patch deployment |
| affectedComponent | ref → [Component](../design/component.md) | no | |
| affectedEnvironment | ref → [Environment](../design/environment.md) | no | |
| resolutionSummary | string | no | |
| createdAt | datetime | yes | |
| resolvedAt | datetime | no | |

## 4. State (as-is / target)

Stateless — a work item; lifecycle tracked via the `status` field.

## 5. Relationships (semantic references)

- **Refers to:** [Issue](../analysis/issue.md), [Risk](../analysis/risk.md), [Static Analysis Finding](../development/static-analysis-finding.md), [Change Request](../analysis/change-request.md), [Pull Request](../development/pull-request.md), [Test Run](../testing/test-run.md), [Deployment Execution](../rollout/deployment-execution.md), [Component](../design/component.md), [Environment](../design/environment.md), [Role](../analysis/role.md), [Stakeholder](../analysis/stakeholder.md).
- **Referred by:** [Monitoring Alert](monitoring-alert.md) (raisesTicket), [Vulnerability Finding](vulnerability-finding.md) (raisesTicket), [Maintenance Log](maintenance-log.md) (resolvesTicket), analysis [Issue](../analysis/issue.md) (raisedTicket via incidentFacet).

## 6. Lifecycle / status

new → triaged → in-progress → resolved → closed. May be reopened (reopened → in-progress). SLA clocks the response + resolution targets.

## 7. Template coverage

- User-listed maintenance activities: continuous monitoring → incident tickets; vulnerability scanning → vulnerability-remediation tickets; maintenance activity documentation → tickets resolved by [Maintenance Log](maintenance-log.md).
- A future `templates/maintenance/*.md` ticket-management section.

## 8. Non-overlap note

The problem belongs to analysis [Issue](../analysis/issue.md); the risk to [Risk](../analysis/risk.md); the change to [Change Request](../analysis/change-request.md); the fix to development [Pull Request](../development/pull-request.md); the test to testing [Test Run](../testing/test-run.md); the deployment to rollout [Deployment Execution](../rollout/deployment-execution.md). The ticket is the operational wrapper that links them with SLA and assignment.
