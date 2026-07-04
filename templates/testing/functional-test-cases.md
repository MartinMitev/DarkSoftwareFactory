# Functional Test Cases

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
| **Product Owner** | <!-- name --> |
| **Date Created** | <!-- date --> |
| **Date Revised** | <!-- date --> |
| **Classification** | <!-- Public | Internal | Confidential --> |
| **Source Documents** | <!-- project scope / SRS / user stories --> |

---

## Table of Contents

1. [Purpose and Scope](#1-purpose-and-scope)
2. [Feature Tests](#2-feature-tests)
3. [Business Component Tests](#3-business-component-tests)
4. [Business Process Tests](#4-business-process-tests)
5. [Usability Tests](#5-usability-tests)
6. [Coverage and Traceability](#6-coverage-and-traceability)
7. [Quality Gates and Exit Criteria](#7-quality-gates-and-exit-criteria)
8. [Evidence and Reporting](#8-evidence-and-reporting)
9. [Appendices](#9-appendices)

---

## 1. Purpose and Scope

<!--
Goal:
- Validate user-visible behavior and business correctness.

This template covers:
- Feature tests (capability-level)
- Business component tests (domain-focused components/services)
- Business process tests (end-to-end workflows)
- Usability tests (task success, learnability, accessibility-adjacent UX)

Coverage expectation:
- All application features are covered (Functional View).
- Critical flows include negative and boundary cases.
-->

| In Scope | Out of Scope |
|----------|--------------|
| <!-- features and processes --> | <!-- e.g., load testing (belongs to NFR) --> |

---

## 2. Feature Tests

### 2.1 Feature Test Case Template

| Field | Value |
|------|-------|
| **Test Case ID** | <!-- TC-FEAT-XXX --> |
| **Feature ID(s)** | <!-- FEAT-XXX --> |
| **User Story / Requirement Link** | <!-- US-XXX / FR-XXX --> |
| **Persona / Role** | |
| **Scenario** | |
| **Preconditions** | |
| **Test Data** | |
| **Steps** | <!-- numbered --> |
| **Expected Results** | |
| **Negative / Edge Cases** | |
| **Automation** | <!-- Manual/Automated --> |
| **Environment** | <!-- staging/preprod --> |
| **Evidence** | |

### 2.2 Feature Test Case List

| Test Case ID | Feature | Scenario | Priority | Status |
|-------------|---------|----------|----------|--------|
| TC-FEAT-001 | | | <!-- P0/P1/P2 --> | |

---

## 3. Business Component Tests

<!--
Business components are coherent domain areas (e.g., Pricing, Eligibility, Payments, Identity).
These tests validate domain rules and consistency across multiple features.
-->

### 3.1 Business Component Test Case Template

| Field | Value |
|------|-------|
| **Test Case ID** | <!-- TC-BC-XXX --> |
| **Business Component** | |
| **Rules / Policies Covered** | |
| **Scenario** | |
| **Inputs and Variants** | |
| **Expected Outcomes** | |
| **Cross-Feature Impact** | <!-- which features depend on this --> |
| **Automation** | <!-- Manual/Automated --> |
| **Evidence** | |

### 3.2 Business Component Test Case List

| Test Case ID | Component | Scenario | Priority | Status |
|-------------|-----------|----------|----------|--------|
| TC-BC-001 | | | | |

---

## 4. Business Process Tests

<!--
Business process tests validate complete workflows end-to-end.
They should be limited to a small set of "golden paths" plus a curated set of failure paths.
-->

### 4.1 Business Process Scenario Template

| Field | Value |
|------|-------|
| **Scenario ID** | <!-- BP-XXX --> |
| **Process Name** | |
| **Start Trigger** | |
| **End Condition** | |
| **Systems Involved** | |
| **Business Objects** | <!-- BO-XXX --> |
| **Happy Path Steps** | |
| **Failure Paths** | |
| **Key Assertions** | <!-- invariants, events, side effects --> |
| **Evidence** | |

### 4.2 Business Process Test Case Template

| Field | Value |
|------|-------|
| **Test Case ID** | <!-- TC-BP-XXX --> |
| **Scenario ID** | <!-- BP-XXX --> |
| **Persona(s)** | |
| **Preconditions** | |
| **Test Data** | |
| **Steps** | |
| **Expected Results** | |
| **Rollback / Cleanup** | |
| **Automation** | <!-- Manual/Automated --> |
| **Evidence** | |

### 4.3 Business Process Test Case List

| Test Case ID | Process | Scenario | Priority | Status |
|-------------|---------|----------|----------|--------|
| TC-BP-001 | | | | |

---

## 5. Usability Tests

<!--
Usability tests measure whether target users can complete key tasks efficiently and correctly.
They are not broad UX reviews; keep tasks concrete and tied to critical flows.
-->

### 5.1 Usability Session Plan Template

| Field | Value |
|------|-------|
| **Session ID** | <!-- UX-SES-XXX --> |
| **Goal** | |
| **Target Users** | <!-- persona(s) --> |
| **Number of Participants** | |
| **Environment** | <!-- device/browser, build --> |
| **Tasks** | <!-- list task IDs --> |
| **Success Criteria** | <!-- completion rate/time/error rate --> |
| **Data Captured** | <!-- notes, screen recording, survey --> |
| **Ethics/Consent** | <!-- if applicable --> |

### 5.2 Usability Task Template

| Field | Value |
|------|-------|
| **Task ID** | <!-- UX-TASK-XXX --> |
| **Task Description** | |
| **Starting State** | |
| **Completion Criteria** | |
| **Metrics** | <!-- time on task, errors, satisfaction --> |
| **Observed Issues** | |
| **Severity** | <!-- High/Medium/Low --> |
| **Recommendation** | |

---

## 6. Coverage and Traceability

### 6.1 Feature Coverage Matrix

| Feature ID | Feature | Test Case IDs | Coverage Status | Notes |
|-----------|---------|---------------|-----------------|------|
| FEAT-001 | | | <!-- Complete/Partial/Gap --> | |

### 6.2 Story/Requirement Traceability

| Requirement/Story ID | Summary | Feature(s) | Test Case IDs | Coverage Status |
|----------------------|---------|-----------|--------------|-----------------|
| | | | | |

---

## 7. Quality Gates and Exit Criteria

| Gate | Criteria | Evidence | Owner | Status |
|------|----------|----------|-------|--------|
| Functional Gate | All P0/P1 features pass | reports | | |
| Process Gate | All golden paths pass | reports | | |
| Usability Gate | Task success thresholds met (if required) | session report | | |

---

## 8. Evidence and Reporting

| Artifact | Location / Link | Produced By | Date |
|----------|------------------|-------------|------|
| Test execution report | | | |
| Defect list (functional) | | | |
| Usability report | | | |

---

## 9. Appendices

### Appendix A: Standard Personas

| Persona | Description | Key Tasks |
|---------|-------------|----------|
| | | |
