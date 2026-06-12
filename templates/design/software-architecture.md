# Software Architecture

> **Template Version:** 1.0  
> **Last Updated:** <!-- date -->  
> **Document Status:** <!-- Draft | Under Review | Approved | Baselined -->

---

## Metadata

| Field                | Value |
|----------------------|-------|
| **Project Name**     | <!-- project name --> |
| **Project Type**     | <!-- Green Field | Brown Field | Software Modernization --> |
| **Sponsor**          | <!-- sponsoring stakeholder or department --> |
| **Product Owner**    | <!-- product owner name --> |
| **Architecture Owner** | <!-- architect or architecture team lead --> |
| **Author(s)**        | <!-- author name(s) --> |
| **Reviewer(s)**      | <!-- reviewer name(s) --> |
| **Date Created**     | <!-- creation date --> |
| **Date Revised**     | <!-- revision date --> |
| **Classification**   | <!-- Public | Internal | Confidential --> |
| **Baseline Version** | <!-- version number once approved --> |
| **Preceding Documents** | <!-- viability study / business case / project scope references --> |

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Introduction and Goals](#2-introduction-and-goals)
3. [Architecture Constraints](#3-architecture-constraints)
4. [Context and Scope](#4-context-and-scope)
5. [Solution Strategy](#5-solution-strategy)
6. [Building Block View](#6-building-block-view)
7. [Runtime View](#7-runtime-view)
8. [Deployment View](#8-deployment-view)
9. [Cross-cutting Concepts](#9-cross-cutting-concepts)
10. [Architecture Decisions](#10-architecture-decisions)
11. [Quality Requirements](#11-quality-requirements)
12. [Risks and Technical Debts](#12-risks-and-technical-debts)
13. [Glossary](#13-glossary)
14. [Appendices](#14-appendices)

---

## 1. Executive Summary

<!-- 
Provide a concise, high-level overview of the software architecture. Write this section last, after all architectural analysis and design is complete.

Expected content:
- A brief statement of the system purpose and the architectural approach taken (2–3 sentences).
- The project type and its architectural implications.
- A summary of the fundamental architectural decisions (technology choices, top-level decomposition, key patterns).
- The top 3–5 quality goals the architecture must satisfy.
- The most significant architectural risks or technical debts.
- Key constraints that shaped the architecture.

Keep this section to 1 page maximum. It must stand alone as a readable summary for stakeholders who need to understand the architectural direction without reading the full document.
-->

| Field | Summary |
|-------|---------|
| **System Purpose** | <!-- 2–3 sentence description of what the system does --> |
| **Project Type** | <!-- Green Field / Brown Field / Software Modernization --> |
| **Architectural Approach** | <!-- e.g., microservices on Kubernetes, event-driven, layered monolith --> |
| **Key Technology Decisions** | <!-- top 3–5 technology choices --> |
| **Top Quality Goals** | <!-- top 3–5 quality attributes with targets --> |
| **Key Constraints** | <!-- top 3–5 constraints shaping the architecture --> |
| **Top Risks / Technical Debts** | <!-- top 3–5 risks or debts --> |

---

## 2. Introduction and Goals

### 2.1 Purpose

<!--
State the purpose of this architecture document and the decisions it supports.

Expected content:
- Why this architecture document exists (e.g., to communicate architectural decisions, to guide development teams, to support governance reviews, to document for long-term maintenance).
- The intended audience (e.g., development team, operations, security, management, auditors).
- What decisions or actions this document enables (e.g., technology selection, team structure, implementation priorities, procurement).
- The relationship to preceding analysis documents (viability study, business case, project scope) — this architecture document translates their requirements and constraints into a concrete technical blueprint.
- The level of detail: this document captures architecturally significant decisions; detailed design is left to implementation teams unless it affects cross-cutting concerns.
-->

### 2.2 Project Type Classification

<!--
Classify the project and explain the implications for the architecture.

**Green Field** — Building a new software product or system from scratch with no existing codebase or legacy constraints.
Architecture focus: technology selection freedom, clean-slate architectural patterns, establishing architectural standards and conventions, defining the complete system structure, choosing deployment and infrastructure models from scratch.

**Brown Field** — Extending, refactoring, or significantly enhancing an existing software system while maintaining backward compatibility and operational continuity.
Architecture focus: fitting new components into the existing structure, managing backward compatibility, identifying refactoring boundaries, minimizing disruption to running systems, working within the constraints of the existing technology stack.

**Software Modernization** — Re-architecting, re-platforming, or migrating a legacy system to modern technologies, architectures, or cloud platforms.
Architecture focus: migration strategy (strangler fig, lift-and-shift, re-architect), feature parity preservation, dual-running architecture, data migration architecture, legacy decommission path, transition states and intermediate architectures.

Mark sections in this template as [APPLICABLE] or [NOT APPLICABLE] based on the project type. Sections marked with icons indicate particular relevance:
- 🟢 = Primarily relevant for Green Field projects
- 🟤 = Primarily relevant for Brown Field projects
- 🔵 = Primarily relevant for Software Modernization projects
- ⚪ = Relevant for all project types
-->

| Attribute | Value |
|-----------|-------|
| **Project Type** | <!-- Green Field / Brown Field / Software Modernization --> |
| **Rationale for Classification** | <!-- why this classification applies --> |
| **Key Implications for Architecture** | <!-- what this means for architectural decisions --> |

### 2.3 Requirements Overview

<!--
Short description of the functional requirements and driving forces that the architecture must support.

Expected content:
- Summary of the essential functional requirements (grouped by feature area or business capability).
- The driving forces behind the project (business goals, market pressures, regulatory mandates).
- Extract or abstract of the requirements — link to the full requirements documents (with version number and information where to find them).
- Reference the project scope document for the detailed scope definition.
- 🟤🔵: Requirements for preserving existing functionality (feature parity) alongside new or changed requirements.
- 🟤🔵: Requirements arising from the migration itself (e.g., data migration, transition, rollback).

Keep these excerpts as short as possible. Balance readability of this document with potential redundancy w.r.t. requirements documents.
-->

| # | Requirement Area | Key Requirements | Source Document | Priority |
|---|-----------------|-------------------|-----------------|----------|
|   |                 |                   |                 |          |

### 2.4 Quality Goals

<!--
The top three (max five) quality goals for the architecture whose fulfillment is of highest importance to the major stakeholders. These are quality goals for the architecture — do not confuse them with project goals.

Consider the ISO 25010 quality categories:
- Functional Suitability
- Performance Efficiency
- Compatibility
- Usability
- Reliability
- Security
- Maintainability
- Flexibility
- Safety

Expected content:
- Each quality goal should be specific and measurable — avoid buzzwords.
- Concrete scenarios that describe what the quality means in practice for this system.
- Ordered by priority — the most important quality goal first.
- 🟤🔵: Quality goals related to migration (e.g., zero-downtime cutover, data integrity during migration).
- Link each quality goal to the stakeholders who care most about it.

Reference: See the Q42 quality model at https://quality.arc42.org for detailed quality attribute definitions.
-->

| # | Quality Goal | Concrete Scenario | Metric / Acceptance Criteria | Priority | Stakeholders |
|---|-------------|-------------------|----------------------------|----------|-------------|
| 1 | <!-- e.g., Performance Efficiency --> | <!-- e.g., The system processes 10,000 orders per minute during peak hours with p99 latency < 200ms --> | | | |
| 2 | | | | | |
| 3 | | | | | |

### 2.5 Stakeholders

<!--
Explicit overview of stakeholders of the system — all persons, roles, or organizations that:
- should know the architecture
- have to be convinced of the architecture
- have to work with the architecture or with code
- need the documentation of the architecture for their work
- have to come up with decisions about the system or its development

Expected content:
- Role or name of each stakeholder.
- Contact information.
- Their expectations with respect to the architecture and its documentation.
- Their influence level (High / Medium / Low).
- Their attitude toward the project (Champion / Neutral / Resistant).
- 🟤🔵: Stakeholders from the legacy system side (current system owners, support teams, users being migrated).

You should know all parties involved in development of the system or affected by the system. Otherwise, you may get nasty surprises later in the development process.
-->

| Role / Name | Contact | Expectations | Influence Level | Attitude |
|-------------|---------|-------------|-----------------|----------|
| | | | | |
| | | | | |

### 2.6 Definitions & Abbreviations

<!--
List terms, acronyms, or abbreviations used throughout the document.

Expected content:
- A table of term/abbreviation and its definition.
- Include architecture-specific terms (e.g., ADR, CQRS, DDD, BFF, SLA, SLO, MTTR, MTBF).
- Include technology-specific terms (e.g., K8s, API GW, IAM, OIDC, RBAC, ABAC).
- Include project-type terms (e.g., strangler fig, lift-and-shift, feature flag, dual-running, feature parity).
- Cross-reference the glossary in Section 13 for the complete list.
-->

| Term / Abbreviation | Definition |
|---------------------|------------|
|                     |            |

### 2.7 References

<!--
List external documents, standards, prior analyses, or data sources referenced.

Expected content:
- Document title, version/date, and location/URL.
- Include the viability study, business case, and project scope that preceded this architecture document.
- Include architecture decision records, API specifications, compliance frameworks.
- Include any vendor documentation or third-party system specifications that constrain the architecture.
- Include relevant architecture frameworks or standards (e.g., arc42, TOGAF, cloud well-architected frameworks).
-->

| Reference | Version / Date | Description | Location |
|-----------|---------------|-------------|----------|
|           |               |             |          |

---

## 3. Architecture Constraints

<!--
Any requirement that constrains software architects in their freedom of design and implementation decisions or decisions about the development process. These constraints sometimes go beyond individual systems and are valid for whole organizations and companies.

Architects should know exactly where they are free in their design decisions and where they must adhere to constraints. Constraints must always be dealt with; they may be negotiable, though.

Expected content:
- Technical constraints (technology mandates, platform restrictions, approved technology lists).
- Organizational constraints (team structure, development process, budget limits, timeline constraints).
- Political constraints (vendor relationships, organizational politics, inter-departmental agreements).
- Conventions (programming guidelines, versioning strategies, documentation requirements, naming conventions).
- Compliance constraints (regulatory requirements, data residency, privacy laws).
- 🟤🔵: Constraints from the existing system (backward compatibility, existing API contracts, data model constraints, vendor lock-in).
- 🟤🔵: Constraints from the migration timeline (hard deadlines, dual-running period limits, contract expirations).

For each constraint, indicate whether it is fixed (non-negotiable) or negotiable.
-->

### 3.1 Technical Constraints ⚪

| # | Constraint | Rationale | Fixed / Negotiable | Impact on Architecture |
|---|-----------|-----------|-------------------|----------------------|
|   |           |           |                   |                      |

### 3.2 Organizational Constraints ⚪

| # | Constraint | Rationale | Fixed / Negotiable | Impact on Architecture |
|---|-----------|-----------|-------------------|----------------------|
|   |           |           |                   |                      |

### 3.3 Conventions ⚪

| # | Convention | Rationale | Applicability | Reference |
|---|-----------|-----------|--------------|-----------|
|   | <!-- e.g., REST API naming conventions --> | | | <!-- link to guidelines --> |

### 3.4 Legacy System Constraints 🟤🔵

<!--
Document constraints imposed by the existing system that the architecture must accommodate.

Expected content:
- Backward compatibility requirements (API contracts that cannot be broken, data formats that must remain supported).
- Technology constraints from the existing stack (frameworks, runtime versions, libraries that cannot be changed).
- Data model constraints (existing schemas, data relationships, data quality issues).
- Vendor lock-in constraints (proprietary technologies, contract terms, licensing restrictions).
- Operational constraints (the system must remain available during migration, maintenance windows).
- Knowledge constraints (tribal knowledge, missing documentation, key-person dependencies).
-->

| # | Legacy Constraint | Source | Fixed / Negotiable | Impact on Architecture | Mitigation |
|---|-----------------|--------|-------------------|----------------------|------------|
|   |                 |        |                   |                      |            |

---

## 4. Context and Scope

<!--
Context and scope delimits your system (i.e. your scope) from all its communication partners (neighboring systems and users, i.e. the context of your system). It thereby specifies the external interfaces.

The domain interfaces and technical interfaces to communication partners are among your system's most critical aspects. Make sure that you completely understand them.

Expected content:
- Context diagrams showing the system as a black box with its communication partners.
- Lists of communication partners and their interfaces.
- Business context: domain-specific inputs and outputs.
- Technical context: channels, protocols, hardware.
-->

### 4.1 Business Context ⚪

<!--
Specification of ALL communication partners (users, IT-systems, ...) with explanations of domain-specific inputs and outputs or interfaces. Optionally add domain-specific formats or communication protocols.

Expected content:
- All kinds of diagrams that show the system as a black box and specify the domain interfaces to communication partners.
- Alternatively (or additionally) a table listing communication partners, their inputs, and their outputs.
- 🟤🔵: Communication partners of both the existing system and the target system — highlight what changes during modernization.
- 🟤🔵: Intermediate communication partners during transition (e.g., synchronization services, event bridges).

Insert a context diagram here (e.g., using C4 System Context diagram, UML use case diagram, or a simple block diagram):
-->

<!-- \<Insert Business Context Diagram\> -->

| Communication Partner | Inputs (from partner to system) | Outputs (from system to partner) | Domain Format / Protocol |
|-----------------------|---------------------------------|----------------------------------|--------------------------|
| | | | |

### 4.2 Technical Context ⚪

<!--
Technical interfaces (channels and transmission media) linking your system to its environment. In addition, a mapping of domain-specific input/output to the channels, i.e. an explanation of which I/O uses which channel.

Expected content:
- Channels and protocols connecting the system to its neighbors.
- Mapping of domain interfaces to technical channels.
- Security mechanisms at each technical interface (authentication, encryption, mTLS).
- 🟤🔵: Technical interfaces during transition (e.g., API gateways routing to both legacy and new system).
- Deployment or infrastructure diagrams showing technical connectivity.

Insert a technical context diagram or deployment diagram here:
-->

<!-- \<Insert Technical Context Diagram\> -->

| Channel | Protocol / Technology | Security | Domain I/O Mapped to This Channel |
|---------|----------------------|----------|-----------------------------------|
| | | | |

### 4.3 External Interface Specifications ⚪

<!--
Detailed specifications of the most important external interfaces.

Expected content:
- For each critical external interface: syntax, semantics, protocols, error handling, restrictions, versions, qualities, necessary compatibilities.
- Link to API documentation (e.g., OpenAPI/Swagger specs) where available.
- 🟤🔵: Interfaces that must remain backward-compatible during transition.
- 🟤🔵: New interfaces introduced during modernization.
- Priority: document interfaces that are architecturally significant or risky; standard or simple interfaces may just reference external documentation.
-->

| Interface | Direction | Protocol / Format | Version | Backward Compat Required? 🟤🔵 | Specification Location |
|-----------|-----------|-------------------|---------|-------------------------------|----------------------|
| | | | | | |

---

## 5. Solution Strategy

<!--
A short summary and explanation of the fundamental decisions and solution strategies that shape the system architecture. These decisions form the cornerstones for your architecture — they are the foundation for many other detailed decisions or implementation rules.

Expected content:
- Technology decisions (programming languages, frameworks, databases, messaging, cloud platform).
- Decisions about the top-level decomposition of the system (e.g., architectural pattern: microservices, monolith, event-driven, layered, CQRS, hexagonal).
- Decisions on how to achieve key quality goals (e.g., how performance targets will be met, how security requirements will be satisfied).
- Relevant organizational decisions (e.g., development process, delegating certain tasks to third parties, team topology).
- 🟢: Full freedom in technology and pattern selection — justify choices against alternatives considered.
- 🟤: How the new or changed components integrate with the existing structure.
- 🔵: Migration strategy (strangler fig, big bang, phased migration, parallel run) and the transition architecture.
- 🔵: How the target architecture will be reached through intermediate states.

Keep the explanations of such key decisions short. Motivate what was decided and why it was decided that way, based upon the problem statement, quality goals, and key constraints. Refer to details in the following sections and to Architecture Decision Records (ADRs) in Section 10.
-->

### 5.1 Technology Decisions ⚪

| # | Decision | Alternatives Considered | Rationale | Affected Quality Goals | ADR Reference |
|---|----------|------------------------|-----------|----------------------|---------------|
|   |          |                        |           |                      |               |

### 5.2 Top-Level Decomposition ⚪

| # | Decision | Alternatives Considered | Rationale | Affected Quality Goals | ADR Reference |
|---|----------|------------------------|-----------|----------------------|---------------|
|   | <!-- e.g., Microservices with domain-driven subdomains --> | <!-- e.g., Modular monolith, layered architecture --> | | | |

### 5.3 Quality Goal Achievement Strategies ⚪

| Quality Goal | Strategy to Achieve It | Architectural Mechanism | Trade-offs Accepted |
|-------------|----------------------|----------------------|-------------------|
| | | | |

### 5.4 Migration Strategy 🔵🟤

<!--
For modernization and brown field projects, describe the overall migration strategy and the transition architecture.

Expected content:
- Migration approach (strangler fig, big bang cutover, phased rollout, parallel run, lift-and-shift followed by refactor).
- Transition architecture: how the system will look in its intermediate states during migration.
- The sequence of migration steps and the target end state.
- How data will be migrated (approach, tooling, validation, cutover).
- How users will be migrated from the legacy system to the new system.
- Rollback strategy for each migration step.
- Dual-running architecture if applicable: how both systems operate simultaneously.
- How and when the legacy system will be decommissioned.
- Feature parity strategy: what is preserved, what is changed, what is retired.
-->

| # | Migration Decision | Rationale | Impact | Rollback Strategy |
|---|-------------------|-----------|--------|-------------------|
|   |                   |           |        |                   |

### 5.5 Organizational Decisions ⚪

| # | Decision | Rationale | Impact on Architecture |
|---|----------|-----------|----------------------|
|   | <!-- e.g., Team topology: stream-aligned teams per subdomain --> | | |

---

## 6. Building Block View

<!--
The building block view shows the static decomposition of the system into building blocks (modules, components, subsystems, classes, interfaces, packages, libraries, frameworks, layers, partitions, tiers, functions, macros, operations, data structures, ...) as well as their dependencies (relationships, associations, ...).

This view is mandatory for every architecture documentation. In analogy to a house this is the "floor plan".

The building block view is a hierarchical collection of black boxes and white boxes:
- Level 1 is the white box description of the overall system together with black box descriptions of all contained building blocks.
- Level 2 zooms into some building blocks of level 1.
- Level 3 zooms into selected building blocks of level 2, and so on.

Prefer relevance over completeness. Specify important, surprising, risky, complex, or volatile building blocks. Leave out normal, simple, boring, or standardized parts.

🟤: Show how new/modified building blocks integrate with the existing structure. Mark existing blocks that are unchanged.
🔵: Show the target building block structure and, if applicable, intermediate transition states.
-->

### 6.1 Whitebox Overall System ⚪

<!--
Describe the decomposition of the overall system at the top level.

Expected content:
- An overview diagram showing the top-level building blocks.
- Motivation for this decomposition.
- Black box descriptions of the contained building blocks.
- Important interfaces that are not explained in the black box templates but are critical for understanding.

Insert the Level 1 overview diagram here (e.g., C4 Container diagram, UML component diagram, or a block diagram):
-->

<!-- \<Insert Level 1 Overview Diagram\> -->

**Motivation:** *\<text explanation of why the system is decomposed this way\>*

**Contained Building Blocks:**

| Name | Responsibility | Interfaces | Quality/Performance Characteristics | Directory/Location |
|------|---------------|------------|------------------------------------|--------------------|
| | | | | |

**Important Interfaces:**

| Interface | Between | Purpose | Protocol / Format |
|-----------|---------|---------|-------------------|
| | | | |

### 6.2 Level 2 — Building Block Details ⚪

<!--
Zoom into selected building blocks from level 1 that are important, complex, risky, or volatile.

For each selected building block, provide:
- An overview diagram of its internal structure.
- Motivation for the decomposition.
- Black box descriptions of contained building blocks.
- Important interfaces.

🟤🔵: For building blocks that exist in the current system, describe what changes and what remains the same.

Copy the following subsection template for each important level-1 building block:
-->

#### 6.2.1 White Box *\<Building Block 1\>*

<!-- \<Insert Level 2 Diagram for Building Block 1\> -->

**Motivation:** *\<why this building block is decomposed this way\>*

**Contained Building Blocks:**

| Name | Responsibility | Interfaces | Quality/Performance Characteristics |
|------|---------------|------------|------------------------------------|
| | | | |

**Important Interfaces:**

| Interface | Between | Purpose | Protocol / Format |
|-----------|---------|---------|-------------------|
| | | | |

#### 6.2.2 White Box *\<Building Block 2\>*

*\<same template as 6.2.1\>*

### 6.3 Level 3 — Deep Dive ⚪

<!--
Zoom into selected building blocks from level 2 when additional detail is architecturally significant.

Only include level 3 when needed — prefer relevance over completeness. Deep dives are justified for building blocks that are:
- Complex or risky
- Critical for achieving quality goals
- Volatile (likely to change)
- Surprising or non-obvious

Copy the following subsection template for each important level-2 building block:
-->

#### 6.3.1 White Box *\<Building Block x.y\>*

<!-- \<Insert Level 3 Diagram\> -->

**Motivation:** *\<why this level of detail is needed\>*

**Contained Building Blocks:**

| Name | Responsibility | Interfaces |
|------|---------------|------------|
| | | |

### 6.4 Existing System Structure 🟤🔵

<!--
For brown field and modernization projects, document the existing system structure that the architecture must accommodate or change.

Expected content:
- The current top-level structure of the existing system (components, modules, layers).
- Which existing building blocks are in scope for modification, replacement, or migration.
- Which existing building blocks remain unchanged.
- Dependencies between existing building blocks that constrain changes.
- Data model of the existing system (if architecturally significant).
- Technical debt in the existing structure.
- Reference to existing documentation if available.
-->

| Existing Building Block | Status | Action | Dependency Constraints |
|------------------------|--------|--------|----------------------|
| | <!-- unchanged / modified / replaced / retired --> | | |

### 6.5 Transition Building Blocks 🔵

<!--
For modernization projects, document the intermediate building blocks that exist only during the transition.

Expected content:
- Synchronization or replication services between legacy and new system.
- API gateways or routers that direct traffic between old and new components.
- Feature flag services or traffic splitting mechanisms.
- Data migration tooling and validation services.
- Dual-running monitoring and reconciliation components.
- Event bridges or message translators between legacy and new system protocols.

These building blocks are temporary — they will be removed once the migration is complete. Document them to ensure they are not forgotten and are properly decommissioned.
-->

| Transition Building Block | Purpose | Lifetime | Decommission Trigger |
|--------------------------|---------|----------|---------------------|
| | | | <!-- e.g., when legacy system is retired --> |

---

## 7. Runtime View

<!--
The runtime view describes concrete behavior and interactions of the system's building blocks in form of scenarios from the following areas:

- Important use cases or features: how do building blocks execute them?
- Interactions at critical external interfaces: how do building blocks cooperate with users and neighboring systems?
- Operation and administration: launch, start-up, stop
- Error and exception scenarios

The main criterion for the choice of possible scenarios (sequences, workflows) is their architectural relevance. It is NOT important to describe a large number of scenarios. You should rather document a representative selection.

Expected content:
- Numbered steps in natural language, or
- Sequence diagrams, activity diagrams, flow charts, BPMN, state machines, or
- Any notation that clearly shows the interaction between building block instances at runtime.

🟤🔵: Include runtime scenarios for the transition period — how requests flow through both legacy and new components.
🟤🔵: Include error and rollback scenarios for the migration.
-->

### 7.1 Runtime Scenario 1: *\<Scenario Name\>* ⚪

<!--
Describe a runtime scenario that is architecturally relevant.

Expected content:
- What triggers the scenario (user action, external event, scheduled job, system start-up).
- The sequence of interactions between building block instances.
- Which data is exchanged at each step.
- Error handling and alternative flows.
- Performance considerations (e.g., expected response time, throughput).
-->

<!-- \<Insert Runtime Diagram or Textual Description\> -->

| Step | Building Block | Action | Data Exchanged | Error Handling |
|------|---------------|--------|----------------|----------------|
| 1 | | | | |
| 2 | | | | |

### 7.2 Runtime Scenario 2: *\<Scenario Name\>* ⚪

*\<same template as 7.1\>*

### 7.3 Migration Runtime Scenario 🔵🟤

<!--
Describe how a critical business flow works during the migration transition — when traffic may route through both legacy and new components.

Expected content:
- How a request flows through the system during the transition period.
- How the API gateway or router decides which system handles the request.
- How data consistency is maintained between legacy and new system during dual-running.
- What happens if the new system fails during transition — rollback flow.
- How the flow changes once the migration step is complete.
-->

<!-- \<Insert Migration Runtime Diagram\> -->

| Step | Building Block | Action | Data Exchanged | Rollback on Failure |
|------|---------------|--------|----------------|---------------------|
| 1 | | | | |

### 7.4 Error and Exception Scenarios ⚪

<!--
Describe architecturally relevant error and exception scenarios.

Expected content:
- How the system handles critical failures (e.g., database unavailability, external service timeout, message queue failure).
- Retry strategies, circuit breaker behavior, fallback mechanisms.
- How errors propagate between building blocks.
- How the system degrades gracefully under failure conditions.
- Monitoring and alerting for critical error conditions.
- 🟤🔵: Error handling during migration — what happens if a migration step fails mid-way.
-->

| Scenario | Failure Mode | Affected Building Blocks | System Response | Recovery Strategy |
|----------|-------------|------------------------|-----------------|-------------------|
| | | | | |

---

## 8. Deployment View

<!--
The deployment view describes:
1. Technical infrastructure used to execute your system, with infrastructure elements like geographical locations, environments, computers, processors, channels and net topologies as well as other infrastructure elements.
2. Mapping of (software) building blocks to that infrastructure elements.

Often systems are executed in different environments, e.g. development environment, test environment, production environment. In such cases you should document all relevant environments.

Especially document a deployment view if your software is executed as a distributed system with more than one computer, processor, server, or container, or when you design and construct your own hardware processors and chips.

🟤🔵: Document the deployment view for both the legacy environment and the target environment, plus the transition deployment if dual-running.
-->

### 8.1 Infrastructure Level 1 ⚪

<!--
Describe the highest-level deployment of the system.

Expected content:
- Distribution of the system to multiple locations, environments, computers, processors, and physical connections between them.
- Important justifications or motivations for this deployment structure.
- Quality and/or performance features of this infrastructure.
- Mapping of software artifacts to elements of this infrastructure.
- For multiple environments or alternative deployments, copy and adapt this section for all relevant environments.

Insert a deployment overview diagram here (e.g., UML deployment diagram, C4 deployment diagram, or infrastructure diagram):
-->

<!-- \<Insert Infrastructure Overview Diagram\> -->

**Motivation:** *\<explanation in text form\>*

**Quality and/or Performance Features:** *\<explanation of infrastructure quality/performance characteristics\>*

**Mapping of Building Blocks to Infrastructure:**

| Building Block | Infrastructure Element | Environment | Notes |
|---------------|----------------------|-------------|-------|
| | | <!-- Dev / Test / Staging / Prod --> | |

### 8.2 Infrastructure Level 2 ⚪

<!--
Here you can include the internal structure of (some) infrastructure elements from level 1.

For each selected infrastructure element, describe:
- Internal structure (sub-elements, network topology, zones).
- Quality and/or performance features.
- Mapping of software building blocks to sub-elements.
-->

#### 8.2.1 *\<Infrastructure Element 1\>*

<!-- \<Insert Diagram + Explanation\> -->

| Sub-Element | Purpose | Building Blocks Mapped | Quality/Performance |
|-------------|---------|----------------------|---------------------|
| | | | |

#### 8.2.2 *\<Infrastructure Element 2\>*

*\<same template as 8.2.1\>*

### 8.3 Environments ⚪

<!--
Describe the different environments the system is deployed to.

Expected content:
- Development, test, staging, pre-production, production environments.
- How environments differ (size, data, configuration, access).
- Which environments are required for the project and who provisions them.
- Environment promotion process (how code moves from dev to production).
- 🟤🔵: Additional environments for migration (e.g., migration test environment, parallel run environment).
-->

| Environment | Purpose | Infrastructure | Data | Access | Provisioned By |
|-------------|---------|---------------|------|--------|---------------|
| Dev | | | | | |
| Test | | | | | |
| Staging | | | | | |
| Prod | | | | | |

### 8.4 Legacy Deployment 🔵🟤

<!--
For modernization and brown field projects, document the current deployment of the existing system.

Expected content:
- Current infrastructure and deployment of the legacy system.
- How the legacy system's deployment constrains the migration.
- The target deployment for the modernized system.
- The transition deployment (dual-running infrastructure if applicable).
- Infrastructure that will be retired when the legacy system is decommissioned.
- Dependencies on legacy infrastructure (shared databases, shared file systems, network zones).
-->

| Deployment Element | Current State | Transition State | Target State | Retirement Timeline |
|-------------------|--------------|-----------------|-------------|---------------------|
| | | | | |

---

## 9. Cross-cutting Concepts

<!--
This section describes cross-cutting concepts (practices, patterns, regulations, or solution ideas). Such concepts are often related to multiple building blocks. They form the basis for conceptual integrity (consistency, homogeneity) of the architecture.

Pick ONLY the most-needed topics for your system and assign each a level-2 heading in this section (e.g., 9.1, 9.2, etc).

DO NOT ATTEMPT to cover all possible cross-cutting topics. Focus on those that are architecturally significant for THIS system.

Common cross-cutting topics include:
- Security and authentication/authorization
- Logging, tracing, and observability
- Error handling and resilience patterns
- Configuration management
- Data access and persistence patterns
- Communication and integration patterns
- Testing strategy and approach
- Domain-driven design patterns

🟤🔵: Cross-cutting concepts that must be consistent between legacy and new system during transition (e.g., same auth mechanism, same logging format).
🟤🔵: Concepts for migration-specific concerns (e.g., data synchronization, feature flag management, dual-running monitoring).
-->

### 9.1 *\<Concept 1 — e.g., Security Concept\>* ⚪

<!--
Describe this cross-cutting concept.

Expected content:
- What the concept is and why it is architecturally important.
- How the concept is implemented consistently across the system.
- Patterns or standards applied.
- Any tooling or frameworks used to enforce the concept.
- 🟤🔵: How this concept applies to both the legacy and new system during transition.
- Examples or references to implementation guidelines.
-->

### 9.2 *\<Concept 2 — e.g., Observability Concept\>* ⚪

*\<same template as 9.1\>*

### 9.3 *\<Concept 3 — e.g., Error Handling & Resilience\>* ⚪

*\<same template as 9.1\>*

### 9.4 *\<Concept 4 — e.g., Data Access & Persistence\>* ⚪

*\<same template as 9.1\>*

### 9.5 *\<Concept 5 — e.g., Integration & Communication\>* ⚪

*\<same template as 9.1\>*

### 9.6 *\<Concept 6 — e.g., Testing Strategy\>* ⚪

*\<same template as 9.1\>*

### 9.7 Migration-Specific Concepts 🔵🟤

<!--
Document cross-cutting concepts that are specific to the migration or transition.

Expected content:
- Data synchronization concept: how data consistency is maintained between legacy and new system during dual-running.
- Feature flag concept: how feature flags are used to control traffic routing and gradual rollout.
- Dual-running monitoring concept: how both systems are monitored and compared during transition.
- Cutover concept: how the switch from legacy to new is executed and validated.
- Rollback concept: how a migration step is reversed if it fails.
-->

| Concept | Description | Applicable To | Transition Duration | Decommission Trigger |
|---------|------------|--------------|--------------------|-----------------------|
| | | | | |

---

## 10. Architecture Decisions

<!--
Important, expensive, large-scale, or risky architecture decisions including rationales. With "decisions" we mean selecting one alternative based on given criteria.

Please use your judgement to decide whether an architectural decision should be documented here in this central section or whether you better document it locally (e.g., within the white box template of one building block).

Avoid redundancy. Refer to Section 5, where you already captured the most important decisions of your architecture.

Expected content:
- Architecture Decision Records (ADRs) for every important decision.
- Each ADR includes: context, decision, status, consequences, and alternatives considered.
- List or table, ordered by importance and consequences, or
- More detailed in form of separate sections per decision.

🟤🔵: Include migration-related architecture decisions (e.g., choice of migration strategy, choice of data migration approach, dual-running approach, rollback strategy).
-->

### 10.1 Architecture Decision Records ⚪

<!--
Use the ADR format (Documenting Architecture Decisions by Michael Nygard) for each important decision.

Each ADR should include:
- Title: A short noun phrase representing the decision.
- Status: Proposed / Accepted / Deprecated / Superseded.
- Context: What is the issue that motivates the decision?
- Decision: What is the change that was made or the approach chosen?
- Alternatives Considered: What other options were evaluated?
- Consequences: What becomes easier or more difficult because of this change?
- Compliance: How will compliance with this decision be ensured?
-->

| ADR # | Title | Status | Date | Consequences | Section Reference |
|-------|-------|--------|------|-------------|-------------------|
| ADR-001 | | <!-- Proposed / Accepted / Deprecated / Superseded --> | | | |
| ADR-002 | | | | | |
| ADR-003 | | | | | |

### 10.2 ADR-001: *\<Decision Title\>*

**Status:** <!-- Proposed / Accepted / Deprecated / Superseded -->

**Context:** *\<What is the issue that motivates this decision?\>*

**Decision:** *\<What is the change that was made or the approach chosen?\>*

**Alternatives Considered:**

| Alternative | Pros | Cons | Reason for Rejection |
|------------|------|------|---------------------|
| | | | |

**Consequences:**

| What Becomes Easier | What Becomes More Difficult |
|---------------------|---------------------------|
| | |

**Compliance:** *\<How will compliance with this decision be ensured?\>*

### 10.3 ADR-002: *\<Decision Title\>*

*\<same template as 10.2\>*

### 10.4 Migration Decision Records 🔵🟤

<!--
Architecture decisions specific to the migration strategy and approach.

Expected content:
- Decision on migration approach (strangler fig vs. big bang vs. phased).
- Decision on data migration strategy (ETL vs. CDC vs. dual-write).
- Decision on dual-running architecture (if applicable).
- Decision on rollback strategy for each migration step.
- Decision on feature parity approach (what is preserved, what is retired).
- Decision on legacy decommission approach and timeline.
-->

| ADR # | Title | Status | Date | Consequences |
|-------|-------|--------|------|-------------|
| ADR-M001 | | | | |
| ADR-M002 | | | | |

---

## 11. Quality Requirements

<!--
This section contains all relevant quality requirements.

The most important of these requirements have already been described in Section 2.4 (quality goals), therefore they should only be referenced here. In this section you should also capture quality requirements with lesser importance, which will not create high risks when they are not fully achieved (but might be nice-to-have).

Since quality requirements will have a lot of influence on architectural decisions you should know what qualities are really important for your stakeholders, in a specific and measurable way.

🟤🔵: Include quality requirements for the migration itself (e.g., data integrity during migration, cutover time window, feature parity completeness).
-->

### 11.1 Quality Requirements Overview ⚪

<!--
An overview or summary of quality requirements.

Expected content:
- Summary of all quality requirement categories applicable to the system.
- Use ISO 25010 categories or the Q42 quality model as a reference structure.
- For each category: a short description of the quality requirement.
- Priority (Must / Should / Could) for each category.
- If these summary descriptions are already precise, specific, and measurable, you may skip Section 11.2.
- 🟤🔵: Include migration quality categories (data integrity, transition availability, rollback speed).
-->

| Quality Category | Requirement Summary | Priority | Related Quality Goal (Section 2.4) |
|-----------------|---------------------|----------|-----------------------------------|
| | | | |

### 11.2 Quality Scenarios ⚪

<!--
Quality scenarios make quality requirements concrete and allow deciding whether they are fulfilled (in the sense of acceptance criteria). Ensure that your scenarios are specific and measurable.

Two kinds of scenarios are especially useful:
- Usage scenarios (runtime reaction to a stimulus): e.g., "The system reacts to a user's request within one second."
- Change scenarios (desired effect of modification or extension): e.g., "Additional functionality is implemented and the effort is less than X person-days."

Expected content (short form — favoured by Q42):
- Context/Background: What kind of system or component, what is the environment?
- Source/Stimulus: Who or what initiates a behaviour, reaction, or action.
- Metric/Acceptance Criteria: A response including a measure or metric.

Expected content (long form — favoured by SEI):
- Scenario ID, Name, Source, Stimulus, Environment, Artifact, Response, Response Measure.
-->

| Scenario ID | Quality Category | Context / Background | Source / Stimulus | Expected Response | Metric / Acceptance Criteria |
|-------------|-----------------|---------------------|-------------------|-----------------|----------------------------|
| QS-001 | | | | | |
| QS-002 | | | | | |
| QS-003 | | | | | |

### 11.3 Migration Quality Scenarios 🔵🟤

<!--
Quality scenarios specific to the migration and transition.

Expected content:
- Data integrity: "During migration of customer data, zero records are lost or corrupted. Validation checks confirm 100% data integrity."
- Transition availability: "During cutover from legacy to new system, total downtime does not exceed 4 hours."
- Feature parity: "At migration completion, 100% of must-have features are available in the new system."
- Rollback: "If migration step 3 fails, the system can be rolled back to the pre-migration state within 1 hour with no data loss."
- Performance during transition: "During dual-running, response time does not degrade by more than 20% compared to pre-migration baseline."
-->

| Scenario ID | Migration Quality | Context / Background | Source / Stimulus | Expected Response | Metric / Acceptance Criteria |
|-------------|-----------------|---------------------|-------------------|-----------------|----------------------------|
| MQS-001 | | | | | |
| MQS-002 | | | | | |

---

## 12. Risks and Technical Debts

<!--
A list of identified technical risks or technical debts, ordered by priority.

"Risk management is project management for grown-ups" (Tim Lister, Atlantic Systems Guild.)

This should be your motto for systematic detection and evaluation of risks and technical debts in the architecture, which will be needed by management stakeholders (e.g. project managers, product owners) as part of the overall risk analysis and measurement planning.

Expected content:
- Technical risks: what could go wrong architecturally and what is the impact?
- Technical debts: what shortcuts were taken, what was deferred, what needs to be addressed later?
- Priority: which risks and debts are most critical?
- Mitigation or remediation: what is the plan for each?
- 🟤🔵: Risks from the existing system (known bugs, fragile components, undocumented behavior).
- 🟤🔵: Risks specific to the migration (data loss, extended dual-running, feature regression, rollback failure).
- 🟤🔵: Technical debts being carried forward or created by the migration.
-->

### 12.1 Technical Risks ⚪

| # | Risk | Likelihood | Impact | Risk Score | Mitigation | Owner | Residual Risk |
|---|------|------------|--------|-----------|------------|-------|---------------|
| | | <!-- Very Low / Low / Medium / High / Very High --> | <!-- Negligible / Minor / Moderate / Major / Catastrophic --> | | | | |

### 12.2 Technical Debts ⚪

| # | Technical Debt | Origin | Impact | Priority | Remediation Plan | Estimated Effort | Target Date |
|---|---------------|--------|--------|----------|-----------------|-----------------|-------------|
| | | <!-- deliberate / inadvertent / legacy --> | | | | | |

### 12.3 Legacy System Risks and Debts 🟤🔵

<!--
Risks and debts originating from the existing system that the architecture must address or carry.

Expected content:
- Fragile components that may break during changes.
- Undocumented behavior or tribal knowledge.
- Known bugs that are being carried forward.
- Performance bottlenecks in the existing system.
- Security vulnerabilities in the existing system.
- Vendor lock-in risks.
- End-of-life technology dependencies.
- Missing test coverage for existing functionality.
-->

| # | Legacy Risk / Debt | System Impact | Migration Impact | Action | Priority |
|---|-------------------|-------------|-----------------|--------|----------|
| | | | | <!-- remediate before migration / accept and carry forward / mitigate during migration --> | |

### 12.4 Migration Risks 🔵🟤

<!--
Risks specific to the migration process and transition.

Expected content:
- Data loss or corruption during migration.
- Extended dual-running period (cost overruns).
- Feature regression (features that work in legacy but fail in new system).
- Performance degradation during transition.
- Rollback failure.
- User resistance to the new system.
- Migration timeline overrun.
- Incomplete data migration.
- Integration failures between legacy and new components during transition.
-->

| # | Migration Risk | Likelihood | Impact | Risk Score | Mitigation | Rollback Strategy | Owner |
|---|---------------|------------|--------|-----------|------------|-------------------|-------|
| | | | | | | | |

---

## 13. Glossary

<!--
The most important domain and technical terms that your stakeholders use when discussing the system.

You can also see the glossary as a source for translations if you work in multi-language teams.

Expected content:
- Term and definition for each important domain and technical term.
- Ensure all stakeholders have an identical understanding of these terms.
- Avoid synonyms and homonyms.
- Include project-type-specific terms 🟤🔵 (e.g., strangler fig, dual-running, feature parity, cutover, rollback).
- Potentially more columns in case you need translations.
-->

| Term | Definition | Synonyms / Translations |
|------|-----------|------------------------|
| | | |

---

## 14. Appendices

### 14.1 Document History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | | | Initial version |

### 14.2 Approval / Sign-off

<!--
List the stakeholders who must approve this architecture document before it is baselined.

Expected content:
- Name, role, and signature/approval status.
- Date of approval.
- Any conditions or reservations noted during approval.
-->

| Name | Role | Approval Status | Date | Conditions / Reservations |
|------|------|----------------|------|--------------------------|
| | | <!-- Approved / Approved with Conditions / Pending / Rejected --> | | |

### 14.3 Diagram and Artifact Index

<!--
List all diagrams and artifacts referenced in or produced as part of this architecture document.

Expected content:
- Diagram name, type, tool/format, and location.
- This helps stakeholders find all visual artifacts and ensures nothing is lost.
-->

| Diagram / Artifact | Type | Section Reference | Tool / Format | Location |
|--------------------|------|-------------------|---------------|----------|
| | <!-- e.g., Context Diagram, Sequence Diagram, Deployment Diagram, ERD --> | | <!-- e.g., draw.io, PlantUML, Lucidchart --> | |

### 14.4 Additional Information

<!--
Any additional information that does not fit into the previous sections.

Expected content:
- Links to external architecture resources, frameworks, or standards used.
- Links to proof-of-concept results or prototypes that validated architectural decisions.
- Links to performance benchmarks or load test results.
- Links to security assessments or threat models.
- Any other supplementary material relevant to the architecture.
-->