# Availability / Live Test Cases

> **Template Version:** 1.0  \
> **Last Updated:** <!-- date -->  \
> **Document Status:** <!-- Draft | Under Review | Approved | Baselined -->

---

## Metadata

| Field | Value |
|------|-------|
| **Project Name** | <!-- project name --> |
| **System / Application** | <!-- system name --> |
| **Release / Change ID** | <!-- release name, CAB/change ID --> |
| **Production Environment** | <!-- prod name/region --> |
| **Author(s)** | <!-- name(s) --> |
| **Reviewer(s)** | <!-- name(s) --> |
| **QA / Test Lead** | <!-- name --> |
| **SRE / Ops Lead** | <!-- name --> |
| **Incident Commander** | <!-- name --> |
| **Date Created** | <!-- date --> |
| **Date Revised** | <!-- date --> |
| **Classification** | <!-- Public | Internal | Confidential --> |

---

## Table of Contents

1. [Purpose and Safety Rules](#1-purpose-and-safety-rules)
2. [Prerequisites](#2-prerequisites)
3. [Live Test Case Format](#3-live-test-case-format)
4. [Smoke and Sanity Live Tests](#4-smoke-and-sanity-live-tests)
5. [Availability and Monitoring Live Tests](#5-availability-and-monitoring-live-tests)
6. [Operational Readiness and Runbook Tests](#6-operational-readiness-and-runbook-tests)
7. [Rollback and Recovery Live Tests](#7-rollback-and-recovery-live-tests)
8. [Quality Gates and Exit Criteria](#8-quality-gates-and-exit-criteria)
9. [Evidence and Reporting](#9-evidence-and-reporting)
10. [Appendices](#10-appendices)

---

## 1. Purpose and Safety Rules

<!--
Goal:
- Validate availability and live operability in the target environment.
- Confirm monitoring, alerting, and runbooks work in real conditions.

Safety rules:
- Live tests must not violate privacy/security policies.
- Use least-privilege test accounts.
- Do not run destructive tests unless explicitly approved.
- Maintain a rollback decision path and stop conditions.
-->

| Safety Constraint | Description |
|------------------|-------------|
| Stop Conditions | <!-- e.g., error rate > X%, customer impact observed --> |
| Approved Test Windows | <!-- maintenance window --> |
| Data Restrictions | <!-- no PII exposure, no real payments --> |
| Stakeholders On Call | <!-- roles required during execution --> |

---

## 2. Prerequisites

| PR-ID | Prerequisite | Owner | Status | Evidence |
|------|--------------|-------|--------|----------|
| LIVE-PR-001 | Change approved (CAB) | | | |
| LIVE-PR-002 | Rollback plan validated | | | |
| LIVE-PR-003 | Monitoring dashboards ready | | | |
| LIVE-PR-004 | Alerts configured and routed | | | |
| LIVE-PR-005 | Test accounts and credentials ready | | | |
| LIVE-PR-006 | Runbooks accessible to on-call | | | |

---

## 3. Live Test Case Format

| Field | Value |
|------|-------|
| **Test Case ID** | <!-- TC-LIVE-XXX --> |
| **Category** | <!-- smoke / monitoring / runbook / rollback --> |
| **Objective** | |
| **Preconditions** | |
| **Steps** | <!-- numbered --> |
| **Expected Results** | |
| **Observed Results** | |
| **Pass/Fail** | <!-- Pass/Fail --> |
| **Owner** | |
| **Timestamp** | <!-- execution time --> |
| **Evidence** | <!-- dashboard link, logs, screenshots --> |

---

## 4. Smoke and Sanity Live Tests

<!--
Minimal set of tests that validate the system is basically working.
Keep this small and stable.
-->

| Test Case ID | Test | Surface | Expected Result | Evidence |
|-------------|------|---------|-----------------|----------|
| TC-LIVE-001 | Health check endpoints | API | 200 + correct payload | |
| TC-LIVE-002 | Login with test account | UI | successful auth, correct role | |
| TC-LIVE-003 | Critical user journey (read-only) | UI/API | completes without errors | |
| TC-LIVE-004 | Background job heartbeat | Jobs | job runs and reports success | |

---

## 5. Availability and Monitoring Live Tests

<!--
Validate monitoring, alerting, and SLO measurement.
These tests confirm you can detect and respond to issues.
-->

| Test Case ID | Test | Expected Result | Evidence |
|-------------|------|-----------------|----------|
| TC-LIVE-010 | Dashboards show key signals | latency/error/traffic visible | |
| TC-LIVE-011 | Synthetic checks running | checks succeed and report | |
| TC-LIVE-012 | Alert routing validation | alert reaches correct on-call channel | |
| TC-LIVE-013 | Log correlation works | request ID traces across services | |

---

## 6. Operational Readiness and Runbook Tests

<!--
Exercise runbooks in a safe manner.
Examples: scale up/down, restart service, rotate credentials (if permitted).
-->

| Test Case ID | Runbook / Procedure | Expected Result | Evidence |
|-------------|----------------------|-----------------|----------|
| TC-LIVE-020 | Restart service procedure | service returns healthy within target | |
| TC-LIVE-021 | Scale-out procedure | latency stable; capacity increases | |
| TC-LIVE-022 | Incident triage drill | timelines and roles validated | |

---

## 7. Rollback and Recovery Live Tests

<!--
Validate rollback in a controlled environment (preferred) or production only when explicitly approved.
If rollback in production is not allowed, validate the decision process and tooling.
-->

| Test Case ID | Test | Expected Result | Evidence |
|-------------|------|-----------------|----------|
| TC-LIVE-030 | Rollback decision drill | criteria and decision path clear | |
| TC-LIVE-031 | Rollback tooling dry run | commands and permissions verified | |
| TC-LIVE-032 | Restore from backup (non-prod) | recovery meets RTO/RPO | |

---

## 8. Quality Gates and Exit Criteria

| Gate | Criteria | Evidence | Owner | Status |
|------|----------|----------|-------|--------|
| Live Readiness Gate | prerequisites satisfied | checklist | | |
| Post-Deploy Gate | smoke tests pass | execution log | | |
| Monitoring Gate | signals and alerts validated | dashboard links | | |

---

## 9. Evidence and Reporting

| Artifact | Location / Link | Produced By | Date |
|----------|------------------|-------------|------|
| Live test execution log | | | |
| Dashboard snapshots | | | |
| Alert routing evidence | | | |
| Incident drill notes | | | |
| Approval record | | | |

---

## 10. Appendices

### Appendix A: Key Dashboards and Links

| Purpose | Link |
|---------|------|
| SLO dashboard | |
| Error budget | |
| On-call schedule | |
| Runbooks index | |
