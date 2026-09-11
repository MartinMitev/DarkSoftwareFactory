# Monitoring Alert

> **Slug:** `monitoring-alert` | **View:** Monitoring View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a signal raised by a monitoring system (error rate, latency, uptime, resource saturation, log anomaly) against a running [Environment](../design/environment.md), with severity, source metric, correlation to a [Ticket](ticket.md), and auto-remediation status.
- **Purpose / when used:** the raw operational signal from runtime monitoring; the runtime counterpart of the development [Static Analysis Finding](../development/static-analysis-finding.md) (which is a pre-deployment tool output).

## 2. Semantics (crisp)

`monitoring-alert` is the **raw operational signal** from monitoring: a source (the monitoring tool / metric), a metric (error rate / p95 latency / uptime / CPU / memory / disk / queue depth / log anomaly), a threshold breach, a severity (critical / warning / info), the design [Environment](../design/environment.md) and design [Infrastructure Resource](../design/infrastructure-resource.md) it relates to, the design [Component](../design/component.md) / rollout [Runtime Configuration](../rollout/runtime-configuration.md) (monitoring config) it was raised against, and a status (firing / acknowledged / resolved / suppressed). When triaged it **raises a [Ticket](ticket.md)** (typically an incident) — it is **not** the ticket and **not** the issue (→ analysis [Issue](../analysis/issue.md)). Auto-remediation (auto-scaling, auto-restart) is captured as a `remediationAction` field; if auto-remediation succeeds the alert resolves without a ticket. It is the **runtime counterpart** of the development [Static Analysis Finding](../development/static-analysis-finding.md) (pre-deployment SAST code analysis) — that is build-time source analysis; this is runtime metric monitoring of a deployed system. It is **not** a static-analysis finding (→ [Static Analysis Finding](../development/static-analysis-finding.md)), **not** a test result (→ testing [Test Result](../testing/test-result.md) — that is a test verdict; this is a production signal), and **not** a ticket (→ [Ticket](ticket.md) — it *raises* one on triage).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. ALERT-001 |
| source | string | yes | tool / metric source |
| metric | string | yes | error rate / p95 latency / uptime / CPU / memory / disk / queue / log-anomaly |
| threshold | string | yes | the breached threshold |
| severity | enum (critical / warning / info) | yes | |
| environment | ref → [Environment](../design/environment.md) | yes | |
| infrastructureResource | ref → [Infrastructure Resource](../design/infrastructure-resource.md) | no | |
| component | ref → [Component](../design/component.md) | no | |
| runtimeConfiguration | ref → [Runtime Configuration](../rollout/runtime-configuration.md) | no | the monitoring config that defined the alert rule |
| status | enum (firing / acknowledged / resolved / suppressed) | yes | |
| raisesTicket | ref → [Ticket](ticket.md) | no | set on triage |
| remediationAction | string | no | auto-scaling / auto-restart / none |
| firedAt | datetime | yes | |
| resolvedAt | datetime | no | |

## 4. State (as-is / target)

Stateless — a signal; lifecycle tracked via the `status` field.

## 5. Relationships (semantic references)

- **Refers to:** [Environment](../design/environment.md), [Infrastructure Resource](../design/infrastructure-resource.md), [Component](../design/component.md), [Runtime Configuration](../rollout/runtime-configuration.md), [Ticket](ticket.md).
- **Referred by:** analysis [Issue](../analysis/issue.md) (detectedByAlert via incidentFacet).

## 6. Lifecycle / status

firing → acknowledged → resolved / suppressed. Auto-remediation may resolve without acknowledgement. Suppressed alerts retain a record with rationale.

## 7. Template coverage

- User-listed "continuous monitoring of the application for possible issues".
- A future `templates/maintenance/*.md` monitoring / alerting section.

## 8. Non-overlap note

The pre-deployment code finding belongs to development [Static Analysis Finding](../development/static-analysis-finding.md); the test verdict belongs to testing [Test Result](../testing/test-result.md); the operational wrapper belongs to [Ticket](ticket.md); the occurred problem belongs to analysis [Issue](../analysis/issue.md). The monitoring alert is the runtime metric signal.
