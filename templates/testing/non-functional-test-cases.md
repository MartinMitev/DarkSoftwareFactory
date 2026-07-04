# Non-Functional Test Cases

> **Template Version:** 1.0  \
> **Last Updated:** <!-- date -->  \
> **Document Status:** <!-- Draft | Under Review | Approved | Baselined -->

---

## Metadata

| Field | Value |
|------|-------|
| **Project Name** | <!-- project name --> |
| **System / Application** | <!-- system name --> |
| **Release / Milestone** | <!-- e.g., MVP, R1 --> |
| **Author(s)** | <!-- name(s) --> |
| **Reviewer(s)** | <!-- name(s) --> |
| **QA / Test Lead** | <!-- name --> |
| **Security Lead** | <!-- name --> |
| **SRE / Ops Lead** | <!-- name --> |
| **Date Created** | <!-- date --> |
| **Date Revised** | <!-- date --> |
| **Classification** | <!-- Public | Internal | Confidential --> |
| **Related Requirements** | <!-- NFR-XXX, policies --> |

---

## Table of Contents

1. [Purpose and Scope](#1-purpose-and-scope)
2. [Performance and Stress Tests](#2-performance-and-stress-tests)
3. [Failover and Recovery Tests](#3-failover-and-recovery-tests)
4. [Security Tests](#4-security-tests)
5. [Quality Gates and Exit Criteria](#5-quality-gates-and-exit-criteria)
6. [Evidence and Reporting](#6-evidence-and-reporting)
7. [Appendices](#7-appendices)

---

## 1. Purpose and Scope

<!--
Goal:
- Validate the system meets non-functional requirements (performance, resiliency, security).

Non-functional test cases must reference measurable targets (SLOs, thresholds, severity rules).
-->

| In Scope | Out of Scope |
|----------|--------------|
| <!-- perf/stress, recovery, security --> | <!-- e.g., functional correctness --> |

---

## 2. Performance and Stress Tests

<!--
Include load, stress, soak, and scalability tests.
Define workload model and success criteria (p95/p99, error rate, saturation signals).
-->

### 2.1 Performance Test Case Template

| Field | Value |
|------|-------|
| **Test Case ID** | <!-- TC-PERF-XXX --> |
| **Type** | <!-- load / stress / soak / spike --> |
| **Target** | <!-- endpoint/service/flow --> |
| **Workload Model** | <!-- users/RPS, ramp, duration --> |
| **Data Model** | <!-- dataset size, distribution --> |
| **Environment** | <!-- perf env details --> |
| **Tooling** | |
| **Success Criteria** | <!-- p95/p99, error rate, resource limits --> |
| **Steps** | |
| **Expected Results** | |
| **Observability Required** | <!-- dashboards, traces --> |
| **Evidence** | <!-- report links --> |

### 2.2 Performance Test Case List

| Test Case ID | Type | Target | Priority | Status |
|-------------|------|--------|----------|--------|
| TC-PERF-001 | | | | |

---

## 3. Failover and Recovery Tests

<!--
Validate resilience patterns and recovery objectives (RTO/RPO).
Include component failure, zone failure, dependency failure, and degraded-mode operation.
-->

### 3.1 Failover/Recovery Test Case Template

| Field | Value |
|------|-------|
| **Test Case ID** | <!-- TC-REC-XXX --> |
| **Failure Mode** | <!-- instance/node/zone/db/dependency --> |
| **Injection Method** | <!-- kill, block, chaos tool, config --> |
| **Expected System Behavior** | <!-- failover, retry, degrade --> |
| **RTO / RPO Targets** | |
| **Customer Impact Expectation** | <!-- downtime/error budget --> |
| **Rollback / Restore Steps** | |
| **Observability Checks** | <!-- alerts, logs, dashboards --> |
| **Evidence** | |

### 3.2 Failover/Recovery Test Case List

| Test Case ID | Failure Mode | Target | Priority | Status |
|-------------|--------------|--------|----------|--------|
| TC-REC-001 | | | | |

---

## 4. Security Tests

<!--
Include automated and manual security testing.
Track vulnerability thresholds and acceptance rules.
-->

### 4.1 Security Test Case Template

| Field | Value |
|------|-------|
| **Test Case ID** | <!-- TC-SEC-XXX --> |
| **Category** | <!-- SAST / DAST / dependency / config / pen-test --> |
| **Target** | <!-- repo/service/endpoints --> |
| **Threat / CWE / Control** | <!-- what is being validated --> |
| **Steps** | |
| **Expected Results** | <!-- no critical/high or accepted --> |
| **Evidence** | <!-- scan report, ticket --> |
| **Owner** | |
| **Status** | |

### 4.2 Security Test Case List

| Test Case ID | Category | Target | Blocking? | Status |
|-------------|----------|--------|-----------|--------|
| TC-SEC-001 | Dependency Scan | | Yes | |
| TC-SEC-002 | DAST | | Yes | |
| TC-SEC-003 | Config Review | | Yes | |
| TC-SEC-004 | Pen Test (if required) | | <!-- Yes/Conditional --> | |

---

## 5. Quality Gates and Exit Criteria

| Gate | Criteria | Evidence | Owner | Status |
|------|----------|----------|-------|--------|
| Performance Gate | Targets met under defined workload | perf reports | | |
| Recovery Gate | RTO/RPO met; alerts correct | recovery report | | |
| Security Gate | No critical; high vulnerabilities triaged | scan reports | | |

---

## 6. Evidence and Reporting

| Artifact | Location / Link | Produced By | Date |
|----------|------------------|-------------|------|
| Performance report | | | |
| Soak test report | | | |
| Failover/recovery report | | | |
| Security scan results | | | |
| Risk acceptance record | | | |

---

## 7. Appendices

### Appendix A: Standard Thresholds

| Metric | Target | Notes |
|--------|--------|------|
| p95 latency | | |
| p99 latency | | |
| Error rate | | |
| Availability | | |
| RTO | | |
| RPO | | |
