# Software Project Risk Profile

> **Template Version:** 1.0  \
> **Last Updated:** <!-- date -->  \
> **Document Status:** <!-- Draft | Under Review | Approved | Baselined -->

---

## Metadata

| Field | Value |
|------|-------|
| **Project Name** | <!-- project name --> |
| **Project Type** | <!-- Green Field | Brown Field | Software Modernization --> |
| **Sponsor** | <!-- sponsoring stakeholder or department --> |
| **Product Owner** | <!-- product owner name --> |
| **Project Manager** | <!-- project manager name --> |
| **Technical Lead** | <!-- technical lead name --> |
| **Security Lead** | <!-- security lead name --> |
| **QA / Test Lead** | <!-- QA lead name --> |
| **Author(s)** | <!-- author name(s) --> |
| **Reviewer(s)** | <!-- reviewer name(s) --> |
| **Date Created** | <!-- creation date --> |
| **Date Revised** | <!-- revision date --> |
| **Classification** | <!-- Public | Internal | Confidential --> |
| **Baseline Version** | <!-- version number once approved --> |
| **Related Documents** | <!-- viability study / business case / project plan / scope / SRS / architecture --> |

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Purpose, Scope, and Approach](#2-purpose-scope-and-approach)
3. [Risk Scales, Taxonomy, and Scoring](#3-risk-scales-taxonomy-and-scoring)
4. [Risk Profile Overview](#4-risk-profile-overview)
5. [Top Risks (Portfolio View)](#5-top-risks-portfolio-view)
6. [Risk Register](#6-risk-register)
7. [Testing and Quality Risk Profile](#7-testing-and-quality-risk-profile)
8. [Security, Privacy, and Compliance Risks](#8-security-privacy-and-compliance-risks)
9. [Delivery, Schedule, and Budget Risks](#9-delivery-schedule-and-budget-risks)
10. [Technology and Architecture Risks](#10-technology-and-architecture-risks)
11. [Operational and Reliability Risks](#11-operational-and-reliability-risks)
12. [Dependency and Vendor Risks](#12-dependency-and-vendor-risks)
13. [Mitigation Plan and Risk Treatment Roadmap](#13-mitigation-plan-and-risk-treatment-roadmap)
14. [Monitoring, Reporting, and Governance](#14-monitoring-reporting-and-governance)
15. [Acceptance, Sign-off, and Residual Risk](#15-acceptance-sign-off-and-residual-risk)
16. [Appendices](#16-appendices)

---

## 1. Executive Summary

<!--
Provide a concise, decision-maker friendly summary. Write this section last.

Expected content:
- Overall risk posture (Low / Medium / High) with rationale.
- Top 3-5 risks that threaten objectives.
- Whether risk is within appetite and what conditions must be met.
- The next 30/60/90-day risk-reduction plan.
- Go/No-Go implications for major milestones (MVP, go-live, cutover).

Keep this section to 1 page maximum.
-->

| Field | Summary |
|------|---------|
| **Overall Risk Posture** | <!-- Low / Medium / High --> |
| **Primary Drivers** | <!-- 2-4 bullets --> |
| **Top Risks** | <!-- R-IDs and short titles --> |
| **Within Risk Appetite?** | <!-- Yes / No / Conditional --> |
| **Conditions / Prerequisites** | <!-- what must be true to proceed safely --> |
| **Upcoming Gate Decisions** | <!-- milestone + decision + date --> |

---

## 2. Purpose, Scope, and Approach

### 2.1 Purpose

<!--
Define why this risk profile exists.

Examples:
- Establish a shared view of project risks across delivery, quality, security, and operations.
- Provide a single authoritative risk register and treatment plan.
- Support stage-gate decisions and executive approvals.
-->

### 2.2 Scope

<!--
Define what is included and excluded.

Include:
- Risks across the full lifecycle: discovery, build, test, deploy, operate, transition/migration.
- Product risks (customer impact), project risks (schedule/budget), and operational risks.

Explicitly state exclusions (e.g., enterprise risks handled elsewhere).
-->

| In Scope | Out of Scope |
|----------|--------------|
| <!-- item --> | <!-- item --> |

### 2.3 Method and Cadence

<!--
Describe how risks were identified and how the profile will be maintained.

Expected content:
- Identification sources (workshops, architecture review, threat model, test strategy, incident history).
- Review frequency (e.g., weekly team review; monthly steering review).
- Tooling (e.g., Jira, Confluence, Excel) and where the canonical register lives.
-->

| Attribute | Value |
|----------|-------|
| **Risk Review Cadence (Team)** | <!-- e.g., weekly --> |
| **Risk Review Cadence (Governance)** | <!-- e.g., monthly --> |
| **Risk Register System of Record** | <!-- link/location --> |
| **Risk Owners Assigned?** | <!-- Yes / No --> |

---

## 3. Risk Scales, Taxonomy, and Scoring

### 3.1 Risk Categories (Taxonomy)

<!--
Use a stable taxonomy so risks can be grouped and reported.
Add/remove categories only if necessary.
-->

| Category | Description |
|----------|-------------|
| **Product / Business** | Value realization, adoption, customer impact, reputational risk |
| **Delivery / Schedule** | Timeline risk, scope volatility, planning uncertainty |
| **Budget / Financial** | Cost overruns, funding gaps, forecast accuracy |
| **Quality / Testing** | Defect escape, test coverage gaps, non-functional validation |
| **Security / Privacy / Compliance** | Threats, vulnerabilities, regulatory exposure |
| **Technology / Architecture** | Design flaws, scalability, performance, maintainability |
| **Operations / Reliability** | Availability, incident risk, observability, supportability |
| **Data / Migration** | Data integrity, cutover, rollback, reconciliation |
| **Dependency / Vendor** | Third-party services, partner delivery, contract risks |
| **People / Organization** | Skills gaps, key-person risk, change resistance |

### 3.2 Likelihood Scale

| Likelihood | Score | Definition |
|------------|------:|------------|
| Very Low | 1 | <!-- unlikely to occur --> |
| Low | 2 | <!-- could occur but unlikely --> |
| Medium | 3 | <!-- likely to occur --> |
| High | 4 | <!-- more likely than not --> |
| Very High | 5 | <!-- almost certain --> |

### 3.3 Impact Scale

<!--
Impact should cover multiple dimensions. Define what "Major" means for your org.
-->

| Impact | Score | Definition (Examples) |
|--------|------:|------------------------|
| Negligible | 1 | <!-- minimal effect; within sprint slack --> |
| Minor | 2 | <!-- manageable; within team control --> |
| Moderate | 3 | <!-- requires management action; may affect milestone --> |
| Major | 4 | <!-- threatens objectives; needs escalation --> |
| Catastrophic | 5 | <!-- severe business impact; may halt launch --> |

### 3.4 Risk Score and RAG Thresholds

<!--
Define how you compute and interpret risk score.
Typical: Risk Score = Likelihood x Impact (1..25).
-->

| Band | Score Range | Meaning | Default Action |
|------|------------:|---------|----------------|
| 🟢 Green | <!-- 1-6 --> | Acceptable | Track; review on cadence |
| 🟡 Amber | <!-- 7-12 --> | Needs mitigation | Add actions and due dates |
| 🔴 Red | <!-- 13-25 --> | Critical | Escalate; define gate criteria |

---

## 4. Risk Profile Overview

### 4.1 Current Snapshot

| Metric | Value |
|--------|-------|
| Total Risks | <!-- count --> |
| Open Risks | <!-- count --> |
| Closed Risks | <!-- count --> |
| 🔴 Red | <!-- count --> |
| 🟡 Amber | <!-- count --> |
| 🟢 Green | <!-- count --> |
| Risks Trending Up (last period) | <!-- count --> |
| Risks Trending Down (last period) | <!-- count --> |

### 4.2 Heat Map (Tabular)

<!--
List risk IDs in the cells.
Keep to top risks; do not try to include everything.
-->

| Likelihood \ Impact | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| 5 | | | | | |
| 4 | | | | | |
| 3 | | | | | |
| 2 | | | | | |
| 1 | | | | | |

### 4.3 Risk Appetite Alignment

<!--
Record agreed thresholds (budget variance, downtime, security severity, etc.).
-->

| Dimension | Appetite / Tolerance | Current Exposure | Within Tolerance? |
|----------|------------------------|------------------|-------------------|
| Cost Overrun | <!-- e.g., <= +15% --> | | |
| Schedule Delay | <!-- e.g., <= 6 weeks --> | | |
| Availability (SLO) | <!-- e.g., 99.9% --> | | |
| Security | <!-- e.g., 0 critical vulns at launch --> | | |
| Data Loss | <!-- e.g., 0 tolerated --> | | |
| Regulatory | <!-- e.g., audit pass required --> | | |

---

## 5. Top Risks (Portfolio View)

<!--
Provide the top risks as a short list for decision makers.
This is not the full register.
-->

| Rank | Risk ID | Risk Title | Category | Score | Owner | Mitigation Summary | Target Date |
|-----:|---------|------------|----------|------:|-------|--------------------|------------|
| 1 | R-001 | | | | | | |
| 2 | R-002 | | | | | | |
| 3 | R-003 | | | | | | |
| 4 | R-004 | | | | | | |
| 5 | R-005 | | | | | | |

---

## 6. Risk Register

<!--
This is the authoritative list.

Guidance:
- Keep risk statements specific and testable.
- Include a trigger and early warning indicators.
- Residual score is required for all non-green items.
-->

| Risk ID | Risk Statement | Category | Likelihood | Impact | Score | Trigger / Early Warning | Treatment (Avoid/Reduce/Transfer/Accept) | Mitigation Actions (Summary) | Owner | Due Date | Residual L | Residual I | Residual Score | Status |
|---------|----------------|----------|-----------:|-------:|------:|--------------------------|------------------------------------------|-----------------------------|-------|---------|-----------:|-----------:|--------------:|--------|
| R-001 | <!-- If X happens, then Y impact --> | | | | | | | | | | | | | <!-- Open / Mitigating / Occurred / Closed --> |

---

## 7. Testing and Quality Risk Profile

<!--
Focus on risks that can cause defect escape, poor user experience, and non-functional failures.
Tie mitigation to measurable test artifacts (test suites, coverage, gates).
-->

### 7.1 Quality Goals and Gates

| Quality Dimension | Baseline | Target | Gate / Enforcement Point |
|------------------|----------|--------|---------------------------|
| Unit Test Coverage | | | <!-- e.g., CI merge gate --> |
| Integration Coverage | | | |
| E2E Coverage | | | |
| Defect Escape Rate | | | |
| Performance (p95/p99) | | | <!-- e.g., release gate --> |
| Accessibility | | | |
| Security Findings | | | |

### 7.2 Test Strategy Risk Checklist

| Risk Area | Question | Answer | Evidence / Link | Risk ID |
|----------|----------|--------|-----------------|--------|
| Test Pyramid | Are we over-relying on E2E tests or manual testing? | <!-- Yes/No/Partial --> | | |
| Regression | Is there a regression suite for critical user flows? | | | |
| Environments | Are test environments production-like (data, config, scale)? | | | |
| Test Data | Do we have reliable, compliant test data provisioning? | | | |
| Flakiness | Is test flakiness controlled with budgets and quarantine rules? | | | |
| Observability | Do tests validate logs/metrics/traces and alerting? | | | |
| Release Safety | Is there a validated rollback plan and smoke test for rollback? | | | |

### 7.3 Key Testing Risks (Detail)

| Risk ID | Risk Title | Type | Affected Areas | Score | Mitigation Summary | Gate / Exit Criteria |
|---------|------------|------|----------------|------:|--------------------|----------------------|
| <!-- e.g., R-012 --> | | <!-- functional / regression / NFR --> | | | | |

---

## 8. Security, Privacy, and Compliance Risks

<!--
Use threat modeling and security testing outputs to populate this section.
Explicitly track launch-blockers (e.g., critical vulnerabilities, missing privacy controls).
-->

### 8.1 Security Posture Summary

| Area | Requirement | Current Status | Gap | Risk ID |
|------|-------------|----------------|-----|--------|
| Authentication / Authorization | <!-- SSO/MFA/RBAC --> | | | |
| Secrets Management | | | | |
| Encryption | <!-- at rest / in transit --> | | | |
| Logging / Audit | | | | |
| Vulnerability Management | <!-- SAST/DAST/Dependencies --> | | | | |
| Security Testing | <!-- pen test / scans --> | | | | |

### 8.2 Privacy and Data Protection

| Topic | Requirement | Evidence | Risk ID |
|------|-------------|----------|--------|
| Data Classification | | | |
| Data Minimization | | | |
| Consent / Lawful Basis | | | |
| Retention / Deletion | | | |
| Data Residency | | | |
| DPIA / PIA (if applicable) | | | |

### 8.3 Compliance and Audit Readiness

| Standard / Regulation | Applicability | Key Controls | Status | Risk ID |
|-----------------------|---------------|-------------|--------|--------|
| <!-- e.g., GDPR --> | <!-- Yes/No --> | | | |

---

## 9. Delivery, Schedule, and Budget Risks

### 9.1 Delivery Risk Drivers

| Driver | Description | Leading Indicator | Risk ID |
|--------|-------------|------------------|--------|
| Scope Volatility | | <!-- e.g., backlog churn rate --> | |
| Estimation Uncertainty | | <!-- e.g., variance vs plan --> | |
| Resource Constraints | | <!-- e.g., staffing gaps --> | |
| Parallel Run Complexity 🟤🔵 | | | |

### 9.2 Budget and Cost Risk

| Cost Area | Assumption | Sensitivity | Mitigation | Risk ID |
|----------|------------|-------------|------------|--------|
| Staffing | | | | |
| Cloud / Infrastructure | | | | |
| Licenses / Vendors | | | | |
| Dual-Running 🟤🔵 | | | | |

### 9.3 Schedule Gate Risks

| Milestone | Date | Key Risks | Entry Criteria | Exit Criteria | Go/No-Go Owner |
|----------|------|-----------|----------------|--------------|----------------|
| <!-- MVP --> | | | | | |
| <!-- Go-Live --> | | | | | |
| <!-- Cutover 🟤🔵 --> | | | | | |

---

## 10. Technology and Architecture Risks

<!--
Capture risks from architecture reviews and ADRs.
Focus on scalability, performance, resiliency, maintainability, and operability.
-->

### 10.1 Key Architectural Risks

| Risk ID | Component / Area | Risk Statement | Score | Mitigation | Validation Method |
|---------|------------------|----------------|------:|------------|-------------------|
| | | | | | |

### 10.2 Technical Debt and Complexity

| Area | Debt Item / Complexity Driver | Impact | Remediation Plan | Owner | Risk ID |
|------|-------------------------------|--------|------------------|-------|--------|
| | | | | | |

---

## 11. Operational and Reliability Risks

### 11.1 Operational Readiness

| Capability | Requirement | Status | Gap | Risk ID |
|-----------|-------------|--------|-----|--------|
| Monitoring / Alerting | | | | |
| On-call / Incident Response | | | | |
| Runbooks | | | | |
| Backup / Restore | | | | |
| DR (RPO/RTO) | | | | |
| Capacity Management | | | | |

### 11.2 SLOs and Error Budgets

| SLO | Target | Measurement Source | Current | Risk ID |
|-----|--------|--------------------|---------|--------|
| Availability | | | | |
| Latency (p95/p99) | | | | |
| Error Rate | | | | |

---

## 12. Dependency and Vendor Risks

### 12.1 External Dependencies

| Dependency | Owner | Criticality | Risk | Mitigation | Risk ID |
|-----------|-------|-------------|------|------------|--------|
| <!-- system/API/vendor --> | | <!-- High/Med/Low --> | | | |

### 12.2 Vendor Lock-in and Exit Strategy

| Vendor / Service | Lock-in Risk | Exit Strategy | Exit Cost | Risk ID |
|------------------|--------------|--------------|----------|--------|
| | | | | |

---

## 13. Mitigation Plan and Risk Treatment Roadmap

<!--
Translate mitigations into an actionable roadmap with owners and dates.
Prefer mitigations that reduce likelihood early and validate impact with gates.
-->

### 13.1 Risk Treatment Roadmap (30/60/90 days)

| Timebox | Focus | Deliverables | Risks Addressed (IDs) | Owner |
|--------|-------|--------------|------------------------|-------|
| 0-30 days | | | | |
| 31-60 days | | | | |
| 61-90 days | | | | |

### 13.2 Mitigation Actions (Detailed)

| Action ID | Action | Linked Risk ID(s) | Priority | Owner | Due Date | Success Metric | Status |
|----------|--------|-------------------|----------|-------|---------|----------------|--------|
| A-001 | | | <!-- High/Med/Low --> | | | | <!-- Not started / In progress / Done --> |

### 13.3 Contingency and Fallbacks

<!--
Document what you will do if mitigation fails.
Examples: rollback plan, feature flag off, reduce scope, extend dual-running.
-->

| Scenario | Trigger | Fallback Plan | Cost / Impact | Decision Owner |
|----------|---------|---------------|---------------|----------------|
| | | | | |

---

## 14. Monitoring, Reporting, and Governance

### 14.1 Review Cadence and Forums

| Forum | Frequency | Participants | Outputs |
|------|-----------|--------------|---------|
| Team Risk Review | | | <!-- updated register, action updates --> |
| Quality Review | | | |
| Security Review | | | |
| Steering Committee | | | <!-- top risks, escalations, decisions --> |
| Release / Cutover War Room 🟤🔵 | | | |

### 14.2 Escalation Criteria

| Trigger | Threshold | Escalate To | Response Time |
|---------|-----------|-------------|---------------|
| Risk Score | <!-- e.g., >= 13 --> | | |
| Budget variance | | | |
| Schedule variance | | | |
| Security findings | <!-- e.g., any critical --> | | |
| Incident rate | | | |

### 14.3 Reporting Template (RAG)

| Area | RAG | Notes | Linked Risk IDs |
|------|-----|------|-----------------|
| Delivery | 🟢/🟡/🔴 | | |
| Quality | 🟢/🟡/🔴 | | |
| Security | 🟢/🟡/🔴 | | |
| Operations | 🟢/🟡/🔴 | | |
| Dependencies | 🟢/🟡/🔴 | | |

---

## 15. Acceptance, Sign-off, and Residual Risk

### 15.1 Residual Risk Summary

<!--
List residual red/amber risks and why proceeding is acceptable (or not).
Include explicit acceptance rationale and compensating controls.
-->

| Risk ID | Residual Score | Acceptance Rationale | Compensating Controls | Accepted By | Date |
|---------|---------------:|----------------------|-----------------------|------------|------|
| | | | | | |

### 15.2 Launch / Cutover Risk Acceptance Checklist

| Area | Requirement | Met? | Evidence | Owner |
|------|-------------|------|----------|-------|
| Testing | Release regression suite passed | <!-- Yes/No --> | | |
| Testing | Performance tests meet thresholds | | | |
| Security | No critical vulnerabilities | | | |
| Security | Pen test findings addressed/accepted | | | |
| Operations | Monitoring and alerting live | | | |
| Operations | Runbooks + on-call ready | | | |
| Data 🟤🔵 | Data migration validated | | | |
| Data 🟤🔵 | Rollback tested | | | |

### 15.3 Approvals

| Stakeholder | Role | Approval | Date | Notes |
|------------|------|----------|------|------|
| | Sponsor | ✅ / ❌ | | |
| | Product Owner | ✅ / ❌ | | |
| | Project Manager | ✅ / ❌ | | |
| | Technical Lead | ✅ / ❌ | | |
| | Security Lead | ✅ / ❌ | | |
| | QA / Test Lead | ✅ / ❌ | | |

---

## 16. Appendices

### Appendix A: Definitions

| Term | Definition |
|------|-----------|
| Risk | <!-- uncertain event that affects objectives --> |
| Issue | <!-- realized risk requiring action --> |
| Residual Risk | <!-- remaining risk after mitigation --> |
| Risk Owner | <!-- accountable person for managing the risk --> |

### Appendix B: Risk Scoring Notes

<!--
Document any project-specific scoring rules.
Examples:
- Security impact scoring ties to CVSS/severity.
- Availability impact ties to SLO error budget burn.
- Financial impact scoring ties to cost thresholds.
-->

### Appendix C: Risk Identification Checklist

| Area | Prompt | Completed By | Date |
|------|--------|--------------|------|
| Architecture | Architecture review performed and risks captured | | |
| Security | Threat model performed and risks captured | | |
| Testing | Test strategy reviewed and risks captured | | |
| Data 🟤🔵 | Migration rehearsal performed | | |
| Ops | Operational readiness review performed | | |

---

## Document History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | <!-- date --> | <!-- author --> | Initial template |

---

## Usage Guide

| Icon | Meaning | When Applicable |
|------|---------|-----------------|
| 🟢 | Green Field | Building new software from scratch |
| 🟤 | Brown Field | Extending or refactoring existing software |
| 🔵 | Software Modernization | Migrating or re-architecting legacy systems |
| ⚪ | All Types | Applicable to every project type |

**How to use this template:**
1. Complete Sections 2 and 3 first (scope, scoring, and governance).
2. Populate the risk register in Section 6 and keep it as the single source of truth.
3. Use Sections 7-12 to ensure coverage across quality, security, operations, and dependencies.
4. For any 🔴 risk, define explicit gate criteria and a contingency plan.
5. Before major releases or cutovers, complete Section 15.2 and obtain approvals in Section 15.3.
