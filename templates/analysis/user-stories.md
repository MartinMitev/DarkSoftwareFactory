# Software Project User Stories

> **Template Version:** 1.0  
> **Last Updated:** <!-- date -->  
> **Document Status:** <!-- Draft | Under Review | Approved | Baselined -->

---

## Metadata

| Field | Value |
|-------|-------|
| **Project Name** | <!-- project name --> |
| **Project Type** | <!-- Green Field | Brown Field | Software Modernization --> |
| **Product Owner** | <!-- product owner name --> |
| **Scrum Master / Agile Lead** | <!-- scrum master name --> |
| **Technical Lead** | <!-- technical lead name --> |
| **Author(s)** | <!-- author name(s) --> |
| **Date Created** | <!-- creation date --> |
| **Date Revised** | <!-- revision date --> |
| **Classification** | <!-- Public | Internal | Confidential --> |
| **Baseline Version** | <!-- version once approved --> |
| **Source Documents** | <!-- SRS / project scope references --> |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [User Story Map](#2-user-story-map)
3. [Epics](#3-epics)
4. [User Stories](#4-user-stories)
5. [Acceptance Criteria](#5-acceptance-criteria)
6. [Non-Functional Story Attributes](#6-non-functional-story-attributes)
7. [Story Dependencies & Sequencing](#7-story-dependencies--sequencing)
8. [Estimation & Velocity](#8-estimation--velocity)
9. [Definition of Ready & Definition of Done](#9-definition-of-ready--definition-of-done)
10. [Story Splitting Guide](#10-story-splitting-guide)
11. [Migration & Transition Stories](#11-migration--transition-stories)
12. [Story Change Control](#12-story-change-control)
13. [Appendices](#13-appendices)

---

## 1. Introduction

### 1.1 Purpose

<!--
State the purpose of this user story document.

Expected content:
- This document captures the user-facing requirements as user stories — the Agile team's contract for what to build.
- The intended audience: development team, product owner, stakeholders, QA.
- Relationship to preceding documents: the SRS defines detailed system requirements; this document translates them into user stories that the delivery team can estimate, plan, and deliver incrementally.
- User stories answer: "What do users need, why, and how do we know it's done?"
-->

### 1.2 Project Type Classification

<!--
Classify the project and explain implications for user stories.

🟢 Green Field — All stories are net-new; full freedom in sequencing and splitting.
🟤 Brown Field — Stories include new behavior, modifications to existing behavior, and regression-safe changes; must reference existing system behavior.
🔵 Software Modernization — Stories include feature parity stories (behavior preservation), new platform stories, and migration transition stories; must reference legacy behavior.

Icons: 🟢 Green Field | 🟤 Brown Field | 🔵 Modernization | ⚪ All Types
-->

| Attribute | Value |
|-----------|-------|
| **Project Type** | <!-- Green Field / Brown Field / Software Modernization --> |
| **Implications for Stories** | <!-- what this means for story writing --> |

### 1.3 User Story Format

<!--
Define the user story format used throughout this document.

Expected content:
- Standard format: "As a [persona/role], I want [action/capability], so that [benefit/value]."
- The persona must match a defined user persona (from SRS Section 3.1 or project scope).
- The action must be specific and testable.
- The benefit must articulate measurable or observable value.
- For 🟤🔵: stories modifying existing behavior use the format: "As a [persona], I want [changed behavior], so that [improved value], where currently [existing behavior]."
-->

### 1.4 Story Identification Scheme

<!--
Define how stories are uniquely identified.

Expected content:
- Epic ID format: EP-XX (e.g., EP-01).
- User Story ID format: US-XXX (e.g., US-001).
- Story IDs are sequential and never reused even if stories are removed.
- Link to SRS requirement IDs (FR-XXX, NFR-XXX) for traceability.
-->

| ID Prefix | Category | Example |
|-----------|----------|---------|
| EP- | Epic | EP-01 |
| US- | User Story | US-001 |
| AC- | Acceptance Criterion | AC-001 (per story: US-001.AC-1) |
| TC- | Test Case | TC-001 |

### 1.5 Definitions & Abbreviations

| Term | Definition |
|------|-----------|
| Epic | Large body of work spanning multiple sprints; decomposed into user stories |
| User Story | Small, deliverable unit of user value; fits within a single sprint |
| Acceptance Criterion | Measurable condition that must be true for the story to be considered done |
| Story Points | Relative size/complexity estimate (Fibonacci: 1, 2, 3, 5, 8, 13) |
| MoSCoW | Must Have / Should Have / Could Have / Won't Have This Time |
| DoR | Definition of Ready — criteria a story must meet before entering a sprint |
| DoD | Definition of Done — criteria a story must meet to be considered complete |
| Feature Parity 🔵 | Story that replicates existing legacy behavior on the new platform |

---

## 2. User Story Map

### 2.1 Story Map Overview ⚪

<!--
Provide the user story map — the backbone of user journeys with stories prioritized vertically (Must → Could) and sequenced horizontally (release phases).

Expected content:
- The backbone: major user activities or workflows (top row).
- Below each activity: user tasks grouped by release phase (MVP / Phase 1 / Phase 2 / Phase N).
- The story map shows the team's plan for incremental delivery.
- 🟤🔵: Include a "Parity Backbone" row showing which legacy features must be replicated per phase.
-->

| User Activity | MVP / Phase 1 | Phase 2 | Phase 3 | Phase N |
|--------------|---------------|---------|---------|---------|
| <!-- activity --> | <!-- stories --> | | | |

### 2.2 Release-Aligned Story Map ⚪

<!--
Map stories to release milestones.

Expected content:
- Release name, target date, story set per release.
- Minimum Viable Product (MVP) or Minimum Marketable Feature (MMF) definition.
- Which epics and stories must be complete for each release.
- 🟤🔵: Legacy feature retirement per release — which legacy features each release replaces.
-->

| Release | Target Date | Epics | Must-Have Stories | Should-Have Stories | Legacy Retired 🔵 |
|---------|-------------|-------|-------------------|---------------------|-------------------|
| MVP | | | | | |
| Phase 2 | | | | | |

### 2.3 Story Map Traceability ⚪

<!--
Map story map activities to SRS requirements and project scope items.

Expected content:
- Each user activity in the story map should trace to scope items and SRS requirements.
- Ensures the story map covers the full scope.
-->

| Story Map Activity | Scope Item | SRS Requirement IDs | Coverage Status |
|-------------------|-----------|---------------------|-----------------|
| | | | <!-- Complete / Partial / Gap --> |

---

## 3. Epics

### 3.1 Epic Registry ⚪

<!--
List all epics with summary information.

Expected content:
- Epic ID, name, description, business value, MoSCoW priority, number of stories, traced SRS requirements.
- Each epic groups related stories that deliver a cohesive capability.
- Epics should align with feature areas from the SRS.
-->

| Epic ID | Epic Name | Description | Business Value | MoSCoW | Story Count | SRS Trace |
|---------|-----------|-------------|---------------|--------|-------------|-----------|
| EP-01 | | | | | | |
| EP-02 | | | | | | |

### 3.2 Epic Details

<!--
For each epic, provide detailed context.

Expected content per epic:
- Epic goal: what business capability this epic delivers.
- Target users: which personas benefit.
- Success metrics: how to measure the epic's value delivery.
- Dependencies on other epics.
- Risk level and complexity.
- 🟤🔵: Parity epic indicator — does this epic replicate legacy behavior?
- 🟤🔵: Legacy features this epic replaces.
-->

#### EP-01: [Epic Name]

| Attribute | Value |
|-----------|-------|
| **Goal** | <!-- what this epic achieves --> |
| **Target Personas** | <!-- who benefits --> |
| **Success Metrics** | <!-- how value is measured --> |
| **Dependencies** | <!-- other epics --> |
| **Risk / Complexity** | <!-- Low / Medium / High --> |
| **Parity Epic?** 🟤🔵 | <!-- Yes — replaces [legacy feature] / No — net-new --> |
| **SRS Requirements** | <!-- FR-XXX, NFR-XXX --> |
| **MoSCoW** | <!-- Must / Should / Could --> |

---

## 4. User Stories

### 4.1 Story Registry ⚪

<!--
Master list of all user stories with key attributes.

Expected content:
- Story ID, title, epic, persona, MoSCoW, story points, sprint/release assignment, status.
- Status values: Backlog / Ready / In Progress / In Review / Done / Blocked.
-->

| Story ID | Title | Epic | Persona | MoSCoW | Points | Sprint / Release | Status |
|----------|-------|------|---------|--------|--------|------------------|--------|
| US-001 | | EP-XX | | | | | Backlog |

### 4.2 Detailed User Story Specifications ⚪

<!--
Each story written in full detail.

Expected content per story:
- Story statement: "As a [persona], I want [action], so that [benefit]."
- For 🟤🔵 modifying existing behavior: "…where currently [existing behavior]."
- Story ID, Epic, Priority, Story Points, Sprint.
- Acceptance criteria (see Section 5).
- Traces to SRS requirements.
- Dependencies on other stories.
- Technical notes (hints for implementation, not design decisions).
- Questions / unknowns.
-->

#### US-001: [Story Title]

| Attribute | Value |
|-----------|-------|
| **Story ID** | US-001 |
| **Epic** | EP-XX |
| **Story Statement** | As a <!-- persona -->, I want <!-- action -->, so that <!-- benefit -->. |
| **Existing Behavior** 🟤🔵 | <!-- what the current system does --> |
| **MoSCoW** | <!-- Must / Should / Could --> |
| **Story Points** | <!-- 1 / 2 / 3 / 5 / 8 / 13 --> |
| **Sprint / Release** | <!-- Sprint X / Release Y --> |
| **SRS Trace** | <!-- FR-XXX, NFR-XXX --> |
| **Dependencies** | <!-- US-XXX must be done first --> |
| **Technical Notes** | <!-- implementation hints --> |
| **Questions / Unknowns** | <!-- open questions --> |
| **Status** | <!-- Backlog / Ready / In Progress / In Review / Done / Blocked --> |

**Acceptance Criteria:**

| AC ID | Criterion | Given | When | Then |
|-------|-----------|-------|------|------|
| US-001.AC-1 | <!-- description --> | <!-- precondition --> | <!-- action --> | <!-- expected result --> |

---

## 5. Acceptance Criteria

### 5.1 Acceptance Criteria Guidelines ⚪

<!--
Define how acceptance criteria are written.

Expected content:
- Use Given/When/Then (BDD/Gherkin) format for behavioral criteria.
- Each criterion must be: testable, unambiguous, and independent.
- Every story must have at least one acceptance criterion.
- Must Have stories require comprehensive criteria; Could Have stories may have lighter criteria.
- 🟤🔵: Parity criteria must specify the exact behavior from the legacy system that must be preserved.
-->

### 5.2 Acceptance Criteria by Story ⚪

<!--
All acceptance criteria collected for review.

Expected content:
- For each story, its full set of acceptance criteria.
- Criteria organized by: functional behavior, error handling, edge cases, NFRs (if story-specific).
-->

| Story ID | AC ID | Type | Given | When | Then |
|----------|-------|------|-------|------|------|
| US-001 | US-001.AC-1 | <!-- Functional / Error / Edge / NFR --> | | | |
| US-001 | US-001.AC-2 | | | | |

### 5.3 Parity Acceptance Criteria 🔵🟤

<!--
Acceptance criteria specifically for feature parity stories.

Expected content:
- For each parity story: the exact legacy behavior, the expected new behavior, and how parity will be verified.
- Behavioral differences (intentional or incidental) between legacy and new system.
- Verification method: parallel test, automated comparison, manual UAT.
-->

| Story ID | Legacy Behavior | New Behavior | Parity Level | Difference | Verification Method |
|----------|----------------|-------------|--------------|-----------|-------------------|
| | | | 100% / Partial | | |

---

## 6. Non-Functional Story Attributes

### 6.1 NFRs Mapped to Stories ⚪

<!--
Map non-functional requirements to the stories they constrain.

Expected content:
- Which stories are affected by which NFRs.
- How NFR acceptance criteria are incorporated into stories.
- Stories with significant NFR implications should be flagged.
-->

| NFR ID | NFR | Affected Stories | AC Integration | Priority |
|--------|-----|-----------------|---------------|----------|
| NFR-001 | <!-- e.g., p99 latency <200ms --> | <!-- US-XXX --> | <!-- added as AC --> | |

### 6.2 Performance Stories ⚪

<!--
Stories specifically about performance targets.

Expected content:
- Stories that establish or validate performance baselines.
- Load testing stories.
- Performance regression stories for 🟤🔵.
-->

| Story ID | Performance Target | Baseline 🟤🔵 | Test Method | Sprint |
|----------|-------------------|---------------|-------------|--------|
| | | | | |

### 6.3 Security Stories ⚪

<!--
Stories specifically about security requirements.

Expected content:
- Authentication, authorization, encryption stories.
- Vulnerability scanning and remediation stories.
- Compliance-mandated security stories.
-->

| Story ID | Security Requirement | Regulation | Sprint |
|----------|---------------------|-----------|--------|
| | | | |

---

## 7. Story Dependencies & Sequencing

### 7.1 Dependency Map ⚪

<!--
Map dependencies between stories.

Expected content:
- Hard dependencies: US-B cannot start until US-A is done.
- Soft dependencies: US-B is easier if US-A is done first.
- External dependencies: story blocked by third-party, vendor, or another team.
- 🟤🔵: Parity dependencies — parity stories that must be done before legacy features can be retired.
-->

| Story | Depends On | Type | Rationale |
|-------|-----------|------|-----------|
| US-002 | US-001 | <!-- Hard / Soft / External --> | |

### 7.2 Critical Path Stories ⚪

<!--
Identify stories on the critical delivery path.

Expected content:
- Stories that, if delayed, push the entire release date.
- Stories with the highest risk or uncertainty.
- 🟤🔵: Migration cutover-critical stories.
-->

| Story | Critical Path Reason | Risk | Mitigation |
|-------|---------------------|------|------------|
| | | | |

### 7.3 Sequencing Recommendations ⚪

<!--
Recommend the order of story delivery.

Expected content:
- Technical sequencing: what must be built first (foundations, enablers).
- Value sequencing: what delivers the most value earliest.
- Risk sequencing: what reduces risk fastest.
- 🟤🔵: Parity-first sequencing vs. new-features-first.
-->

| Priority | Sequencing Strategy | Stories Affected | Rationale |
|----------|-------------------|------------------|-----------|
| 1 | <!-- e.g., Enablers first --> | | |

---

## 8. Estimation & Velocity

### 8.1 Story Point Summary ⚪

<!--
Summarize estimation data.

Expected content:
- Total story points by epic.
- Total story points by MoSCoW priority.
- Total story points by release/phase.
- Team velocity assumption (points per sprint).
- Estimated number of sprints per release.
-->

| Epic | Must Have Points | Should Have Points | Could Have Points | Total Points |
|------|-----------------|-------------------|------------------|-------------|
| EP-01 | | | | |
| **Total** | | | | |

| Release | Total Points | Team Velocity | Estimated Sprints | Target Date |
|---------|-------------|--------------|------------------|-------------|
| MVP | | | | |

### 8.2 Estimation Basis ⚪

<!--
Document the estimation approach.

Expected content:
- Estimation method (Planning Poker, T-shirt sizing, etc.).
- Reference story: which story is the team's "1-point" baseline.
- Assumptions underlying estimates (team size, sprint length, availability).
- Confidence level of estimates (Rough / Budget / Committed).
-->

| Parameter | Value |
|-----------|-------|
| Estimation Method | <!-- e.g., Planning Poker --> |
| Sprint Length | <!-- e.g., 2 weeks --> |
| Reference 1-Point Story | <!-- description --> |
| Team Size | <!-- number --> |
| Confidence | <!-- Rough / Budget / Committed --> |

### 8.3 Velocity Tracking ⚪

<!--
Track actual velocity against estimated.

Expected content:
- Sprint-by-sprint actual vs. planned velocity.
- Running average velocity.
- Burn-down or burn-up chart reference.
-->

| Sprint | Planned Points | Completed Points | Velocity | Running Average | Notes |
|--------|---------------|-----------------|----------|---------------|-------|
| Sprint 1 | | | | | |

---

## 9. Definition of Ready & Definition of Done

### 9.1 Definition of Ready (DoR) ⚪

<!--
Define when a story is ready to be worked on in a sprint.

Expected content:
- Story statement is clear and uses the standard format.
- Acceptance criteria are defined and reviewed.
- Dependencies are identified and resolved (or have a plan).
- SRS traceability is established.
- UX designs or wireframes are available (if UI story).
- Technical approach is understood (spike completed if uncertain).
- Story is estimated by the team.
- Product Owner has prioritized the story.
-->

| DoR Criterion | Verified By | Enforced At |
|---------------|-------------|-------------|
| Story statement uses standard format | PO | Backlog refinement |
| Acceptance criteria defined | PO + QA | Backlog refinement |
| Dependencies identified | Tech Lead | Backlog refinement |
| SRS trace established | Analyst | Backlog refinement |
| UX designs available | Designer | Sprint planning |
| Story estimated | Team | Sprint planning |
| **All criteria met → Ready** | Scrum Master | Sprint planning |

### 9.2 Definition of Done (DoD) ⚪

<!--
Define when a story is considered complete.

Expected content:
- Code implemented and peer-reviewed.
- Unit and integration tests written and passing.
- Test coverage meets minimum threshold.
- Acceptance criteria verified (all AC pass).
- Security scan completed with no critical/high findings.
- Documentation updated (API docs, user docs, runbooks).
- Deployed to target environment.
- Product Owner sign-off.
- 🟤🔵: Regression tests passed for existing functionality.
- 🟤🔵: Feature parity verified for migrated features.
-->

| DoD Criterion | Verified By | Enforced At |
|---------------|-------------|-------------|
| Code reviewed | Team | PR merge |
| Tests passing | CI | PR merge |
| Coverage threshold met | CI | PR merge |
| Acceptance criteria verified | QA + PO | Sprint review |
| Security scan clean | CI | Release |
| Documentation updated | Team | PR checklist |
| PO sign-off | PO | Sprint review |
| **All criteria met → Done** | Scrum Master | Sprint review |

---

## 10. Story Splitting Guide

### 10.1 When to Split Stories ⚪

<!--
Define thresholds for when stories should be split.

Expected content:
- Stories estimated at 8+ points should be split.
- Stories spanning multiple personas should be split.
- Stories with more than 6 acceptance criteria should be split.
- Stories mixing functional and non-functional concerns should be split.
- Stories that cannot be completed in a single sprint should be split.
-->

| Splitting Trigger | Threshold | Action |
|-------------------|-----------|--------|
| Story too large | ≥ 8 points | Split into 2+ smaller stories |
| Multiple personas | > 1 persona | Split by persona |
| Too many AC | > 6 criteria | Split by functional boundary |
| Mixed concerns | Functional + NFR | Separate NFR into own story or AC |
| Sprint overflow | Cannot finish in 1 sprint | Split into sprint-sized pieces |

### 10.2 Story Splitting Patterns ⚪

<!--
Provide patterns for splitting stories effectively.

Expected content:
- Split by workflow step: CRUD → Create story, Read story, Update story, Delete story.
- Split by data: happy path first, then edge cases.
- Split by persona: split stories serving different users.
- Split by platform: web first, then mobile.
- Split by business rule: simple rule first, complex rules as additional stories.
- 🟤🔵: Split parity story from new-feature story.
-->

| Pattern | When to Use | Example |
|---------|------------|---------|
| By workflow step | Story covers full CRUD | US-001: Create → US-002: Read → US-003: Update |
| By data | Happy path + edge cases | US-001: Valid input → US-004: Invalid input |
| By persona | Multiple user types | US-001: Admin view → US-005: End-user view |
| By business rule | Simple + complex rules | US-001: Basic pricing → US-006: Discount rules |
| Parity vs. new 🟤🔵 | Legacy replication + enhancement | US-001: Replicate search → US-007: Add filters |

---

## 11. Migration & Transition Stories

### 11.1 Feature Parity Stories 🔵🟤

<!--
Stories that replicate existing legacy behavior on the new platform.

Expected content:
- Each parity story references the exact legacy feature and its behavior.
- Parity stories include behavioral acceptance criteria matching the legacy system.
- Priority: Must Have (parity stories are typically prerequisites for migration).
- Stories are marked with 🔵 parity indicator.
-->

| Story ID | Legacy Feature | Legacy Behavior | New Behavior | Parity Level | Priority |
|----------|---------------|----------------|-------------|--------------|----------|
| | | | | 100% / Partial | Must |

### 11.2 Data Migration Stories 🔵🟤

<!--
Stories for data migration activities.

Expected content:
- Data migration scripts, tooling, validation, reconciliation.
- Each story covers a specific data entity or migration phase.
- Includes stories for: migration script development, test migration, validation, delta migration, cutover migration.
-->

| Story ID | Data Entity | Migration Phase | Validation Method | Sprint |
|----------|-------------|----------------|-------------------|--------|
| | | <!-- script / test / delta / cutover --> | | |

### 11.3 Transition Stories 🔵🟤

<!--
Stories for the transition period (dual-running, cutover, rollback).

Expected content:
- Dual-running monitoring stories.
- Feature flag setup stories.
- Cutover execution stories.
- Rollback testing stories.
- User migration and communication stories.
-->

| Story ID | Transition Activity | Rollback Covered | Sprint |
|----------|-------------------|------------------|--------|
| | | <!-- Yes / No --> | |

### 11.4 Legacy Decommission Stories 🔵

<!--
Stories for retiring the legacy system.

Expected content:
- Decommission checklist execution.
- Legacy system shutdown.
- Contract termination.
- Data archival.
- Final verification that no dependencies remain.
-->

| Story ID | Decommission Activity | Prerequisite | Sprint |
|----------|----------------------|-------------|--------|
| | | | |

---

## 12. Story Change Control

### 12.1 Story Lifecycle ⚪

<!--
Define the lifecycle states of a user story.

Expected content:
- States: Draft → Backlog → Ready → In Progress → In Review → Done → Blocked → Removed.
- Transitions and criteria between states.
- Who can move a story between states.
-->

| State | Entry Criteria | Who Moves |
|-------|---------------|-----------|
| Draft | Story statement written | Anyone |
| Backlog | Estimated, DoR partially met | PO |
| Ready | DoR fully met | Scrum Master |
| In Progress | Sprint started, developer assigned | Developer |
| In Review | Code submitted, PR open | Developer |
| Done | DoD fully met | PO (sign-off) |
| Blocked | External dependency or impediment | Developer / Scrum Master |
| Removed | Story no longer needed | PO |

### 12.2 Story Changes ⚪

<!--
Define how stories are changed after baselining.

Expected content:
- Minor changes (AC clarification, no scope change): PO can update directly.
- Moderate changes (new AC, scope expansion within same epic): PO + Tech Lead review.
- Major changes (scope beyond original epic, new NFRs): requires change control per SRS Section 15.
- Story removal: PO decision, documented with rationale.
-->

| Change Type | Criteria | Approval | Documentation |
|-------------|----------|----------|---------------|
| Minor | AC clarification, no scope change | PO | Story comment |
| Moderate | New AC or scope within epic | PO + Tech Lead | Story update + comment |
| Major | Scope beyond epic or new NFRs | Change Control Board | CR per SRS Section 15 |
| Removal | Story no longer needed | PO | Rationale documented |

### 12.3 Story Change Log ⚪

<!--
Log all story changes after baselining.

| CR ID | Date | Story | Change | Reason | Decision |
|-------|------|-------|--------|--------|----------|
| | | | | | |
-->

---

## 13. Appendices

### Appendix A: Full Story Registry

<!--
Complete registry of all user stories with all attributes.

Expected content:
- Every story with full detail: ID, statement, epic, persona, MoSCoW, points, sprint, status, AC count, SRS trace, dependencies.
-->

### Appendix B: Acceptance Criteria Catalog

<!--
Complete catalog of all acceptance criteria.

Expected content:
- Every AC with Given/When/Then format.
- Organized by story, then by epic.
-->

### Appendix C: Traceability Matrix (Stories ↔ SRS ↔ Scope)

<!--
Map stories to SRS requirements and project scope items.

Expected content:
- Every story traces to at least one SRS requirement.
- Every SRS Must Have requirement traces to at least one story.
- Gaps indicate: stories without requirements (untraceable) or requirements without stories (unplanned).
-->

| Story ID | SRS Requirement(s) | Scope Item | Coverage |
|----------|---------------------|-----------|----------|
| | | | <!-- Complete / Partial / Gap --> |

### Appendix D: Parity Story Comparison (🔵🟤)

<!--
Detailed comparison of parity stories vs. legacy features.

Expected content:
- Every legacy feature mapped to its parity story.
- Behavioral comparison per story.
- Parity verification method per story.
-->

### Appendix E: Sprint History & Velocity

<!--
Sprint-by-sprint delivery record.

Expected content:
- Sprint number, dates, stories committed, stories completed, velocity, carry-over, retrospective actions.
-->

### Appendix F: Glossary

| Term | Definition |
|------|-----------|
| | |

---

## Document History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | <!-- date --> | <!-- author --> | Initial template |

---

## Usage Guide

| Icon | Meaning | When Applicable |
|------|---------|-----------------|
| 🟢 | Green Field | All stories are net-new |
| 🟤 | Brown Field | Stories modify existing behavior |
| 🔵 | Software Modernization | Stories include parity, migration, and transition |
| ⚪ | All Types | Applicable to every project type |

**How to use this template:**
1. Start from the User Story Map (Section 2) to establish the delivery backbone.
2. Define Epics (Section 3) aligned with SRS feature areas.
3. Write User Stories (Section 4) with Acceptance Criteria (Section 5) in Given/When/Then format.
4. Every story must trace to at least one SRS requirement (Appendix C).
5. Every Must Have SRS requirement must trace to at least one story — gaps mean unplanned requirements.
6. Use the DoR (Section 9.1) as the gate for sprint entry — no story enters a sprint until Ready.
7. Use the DoD (Section 9.2) as the gate for completion — no story is Done until all criteria pass.
8. Split stories that exceed 8 points or 6 acceptance criteria (Section 10).
9. 🟤🔵: Always specify existing/legacy behavior in modifying and parity stories.
10. Baseline the document once approved — changes go through story change control (Section 12).

**Relationship to Preceding Documents:**
- The SRS answers: *"What must the system do, how well, and how do we verify it?"*
- The User Stories document answers: *"What do users need, in what order, and how do we deliver it incrementally?"*
- User stories translate SRS requirements into delivery-sized units that the team can plan, estimate, and ship sprint by sprint.