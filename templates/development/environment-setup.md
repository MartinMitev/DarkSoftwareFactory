# Environment Setup Document

> **Template Version:** 1.0  \
> **Last Updated:** <!-- date -->  \
> **Document Status:** <!-- Draft | Under Review | Approved | Baselined -->

---

## Metadata

| Field | Value |
|------|-------|
| **Project Name** | <!-- project name --> |
| **System / Application** | <!-- system name --> |
| **Project Type** | <!-- Green Field | Brown Field | Software Modernization --> |
| **Sponsor** | <!-- sponsor --> |
| **Product Owner** | <!-- PO --> |
| **Project Manager** | <!-- PM --> |
| **Technical Lead** | <!-- tech lead --> |
| **DevOps Lead** | <!-- devops lead --> |
| **Security Lead** | <!-- security lead --> |
| **Author(s)** | <!-- author(s) --> |
| **Reviewer(s)** | <!-- reviewer(s) --> |
| **Date Created** | <!-- date --> |
| **Date Revised** | <!-- date --> |
| **Classification** | <!-- Public | Internal | Confidential --> |
| **Baseline Version** | <!-- once approved --> |
| **Related Documents** | <!-- SRS / architecture / test concept / risk profile / release plan --> |

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Purpose, Scope, and Definitions](#2-purpose-scope-and-definitions)
3. [Project Overview](#3-project-overview)
4. [Stages (Environments)](#4-stages-environments)
5. [Version Control Repositories](#5-version-control-repositories)
6. [Collaboration Platform](#6-collaboration-platform)
7. [CI/CD Pipelines](#7-cicd-pipelines)
8. [Prerequisites and Access Management](#8-prerequisites-and-access-management)
9. [Additional Environment Setup Content](#9-additional-environment-setup-content)
10. [Acceptance and Sign-off](#10-acceptance-and-sign-off)
11. [Appendices](#11-appendices)

---

## 1. Executive Summary

<!--
Write this section last.

Expected content:
- What systems/components the environment setup covers.
- The stages used (dev, test, int, prod) and their hosting summary.
- Version control and collaboration platform at a glance.
- CI/CD tooling and promotion flow summary.
- Key constraints (budget, compliance, network, licensing).
-->

| Field | Summary |
|------|---------|
| **Scope of Setup** | <!-- 2-4 bullets --> |
| **Stages in Use** | <!-- e.g., dev / test / int / prod --> |
| **Version Control Summary** | <!-- VCS host, number of repos, branching model --> |
| **Collaboration Platform** | <!-- platform and main workspaces --> |
| **CI/CD Summary** | <!-- tool, pipelines, promotion flow --> |
| **Main Risks / Constraints** | <!-- short list --> |

---

## 2. Purpose, Scope, and Definitions

### 2.1 Purpose

<!--
Define why this Environment Setup document exists.

Examples:
- Provide a single source of truth for all environments, repositories, collaboration spaces, and pipelines.
- Enable every team member to find access, tools, and endpoints without tribal knowledge.
- Serve as the provisioning and acceptance baseline for DevOps / platform work.
-->

### 2.2 Scope

<!--
Define what is covered and what is not.

Include:
- All runtime stages (dev, test, int, prod) for the system(s) in scope.
- Version control repositories used for source, infrastructure, and documentation.
- Collaboration platform workspaces used for communication and coordination.
- CI/CD pipelines from commit to production deployment.
- Supporting setup: access, secrets, DNS, monitoring, backup, support.

Exclude (if applicable):
- Physical hardware procurement, org-wide network infrastructure.
- Other projects' environments unless shared.
-->

| In Scope | Out of Scope |
|----------|--------------|
| <!-- item --> | <!-- item --> |

### 2.3 Definitions and Abbreviations

| Term / Abbreviation | Definition |
|---------------------|------------|
| Stage | A distinct runtime environment of the system (dev, test, int, prod) |
| Promotion | Moving a validated build from one stage to the next |
| Quality Gate | Measurable criterion that must be met before promotion |
| Version Control Repository | Git repository hosting source code, IaC, or documentation |
| Collaboration Platform | Central platform for communication, work items, and knowledge (e.g., Teams, Jira) |
| CI/CD Pipeline | Automated build, test, and deployment workflow |
| IaC | Infrastructure as Code |
| SLO | Service Level Objective |

---

## 3. Project Overview

<!--
Give the context needed to understand the setup:
- What the system is and its main components.
- Deployment model and hosting approach.
- Who owns and operates the setup.
-->

| Field | Value |
|------|-------|
| **System / Application** | <!-- name and short description --> |
| **Main Components** | <!-- frontend / backend / APIs / jobs / databases --> |
| **Deployment Model** | <!-- cloud (which provider) / on-prem / hybrid --> |
| **Technology Stack Summary** | <!-- languages, frameworks, runtimes, databases --> |
| **Operations Model** | <!-- who deploys, who operates, support model --> |
| **Audience of This Document** | <!-- developers, QA, DevOps, support --> |

---

## 4. Stages (Environments)

<!--
This section defines the canonical stages of the project.
Use exactly the four stages below unless the project justifies deviations
(e.g., additional perf or training stage); document any extra stage with the
same per-stage template.

For each stage describe:
- Purpose and typical usage.
- Target environment and deployment model.
- Data profile and privacy constraints.
- Access controls (who can deploy, who can view).
- Configuration (env vars, feature flags, secret references).
- Quality gates required to promote to the next stage.
- Observability (logs, metrics, alerts).
-->

### 4.1 Stage Overview

| Stage | Purpose | Target Platform | Data Profile | Refresh Cadence | Access Controls | Owner |
|-------|---------|-----------------|--------------|-----------------|-----------------|-------|
| DEV | <!-- developer integration and experimentation --> | <!-- e.g., cloud dev subscription --> | <!-- synthetic / mock data --> | <!-- continuous --> | <!-- dev team only --> | |
| TEST | <!-- automated QA: functional, integration, NFR tests --> | | <!-- masked or synthetic test data --> | | <!-- dev + QA --> | |
| INT | <!-- integration / pre-production validation with partner systems --> | | <!-- prod-like masked data --> | | <!-- QA + selected stakeholders --> | |
| PROD | <!-- live operation for end users --> | | <!-- real data (protected) --> | <!-- n/a --> | <!-- ops + change-approved access --> | |

### 4.2 Stage Details

#### 4.2.1 Stage: DEV

<!--
Expected content:
- Purpose: continuous developer integration; unstable by design.
- Deployment: automatic on merge / per-commit, developer-triggered.
- Data: synthetic only; no personal or sensitive data allowed.
- Access: full dev team; lowest controls, highest speed.
- Quality gates to leave this stage: build green, unit tests, lint, scan.

Guidance:
- State explicitly what is NOT guaranteed here (availability, data realism).
-->

| Field | Value |
|------|-------|
| **Purpose and Usage** | <!-- what happens here and who uses it --> |
| **Target Environment** | <!-- platform, region, service plan --> |
| **Deployment Model** | <!-- trigger: on merge / manual; mechanism --> |
| **Data Profile** | <!-- synthetic data, reset strategy, prohibited data --> |
| **Access Controls** | <!-- deploy rights, view rights, approval needs --> |
| **Configuration Sources** | <!-- env vars, feature flags, secret references --> |
| **Quality Gates (Promotion to TEST)** | <!-- e.g., CI green, unit pass, lint, SAST --> |
| **Observability** | <!-- log access, metrics, alerts (if any) --> |

#### 4.2.2 Stage: TEST

<!--
Expected content:
- Purpose: automated QA execution (functional, integration, regression, NFR).
- Deployment: automatic from CI after quality gates, versioned builds only.
- Data: masked or synthetic test data sets; refresh cadence defined.
- Access: dev + QA; deployments restricted to pipeline/service accounts.
- Quality gates to leave this stage: automated test suites pass, no open
  critical defects, NFR criteria where applicable.

Guidance:
- Reference the Test Concept for suites that run here.
- Define how the stage is reset between test cycles.
-->

| Field | Value |
|------|-------|
| **Purpose and Usage** | |
| **Target Environment** | |
| **Deployment Model** | |
| **Data Profile** | <!-- data sets, masking, refresh cadence, owner --> |
| **Access Controls** | |
| **Configuration Sources** | |
| **Quality Gates (Promotion to INT)** | <!-- e.g., regression suite pass, no critical defects --> |
| **Observability** | |

#### 4.2.3 Stage: INT

<!--
Expected content:
- Purpose: pre-production integration with real partner/external systems and
  UAT by business stakeholders.
- Deployment: from a release candidate (tagged), manual approval required.
- Data: prod-like masked data; anonymization documented.
- Access: QA, tech lead, selected business stakeholders; change-controlled.
- Quality gates to leave this stage: UAT sign-off, security/perf evidence,
  release checklist complete.

Guidance:
- This is the last stage before PROD: treat configuration parity with prod as
  a requirement (same service plans where feasible).
-->

| Field | Value |
|------|-------|
| **Purpose and Usage** | |
| **Target Environment** | |
| **Deployment Model** | <!-- release candidate tag + manual approval --> |
| **Data Profile** | <!-- prod-like masked data, anonymization approach --> |
| **Access Controls** | <!-- approvers, UAT participants --> |
| **Configuration Sources** | |
| **Quality Gates (Promotion to PROD)** | <!-- e.g., UAT sign-off, security scan clean, perf SLOs met --> |
| **Observability** | |

#### 4.2.4 Stage: PROD

<!--
Expected content:
- Purpose: live operation serving real users and business traffic.
- Deployment: from approved release only; change window and approvers defined.
- Data: real, protected data; access restricted and audited.
- Access: operations team; break-glass procedure documented.
- Quality gates are entry gates: change approval, go-live gate (see Test
  Concept Section 5), rollback plan available.

Guidance:
- Document SLA/SLO targets, maintenance windows, and support hours.
- Document the rollback and incident escalation path.
-->

| Field | Value |
|------|-------|
| **Purpose and Usage** | |
| **Target Environment** | <!-- platform, region(s), high availability setup --> |
| **Deployment Model** | <!-- approved releases only, change window, approvers --> |
| **Data Profile** | <!-- real data; protection and audit requirements --> |
| **Access Controls** | <!-- ops roles, break-glass procedure --> |
| **Configuration Sources** | <!-- prod config, secret store references --> |
| **Entry Quality Gates (from INT)** | <!-- change approval + go-live gate + rollback plan --> |
| **Observability** | <!-- dashboards, alerts, on-call integration --> |
| **SLA / SLO Targets** | <!-- availability, response time, support hours --> |

### 4.3 Stage Promotion Flow

<!--
Define how builds move between stages.

Rules of thumb:
- DEV → TEST: automatic on green CI, no human approval.
- TEST → INT: automatic after test suites pass, tagged release candidate.
- INT → PROD: manual approval (change management), go-live gate.
-->

| From | To | Trigger | Automation | Required Approvals | Quality Gates | Rollback Strategy |
|------|----|---------|------------|--------------------|---------------|-------------------|
| DEV | TEST | <!-- e.g., merge to main --> | <!-- automatic --> | <!-- none --> | <!-- CI gates --> | <!-- redeploy previous build --> |
| TEST | INT | <!-- release candidate tagged --> | <!-- automatic / manual --> | <!-- tech lead --> | <!-- test suites --> | |
| INT | PROD | <!-- go-live decision --> | <!-- manual --> | <!-- change board / PO --> | <!-- go-live gate --> | |

---

## 5. Version Control Repositories

<!--
Inventory every repository the project relies on:
- Source code, IaC, scripts, documentation repos.
- Which stage deploys from which branch.
- Branching model and versioning scheme (align with the
  git-workflow-and-versioning skill if used).
-->

### 5.1 Repository Inventory

| Repo ID | Repository | VCS Host | Purpose | Visibility | Default Branch | Owner |
|---------|-----------|----------|---------|------------|----------------|-------|
| REPO-001 | <!-- e.g., project-backend --> | <!-- GitHub / Azure DevOps / GitLab --> | <!-- backend source --> | <!-- private --> | <!-- main --> | |
| REPO-002 | <!-- e.g., project-infra --> | | <!-- IaC and environment setup --> | | | |

### 5.2 Branching and Versioning Model

<!--
Expected content:
- Branch naming conventions (feature/, bugfix/, release/, hotfix/).
- Which branch deploys to which stage (e.g., main → TEST, tag → INT/PROD).
- Versioning scheme (e.g., Semantic Versioning) and tag format.
-->

| Branch / Tag Pattern | Purpose | Deploys To | Protection |
|---------------------|---------|------------|------------|
| <!-- feature/* --> | <!-- work in progress --> | <!-- none (PR only) --> | <!-- no direct push --> |
| <!-- main --> | <!-- integration branch --> | <!-- DEV / TEST --> | <!-- PR + reviews required --> |
| <!-- release/* --> | <!-- release candidates --> | <!-- INT --> | <!-- maintainer approval --> |
| <!-- tag vX.Y.Z --> | <!-- released versions --> | <!-- INT / PROD --> | <!-- signed tags --> |

### 5.3 Protection and Review Rules

<!--
List repository protection rules and review requirements.
-->

| Rule | Applies To | Enforcement | Owner |
|------|-----------|-------------|-------|
| <!-- required PR reviews --> | | <!-- branch protection --> | |
| <!-- signed commits --> | | | |
| <!-- status checks required --> | | <!-- CI must pass before merge --> | |
| <!-- no force push / no direct push to main --> | | | |

---

## 6. Collaboration Platform

<!--
Describe the collaboration platform(s) used for communication, work items,
and knowledge management. Cover both chat/collaboration (e.g., Microsoft
Teams, Slack) and work management (e.g., Jira, Azure Boards) if both exist.
-->

### 6.1 Platform Overview

| Field | Value |
|------|-------|
| **Platform** | <!-- e.g., Microsoft Teams / Slack / Jira --> |
| **Purpose** | <!-- communication, work items, documentation --> |
| **Tenant / Organization** | <!-- tenant name or URL --> |
| **Admin / Owner** | <!-- who administers the workspace --> |

### 6.2 Workspaces and Channels

| ID | Workspace / Channel | Type | Purpose | Audience | Owner |
|----|---------------------|------|---------|----------|-------|
| COL-001 | <!-- e.g., Team: <Project> General --> | <!-- team / channel --> | <!-- announcements, general coordination --> | <!-- whole project team --> | |
| COL-002 | <!-- e.g., Channel: <Project> CI/CD Alerts --> | | <!-- pipeline notifications --> | | |
| COL-003 | <!-- e.g., Channel: <Project> Incidents --> | | <!-- incident coordination --> | | |

### 6.3 Artifact Linking

<!--
Document where key artifacts live and how they are linked so that anyone can
navigate from chat to code, pipelines, and documents.
-->

| Artifact | Location / Link | Notes |
|----------|-----------------|-------|
| <!-- Source repositories --> | | <!-- linked in channel tabs/pins --> |
| <!-- CI/CD pipelines --> | | |
| <!-- Work items / backlog --> | | |
| <!-- Project documentation --> | <!-- documentation/ folder or wiki --> | |
| <!-- Dashboards / reports --> | | |

### 6.4 Notifications and Alerts

<!--
Define what is pushed to which channel and who is expected to react.
-->

| Source | Channel / Audience | Trigger | Expected Reaction |
|--------|--------------------|---------|-------------------|
| <!-- CI pipeline failures --> | | <!-- build/test failure on main --> | <!-- fix or revert same day --> |
| <!-- CD deployments --> | | <!-- deployment to TEST/INT/PROD --> | |
| <!-- Production alerts --> | | <!-- SLO breach, incident --> | <!-- on-call responds per SLA --> |

---

## 7. CI/CD Pipelines

<!--
Inventory all pipelines from commit to production.
For each pipeline define triggers, stages, approvals, and quality gates.
Align quality gates with the Test Concept (Section 5).
-->

### 7.1 Pipeline Inventory

| Pipeline ID | Pipeline Name | Tool | Trigger | Stage(s) | Purpose | Owner |
|-------------|---------------|------|---------|----------|---------|-------|
| PIPE-001 | <!-- e.g., build-and-test --> | <!-- GitHub Actions / Azure Pipelines --> | <!-- push / PR --> | <!-- DEV/TEST --> | <!-- build, unit tests, scans --> | |
| PIPE-002 | <!-- e.g., deploy-test --> | | <!-- CI success on main --> | <!-- TEST --> | | |
| PIPE-003 | <!-- e.g., deploy-int --> | | <!-- release tag --> | <!-- INT --> | | |
| PIPE-004 | <!-- e.g., deploy-prod --> | | <!-- manual + approval --> | <!-- PROD --> | | |

### 7.2 CI Pipeline Stages (Build and Verify)

<!--
Expected content:
- Jobs and their order (build, unit tests, lint, SAST/SCA, package).
- What artifacts are produced (container images, packages) and where stored.
- Success criteria to pass CI.
-->

| Job | Purpose | Tools | Success Criteria | Blocking? |
|-----|---------|-------|------------------|-----------|
| <!-- build --> | <!-- compile and package --> | | <!-- artifact produced --> | Yes |
| <!-- unit tests --> | <!-- logic validation --> | | <!-- pass rate + coverage target --> | Yes |
| <!-- lint / static analysis --> | <!-- code quality --> | | <!-- no new findings --> | <!-- Yes/No --> |
| <!-- security scan (SAST/SCA) --> | <!-- vulnerability detection --> | | <!-- no critical/high without waiver --> | <!-- Yes/No --> |

### 7.3 CD Pipeline Stages (Deploy and Promote)

<!--
Expected content:
- Per stage: deployment method, approvals, and post-deployment verification
  (smoke tests, health checks).
- Rollback mechanism per stage.
-->

| Pipeline | Target Stage | Deployment Method | Approvals | Post-Deployment Verification | Rollback |
|----------|--------------|-------------------|-----------|------------------------------|----------|
| <!-- deploy-test --> | TEST | <!-- e.g., IaC + pipeline --> | <!-- automatic --> | <!-- smoke tests --> | <!-- redeploy previous --> |
| <!-- deploy-int --> | INT | | <!-- tech lead --> | <!-- UAT readiness check --> | |
| <!-- deploy-prod --> | PROD | <!-- e.g., blue-green / rolling --> | <!-- change board --> | <!-- health checks + alerts quiet --> | |

### 7.4 Pipeline Variables and Secrets

<!--
Expected content:
- Where pipeline variables live (pipeline config, variable groups, secret store).
- Secret handling rules: never in code, masked in logs, rotation owner.
- Mapping of secrets to stages.
-->

| Secret / Variable | Stages | Source of Truth | Access | Rotation Owner |
|-------------------|--------|-----------------|--------|----------------|
| <!-- e.g., DB connection string --> | | <!-- secret store reference --> | <!-- pipeline service account only --> | |

### 7.5 Quality Gates

<!--
Define measurable gates tied to the promotion flow (Section 4.3).
Use "blocking" vs "non-blocking".
-->

| Gate ID | Gate Name | Stage | Blocking? | Criteria | Measured By | Owner |
|---------|-----------|-------|-----------|----------|-------------|-------|
| G-001 | PR Merge Gate | <!-- PR/CI --> | Yes | <!-- build + unit + lint + scan pass --> | | |
| G-002 | Test Stage Gate | <!-- TEST --> | Yes | <!-- automated suites pass; no critical defects --> | | |
| G-003 | INT Gate | <!-- INT --> | Yes | <!-- UAT sign-off; security/perf evidence --> | | |
| G-004 | Go-Live Gate | <!-- PROD --> | Yes | <!-- change approval + rollback plan --> | | |

---

## 8. Prerequisites and Access Management

<!--
Everything a person needs before working on the project:
accounts, roles, licenses, and installed tools.
Track provisioning as a checklist with owners and status.
-->

### 8.1 Accounts and Roles

| System | Role / Account | Who Needs It | How to Request | Approval |
|--------|----------------|--------------|----------------|----------|
| <!-- VCS --> | <!-- developer write access --> | | <!-- e.g., via access request form --> | |
| <!-- Collaboration platform --> | <!-- team membership --> | | | |
| <!-- CI/CD tool --> | <!-- pipeline admin / viewer --> | | | |
| <!-- Cloud platform --> | <!-- subscription roles per stage --> | | | |

### 8.2 Licenses and Tools

| Tool | Version | Purpose | License Required? | Owner |
|------|---------|---------|-------------------|-------|
| <!-- IDE --> | | | | |
| <!-- runtime (Node/Java/Python) --> | | | | |
| <!-- container tooling --> | | | | |
| <!-- IaC CLI (Terraform/Bicep) --> | | | | |

### 8.3 Provisioning Checklist

| ID | Item | Applies To | Needed By | Owner | Status |
|----|------|------------|-----------|-------|--------|
| PR-001 | VCS repositories created and protected | All | <!-- Kick-off --> | | <!-- Not started / In progress / Done --> |
| PR-002 | Collaboration workspace and channels created | All | | | |
| PR-003 | DEV stage provisioned (IaC applied) | DEV | | | |
| PR-004 | TEST stage provisioned with test data sets | TEST | | | |
| PR-005 | INT stage provisioned, partner connections agreed | INT | | | |
| PR-006 | PROD stage provisioned, change process registered | PROD | | | |
| PR-007 | CI/CD pipelines configured with service accounts | All | | | |
| PR-008 | Secrets created in secret store and referenced | All | | | |
| PR-009 | Monitoring/alerting wired to on-call | PROD | | | |

---

## 9. Additional Environment Setup Content

<!--
Additional setup topics that belong to a complete environment but are not
pure code or pipelines. Complete every subsection; mark n/a explicitly if a
topic does not apply.
-->

### 9.1 Domain, DNS, and Certificates

<!--
Expected content:
- DNS zones and records per stage, who manages them.
- TLS certificate sources (managed by platform, CA-issued), renewal process.
-->

| Stage | Domain / URL | DNS Management | Certificate | Renewal / Owner |
|-------|--------------|----------------|-------------|-----------------|
| DEV | | | | |
| TEST | | | | |
| INT | | | | |
| PROD | | | | |

### 9.2 Secrets Management and Credential Rotation

<!--
Expected content:
- Secret store(s) per stage.
- Which secrets exist and their owners.
- Rotation schedule and emergency rotation procedure.
-->

| Secret Store | Stages | What Is Stored | Access | Rotation Schedule | Owner |
|--------------|--------|----------------|--------|-------------------|-------|
| | | <!-- credentials, keys, connection strings --> | | | |

### 9.3 Networking and Connectivity

<!--
Expected content:
- Network topology per stage (VNets, subnets, firewall rules).
- Required connectivity to partner/external systems (INT especially).
- IP allowlists and service endpoints.
-->

| Topic | Stage(s) | Description | Owner |
|-------|----------|-------------|-------|
| <!-- network topology --> | | | |
| <!-- partner connectivity --> | <!-- INT/PROD --> | <!-- endpoints, protocols, allowlists --> | |
| <!-- firewall rules / egress --> | | | |

### 9.4 Backup and Disaster Recovery

<!--
Expected content:
- What is backed up per stage (databases, configs, secrets).
- Backup schedule, retention, and restore test cadence.
- RTO/RPO targets and DR strategy per stage.
-->

| Stage | Backup Scope | Schedule / Retention | RTO / RPO | Restore Test Cadence | Owner |
|-------|--------------|----------------------|-----------|----------------------|-------|
| DEV | <!-- minimal / none accepted --> | | <!-- n/a --> | | |
| TEST | | | | | |
| INT | | | | | |
| PROD | <!-- full backup + DR site/strategy --> | | | | |

### 9.5 Monitoring, Alerting, and On-Call

<!--
Expected content:
- Observability stack per stage (logs, metrics, traces, dashboards).
- Alert rules and severities; who receives them.
- On-call rotation and escalation path.
-->

| Stage | Logs | Metrics / Dashboards | Alerts | On-Call |
|-------|------|----------------------|--------|---------|
| DEV | <!-- optional --> | | <!-- none expected --> | <!-- n/a --> |
| TEST | | | <!-- pipeline/test failures --> | |
| INT | | | <!-- integration health --> | |
| PROD | <!-- full retention per policy --> | | <!-- SLO alerts, severities --> | <!-- rotation + escalation --> |

### 9.6 Support and Incident Management

<!--
Expected content:
- Service desk / support channels per stage.
- Incident severity levels and response SLAs.
- Runbook locations and escalation contacts.
-->

| Field | Value |
|------|-------|
| **Support Channels** | <!-- service desk, ticketing, chat --> |
| **Incident Severity Levels** | <!-- Sev1..Sev4 with definitions and response SLAs --> |
| **Runbooks Location** | <!-- link --> |
| **Escalation Contacts** | <!-- roles and order --> |

---

## 10. Acceptance and Sign-off

### 10.1 Exit Criteria Summary

| Area | Exit Criterion | Met? | Evidence |
|------|----------------|------|----------|
| Stages | All stages in Section 4 provisioned and verified | <!-- Yes/No --> | <!-- IaC apply logs --> |
| Repositories | All repos in Section 5 created with protections | | |
| Collaboration | Workspaces and channels created, links verified (Section 6) | | |
| CI/CD | All pipelines in Section 7 executed end-to-end once | | |
| Access | Accounts/roles provisioned (Section 8) | | |
| Operations | Monitoring, backup, and support setup verified (Section 9) | | |

### 10.2 Sign-off

| Stakeholder | Role | Approval | Date | Notes |
|-------------|------|----------|------|-------|
| | Product Owner | ✅ / ❌ | | |
| | Technical Lead | ✅ / ❌ | | |
| | DevOps Lead | ✅ / ❌ | | |
| | Security Lead | ✅ / ❌ | | |
| | Project Manager | ✅ / ❌ | | |

---

## 11. Appendices

### Appendix A: Environment Setup Checklist

| Checklist Item | Status | Notes |
|----------------|--------|-------|
| All four stages defined with purpose, data, access | | |
| Stage promotion flow documented and agreed | | |
| Repository inventory complete with protections | | |
| Collaboration workspaces and channels created | | |
| Pipeline inventory complete and end-to-end tested | | |
| Secrets stored in secret store, rotation defined | | |
| DNS, domains, certificates in place | | |
| Backup/DR configured and restore tested | | |
| Monitoring/alerting wired to on-call | | |
| Support/incident process documented | | |

### Appendix B: Provisioning Checklist Reference

<!--
Use Section 8.3 as the working checklist during setup.
Keep status here only if you want a snapshot at sign-off time.
-->

| Phase | Items (from Section 8.3) | Status Snapshot | Date |
|-------|--------------------------|-----------------|------|
| Kick-off | | | |
| First release to TEST | | | |
| First release to PROD | | | |

### Appendix C: Troubleshooting Notes

<!--
Collect recurring setup issues and fixes so future team members save time.
-->

| Symptom | Likely Cause | Fix / Where to Look |
|---------|--------------|---------------------|
| | | |

---

## Document History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | <!-- date --> | <!-- author --> | Initial template |
