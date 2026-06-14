# Skill: Generate Software Architecture

## Description

Generates a complete, rigorous Software Architecture document based on the template `templates/design/software-architecture.md`. The skill deeply analyzes all available project information — preceding analysis documents (viability study, business case, project scope, SRS), user stories, existing documentation, codebase, stakeholder inputs, and any informal requirements artifacts — to populate every applicable section with detailed, justified architectural decisions. The skill **proposes a software stack** and aligns it with the user before finalizing. When gaps, ambiguities, or contradictions are detected in the source material, the skill asks targeted open questions with suggested valid answers before proceeding. The architecture document specifies HOW the system will be built — it translates the SRS's "what the system must do" into concrete technology choices, decomposition strategies, runtime behaviors, deployment models, and cross-cutting concepts.

## Activation

When the user requests to create, generate, or draft a Software Architecture document, architecture design, architecture specification, system architecture, or technical design for a software project.

## Instructions

### Phase 1: Information Gathering & Deep Analysis

1. **Read the template** at `templates/design/software-architecture.md` to understand the full structure, all 14 sections, their subsections, expected content, and project-type applicability (🟢 🟤 🔵 ⚪). Pay special attention to:
   - The Metadata table — project name, type classification, stakeholders.
   - The Executive Summary (Section 1) — must be written last, after all architectural decisions are made.
   - The project type classification (Section 2.2) — 🟢 Green Field, 🟤 Brown Field, 🔵 Software Modernization — and how it determines which sections are applicable.
   - The quality goals (Section 2.4) — these drive architectural decisions and must be specific and measurable.
   - The solution strategy (Section 5) — technology decisions, top-level decomposition, quality goal achievement strategies.
   - The building block view (Section 6) — hierarchical decomposition into components with responsibilities and interfaces.
   - The runtime view (Section 7) — how building blocks interact at runtime in key scenarios.
   - The deployment view (Section 8) — infrastructure and mapping of building blocks to infrastructure.
   - The cross-cutting concepts (Section 9) — security, observability, error handling, etc.
   - The architecture decisions (Section 10) — ADRs with alternatives, rationale, and consequences.
   - The quality requirements (Section 11) — quality scenarios with metrics.
   - The project-type markers throughout: 🟢 = Green Field, 🟤 = Brown Field, 🔵 = Software Modernization, ⚪ = All types.

2. **Discover and read all existing project information:**
   - Search the workspace for any SRS documents (check `documentation`, `docs`, project folders, or any `.md` files with "requirements" or "srs" in the name). If found, read it thoroughly — this is the **most critical** preceding document for architecture. The SRS defines what the system must do; architecture defines how it will do it. Every architectural decision must trace to one or more SRS requirements.
   - Search for any user story documents (check `documentation`, `docs`, project folders, or any `.md` files with "user-stories" or "user_stories" in the name, and any `documentation/user-stories/` folder with individual story files). If found, read them — user stories reveal delivery priorities, dependencies, and incremental delivery requirements that shape the architecture's modularity and deployment strategy.
   - Search for any project scope documents (check `documentation`, `docs`, project folders, or any `.md` files with "project-scope" or "project_scope" in the name). If found, read it — the scope defines boundaries, MoSCoW priorities, and delivery phases that constrain architectural choices.
   - Search for any business case documents. If found, read it — the business case's success criteria, benefit assumptions, and investment constraints inform quality goals and technology investment decisions.
   - Search for any viability study documents. If found, read it — the viability study's technical feasibility assessment, risk analysis, and project type classification shape architectural constraints and risk mitigation strategies.
   - Search for any existing architecture decision records (ADRs), README files, or technical documentation — these may contain prior architectural decisions to preserve or evolve.
   - Search for any configuration files (`package.json`, `pom.xml`, `build.gradle`, `docker-compose.yml`, `terraform/`, `k8s/`, etc.) that reveal the current technology stack, deployment model, and infrastructure.
   - If a codebase exists, explore the directory structure to understand current modules, services, and integrations — this reveals existing architecture for 🟤🔵 projects and constrains new architecture decisions.
   - Search for any stakeholder communication, meeting notes, or decision logs — these may reveal architectural constraints or preferences not captured in formal documents.
   - Search for any API specifications (OpenAPI, Swagger, GraphQL schemas, gRPC proto files) — these define interface contracts that the architecture must accommodate or evolve.
   - Search for any database schemas, data dictionaries, or entity-relationship diagrams — these inform data architecture and persistence decisions.
   - Search for any UI/UX artifacts — wireframes, prototypes, design system references — these inform frontend architecture decisions.
   - Search for any compliance, security, or regulatory documentation — these constrain architecture decisions (data residency, encryption, audit requirements).
   - Search for any infrastructure or deployment documentation — existing CI/CD pipelines, cloud accounts, network topologies.
   - Search for any performance benchmarks, load test results, or capacity plans — these inform quality goal targets.
   - Search for any workflow diagrams, process models, or state machine definitions — these inform runtime view scenarios.

3. **Classify the project type** based on available evidence:
   - **Green Field (🟢)**: New product from scratch — full freedom in technology selection, architectural patterns, and deployment models. Architecture establishes the foundational patterns, conventions, and standards. All 🟢-marked sections are primary.
   - **Brown Field (🟤)**: Existing system enhancement — architecture must fit new components into the existing structure, maintain backward compatibility, and work within the existing technology stack's constraints. All 🟤-marked sections are primary.
   - **Software Modernization (🔵)**: Legacy system migration — architecture must define migration strategy (strangler fig, lift-and-shift, re-architect), transition architecture, dual-running, data migration, and decommission path. All 🔵-marked sections are primary.
   - If a preceding document (viability study, business case, project scope, or SRS) already classified the project type, adopt that classification unless new evidence contradicts it — note any contradiction as a question for Phase 2.
   - If classification is ambiguous, note this as a [Critical] question — the classification determines which sections apply and how architectural decisions are framed.

4. **Map existing information to template sections.** For each of the 14 sections and their subsections, determine:
   - **Covered**: Sufficient information exists to populate the section with evidence-based, architecture-level content.
   - **Partially Covered**: Some information exists but is incomplete, too requirements-level (not yet architectural), or lacks the detail needed for architectural decisions.
   - **Gap**: No information exists for this section.
   - **Contradiction**: Information from different sources conflicts (e.g., SRS requires real-time processing but the scope document assumes batch processing).

5. **Perform deep architecture-readiness analysis.** The architecture document is a design document — it must be precise, justified, and internally consistent. Go beyond surface-level mapping:

   **Preceding document alignment checks:**
   - Does the SRS's functional requirements map cleanly to architectural building blocks, or are there requirements too compound or ambiguous to decompose without clarification?
   - Does the SRS's non-functional requirements provide specific, measurable targets that the architecture can be designed to meet, or are they too vague to derive architectural mechanisms from?
   - Are the user stories' dependencies and delivery sequence consistent with a feasible architectural dependency order (foundations before features)?
   - Are the project scope's delivery phases consistent with an achievable architectural roadmap?
   - Are the business case's success criteria reflected in the architecture's quality goals?
   - Does the viability study's technical feasibility assessment constrain the architecture in ways not captured in the SRS?
   - Are there implicit architectural requirements in the user stories that aren't explicitly stated in the SRS (e.g., stories requiring authentication imply an identity management building block)?

   **Architecture decision readiness checks:**
   - Can the technology stack be proposed based on the SRS's requirements and constraints, or are there too many unknowns to make informed technology choices?
   - Can the top-level decomposition be determined from the SRS's functional areas and user stories' epics, or are there ambiguities in how the system should be structured?
   - Are the quality goals specific enough to derive architectural strategies from (e.g., "99.9% availability" → redundant deployment, health checks, failover), or are they too vague?
   - Are the constraints specific enough to respect (e.g., "must run on Kubernetes" vs. "must be cloud-deployable")?
   - Are there conflicting quality goals that require trade-off decisions (e.g., extreme performance vs. rapid development)?

   **Cross-view consistency pre-checks:**
   - Do the functional requirements imply building blocks that can be independently deployed and scaled, or is a monolithic deployment necessary?
   - Do the user stories' epics map to potential architectural subsystems or bounded contexts?
   - Do the external interfaces from the SRS map to clear integration patterns in the architecture?
   - Do the data requirements suggest a particular data architecture (relational, document, event, graph)?
   - Do the security requirements imply a particular authentication/authorization architecture?

   **Project-type-specific checks:**
   - 🟢 Green Field: Is there enough information to propose a complete technology stack from scratch, or are there too many degrees of freedom? What are the team's skills and preferences — these constrain technology selection?
   - 🟤 Brown Field: Is the existing system's architecture documented precisely enough to understand how new components fit? Are there undocumented dependencies or tribal knowledge about the existing architecture? What is the existing technology stack and its version constraints?
   - 🔵 Modernization: Is the legacy system's architecture understood well enough to plan a migration? What is the existing deployment model? What are the integration points that must be preserved during transition? What is the target end-state architecture?

6. **Propose a software stack** based on the analysis:
   - **Programming language(s)** — consider: team skills, performance requirements, ecosystem maturity, project type constraints.
   - **Backend framework** — consider: productivity, scalability, community support, compatibility with chosen language and quality goals.
   - **Frontend framework** (if applicable) — consider: user interaction complexity, real-time requirements, team expertise.
   - **Database(s)** — consider: data model complexity, read/write patterns, consistency requirements, scalability needs, SRS data requirements.
   - **Messaging / event system** (if applicable) — consider: decoupling requirements, event-driven architecture needs, integration patterns.
   - **Cloud platform / infrastructure** — consider: deployment model, scalability, compliance constraints, cost.
   - **CI/CD tooling** — consider: existing organizational standards, automation requirements.
   - **Observability stack** — consider: monitoring, tracing, logging requirements from quality goals.
   - **Authentication / authorization** — consider: SRS security requirements, compliance constraints, existing organizational identity systems.

   For each technology choice, document: the choice, alternatives considered, rationale (tracing to SRS requirements and quality goals), and any constraints that drove the decision.

7. **Build an architecture readiness map** — for each section, tag readiness:
   - 🟢 **Architecture-Ready**: Information is detailed, specific, and sufficient to make justified architectural decisions.
   - 🟡 **Partially Ready**: Information exists but is too vague, incomplete, or needs architectural interpretation.
   - 🔴 **Not Ready**: Missing, unquantified, or based on unsupported assertions — cannot make architectural decisions without clarification.

   Sections with 🔴 readiness are priority candidates for Phase 2 questions.

### Phase 2: Clarification Questions & Software Stack Alignment

Before generating the document, ask the user targeted questions for every **Partially Covered**, **Gap**, **Contradiction**, or **Not Ready** area identified in Phase 1. **Crucially, also present the proposed software stack for user alignment.**

#### Question Design Principles

- **Ask open questions** that invite thoughtful responses and deeper thinking — not yes/no questions.
- **Always suggest 2–3 possible valid answers** for each question to help the user think through the options and to demonstrate understanding of the domain.
- **Contextualize each question** — briefly explain why the information matters for the architecture and what happens if it remains unanswered (e.g., "Without this, the architecture cannot determine the deployment model, which means the system's scalability and availability characteristics are undefined and the quality goals cannot be achieved").
- **Group questions by template section** so the user can address them systematically.
- **Prioritize questions** — mark questions as:
   - **[Critical]**: Blocks architectural decision-making — the architecture document cannot be generated for this section without this information. The decision would be arbitrary or unjustified.
   - **[Important]**: Affects the quality, justification, or consistency of architectural decisions. Decisions can be made but will have weak rationale or unverified assumptions.
   - **[Optional]**: Refines the architecture but does not block decision-making. Can be documented as an assumption with a validation plan.
- **Reference the source** of the contradiction or gap (e.g., "The SRS defines FR-042 requiring real-time data processing, but the project scope assumes a batch-processing architecture — this creates a fundamental architectural contradiction about the processing model").
- **Surface implicit architectural decisions** — when a requirement or constraint implies an architectural pattern that isn't explicitly stated, propose the implied architecture and ask the user to confirm, challenge, or refine it.
- **Challenge architecture-unfriendly requirements** — when existing information contains requirements that are architecturally unrealistic, contradictory, or overly constrained, flag them and ask for clarification or relaxation.
- **Do not ask questions that can be answered by reading existing documentation** — if the answer exists in a file the skill has already read, use that information directly.
- **Distinguish between information that must be resolved now vs. information that can be documented as assumptions with validation plans** — for [Optional] questions, offer to proceed with a stated assumption.

#### Software Stack Alignment Questions

Present the proposed software stack as a dedicated question block. For each technology choice:

- State the proposed technology.
- State the rationale (tracing to SRS requirements, quality goals, and constraints).
- State the alternatives considered and why they were rejected.
- Ask the user to confirm, challenge, or suggest alternatives.
- If the user's team has specific expertise or preferences that differ from the proposal, adjust the recommendation.

Format the software stack question as:

---

**[Critical] Section 5.1 — Technology Decisions: Proposed Software Stack**

Based on the analysis of the SRS requirements, quality goals, and constraints, the following software stack is proposed. Each choice traces to specific requirements and quality goals. Please review and confirm, challenge, or suggest alternatives for each.

| Layer | Proposed Technology | Rationale | Alternatives Considered | SRS/Quality Goal Trace |
|-------|-------------------|-----------|----------------------|----------------------|
| Language | [proposed] | [rationale] | [alt1, alt2] | [FR-XX, QG-XX] |
| Backend Framework | [proposed] | [rationale] | [alt1, alt2] | [FR-XX, QG-XX] |
| Frontend Framework | [proposed] | [rationale] | [alt1, alt2] | [FR-XX, QG-XX] |
| Primary Database | [proposed] | [rationale] | [alt1, alt2] | [FR-XX, QG-XX] |
| Messaging/Events | [proposed] | [rationale] | [alt1, alt2] | [FR-XX, QG-XX] |
| Cloud/Infrastructure | [proposed] | [rationale] | [alt1, alt2] | [FR-XX, QG-XX] |
| CI/CD | [proposed] | [rationale] | [alt1, alt2] | [FR-XX, QG-XX] |
| Observability | [proposed] | [rationale] | [alt1, alt2] | [FR-XX, QG-XX] |
| Auth/Authz | [proposed] | [rationale] | [alt1, alt2] | [FR-XX, QG-XX] |

Suggested responses:
- *Option A*: "I confirm the proposed software stack — proceed with these technology choices in the architecture document."
- *Option B*: "I want to adjust specific technology choices — [specify which ones and preferred alternatives]."
- *Option C*: "I need more information to decide — provide deeper comparison of alternatives for [specific layers]."
- *Custom*: [your own answer]

---

#### Question Template

For each non-stack question, use this format:

---

**[Priority] Section X.Y — [Topic]**

[Context: Why this matters for the architecture and what happens if unanswered]

[The open question]

Suggested answers:
- *Option A*: [description and implications for architecture]
- *Option B*: [description and implications for architecture]
- *Option C*: [description and implications for architecture]
- *Custom*: [your own answer]

---

#### Minimum Required Questions by Project Type

**All project types** must resolve these before the architecture document can be generated:

- What is the core purpose of the system — what problem does it solve for whom?
- What is the project type classification (🟢 🟤 🔵) and what are its architectural implications?
- What are the top 3–5 quality goals the architecture must satisfy, with specific, measurable targets?
- What are the key constraints (technical, organizational, compliance) that shape the architecture?
- What is the proposed software stack, and does the user align with it?
- What is the top-level decomposition pattern (microservices, modular monolith, layered, event-driven, hexagonal)?
- What external systems does the architecture need to integrate with, and what are the integration patterns?
- What are the key architectural risks and how will they be mitigated?
- What are the deployment model and environment requirements?

**Green Field (🟢) additional questions:**
- What is the complete technology stack proposal — languages, frameworks, databases, infrastructure — and what is the user's alignment?
- What architectural patterns and conventions should be established as the foundation?
- What is the team's expertise and preference — this constrains technology selection more than any other factor?
- What is the initial deployment target (cloud provider, on-premises, hybrid) and what are the scaling expectations?
- What are the foundational building blocks that must be in place before feature development (auth, logging, error handling, data models)?

**Brown Field (🟤) additional questions:**
- What is the existing system's architecture — components, layers, dependencies, data model, deployment?
- Which existing building blocks are in scope for modification, replacement, or extension?
- Which existing building blocks must remain unchanged — what are the backward compatibility constraints?
- What is the existing technology stack and what version constraints apply?
- What undocumented architectural dependencies or tribal knowledge exist in the current system?
- How will the new/modified components integrate with the existing structure — what are the integration points?

**Software Modernization (🔵) additional questions:**
- What is the migration strategy (strangler fig, big bang, phased rollout, parallel run, lift-and-shift)?
- What is the target architecture end-state and what are the intermediate transition states?
- What is the legacy system's architecture — components, data model, integrations, deployment?
- What is the data migration strategy (ETL, CDC, dual-write) and what data is in scope?
- What is the dual-running architecture (if applicable) — how will both systems operate simultaneously?
- What is the rollback strategy for each migration step?
- How and when will the legacy system be decommissioned?

### Phase 3: Document Generation

Once all critical and important questions are resolved and the software stack is aligned with the user, generate the Software Architecture document.

#### Generation Rules

1. **Use the template structure exactly** — follow `templates/design/software-architecture.md` section by section, including all subsections.
2. **Replace all `<!-- -->` placeholders** with project-specific content derived from the analysis and user answers.
3. **Mark sections as [APPLICABLE] or [NOT APPLICABLE]** based on the project type classification. For [NOT APPLICABLE] sections, include a one-line rationale (e.g., "[NOT APPLICABLE] — Green Field project with no existing system to migrate").
4. **For 🟤🔵 sections**, populate them if the project type matches; otherwise mark [NOT APPLICABLE].
5. **Fill every table** with concrete, specific content — no placeholder values remaining in the final document.
6. **Write the Executive Summary (Section 1) last** — after all other sections are complete, synthesize the architectural approach, key decisions, quality goals, constraints, and risks.
7. **Every architectural decision must be justified** — trace it to specific SRS requirements, quality goals, or constraints. Arbitrary choices are not acceptable. The rationale column must reference specific requirement IDs or quality goal scenarios.
8. **Every ADR (Section 10) must include**: title, status, context, decision, alternatives considered with pros/cons, consequences, and compliance mechanism. Use the Michael Nygard ADR format.
9. **Every building block must have**: name, responsibility, interfaces, quality/performance characteristics, and directory/location. Responsibilities must trace to SRS functional requirements.
10. **Every runtime scenario must be architecturally relevant** — focus on scenarios that demonstrate how quality goals are achieved, how building blocks interact in critical paths, and how errors are handled. Don't describe trivial scenarios.
11. **Every cross-cutting concept must be architecturally significant** — only include concepts that affect multiple building blocks and are essential for conceptual integrity. Don't pad with generic content.
12. **Every quality scenario must be specific and measurable** — avoid "the system shall be fast." Write "the system shall process 10,000 orders per minute with p99 latency < 200ms under normal load conditions."
13. **The building block view must be hierarchical** — Level 1 (overall system), Level 2 (zoom into important Level 1 blocks), Level 3 (deep dive into architecturally significant Level 2 blocks). Not every block needs Level 2 or Level 3 detail — prefer relevance over completeness.
14. **The deployment view must map building blocks to infrastructure** — show where each component runs, how they communicate, and what the quality/performance characteristics of the infrastructure are.
15. **The solution strategy (Section 5) must be concise** — it summarizes the fundamental decisions; detailed justification belongs in the ADRs (Section 10). Section 5 references ADRs.
16. **For 🟤🔵: always distinguish between existing and new/modified building blocks** — use the "Existing System Structure" (Section 6.4) and "Transition Building Blocks" (Section 6.5) sections. Mark each existing block's status: unchanged, modified, replaced, or retired.
17. **For 🔵: populate the migration strategy (Section 5.4), migration runtime scenarios (Section 7.3), legacy deployment (Section 8.4), migration-specific concepts (Section 9.7), and migration decision records (Section 10.4)**.
18. **Cross-reference between sections** — when content in one section depends on another, reference it (e.g., "As specified in ADR-001 (Section 10.2), the system uses event-driven architecture; the runtime view (Section 7.1) demonstrates how events flow between building blocks").
19. **Ensure traceability from architecture to SRS** — every building block's responsibility should trace to SRS functional requirements. Every quality goal achievement strategy should trace to SRS non-functional requirements. Every constraint should trace to SRS constraints.
20. **Ensure the proposed software stack is reflected consistently** throughout the document — technology decisions (Section 5.1), building block implementations (Section 6), deployment infrastructure (Section 8), and ADRs (Section 10) must all be consistent with the aligned software stack.
21. **Save the generated document** to `documentation/software-architecture.md` (suggested).

#### Architecture Decision Writing Guidelines

- Use the ADR format (Documenting Architecture Decisions by Michael Nygard).
- Each ADR should have a short noun phrase as title: "ADR-001: Use Event-Driven Architecture for Order Processing."
- Status: Proposed / Accepted / Deprecated / Superseded.
- Context: What is the issue that motivates the decision? Reference specific SRS requirements or quality goals.
- Decision: What is the change or approach chosen? Be specific.
- Alternatives Considered: For each alternative, state pros, cons, and reason for rejection.
- Consequences: What becomes easier or more difficult? Be honest about trade-offs.
- Compliance: How will compliance with this decision be ensured? (Code review, architecture fitness functions, automated checks.)

#### Building Block Description Guidelines

- Each building block must have a clear, singular responsibility.
- Interfaces must be explicit — what does this block expose to other blocks?
- Quality/performance characteristics must reference SRS NFRs where applicable.
- Directory/location should suggest a concrete project structure (e.g., `src/order-service/`, `packages/ui/`).
- Prefer composition over inheritance in the decomposition.
- Building blocks should align with user story epics where possible — this supports independent delivery.
- For 🟤🔵: existing building blocks must have their current status and action (unchanged/modified/replaced/retired).

#### Runtime Scenario Writing Guidelines

- Focus on architecturally relevant scenarios — those that demonstrate:
   - Critical business flows (the "happy path" through the architecture).
   - How quality goals are achieved at runtime (e.g., how the architecture handles high load, how it recovers from failure).
   - How cross-cutting concepts work in practice (e.g., how a request flows through authentication, authorization, business logic, and observability).
   - Error and exception scenarios (how the architecture degrades gracefully).
- Each step should identify the building block, its action, the data exchanged, and error handling.
- For 🟤🔵: include at least one migration runtime scenario showing how a critical flow works during transition.
- Keep scenarios concrete and specific — use real domain entities and actions from the SRS.

#### Quality Checks Before Delivery

After generating the document, perform these self-checks:

- [ ] Every section is either populated with project-specific content or marked [NOT APPLICABLE] with rationale.
- [ ] No `<!-- -->` placeholders remain (except the document status, date, and sign-off fields that require human input).
- [ ] The Executive Summary (Section 1) accurately reflects the full document — architectural approach, key decisions, quality goals, constraints, and risks are correctly summarized.
- [ ] The project type classification in Section 2.2 is consistent with how 🟢🟤🔵 sections are handled throughout the document.
- [ ] Every architectural decision in Section 5.1 and Section 5.2 traces to at least one SRS requirement or quality goal.
- [ ] Every ADR in Section 10 includes: context, decision, alternatives, consequences, and compliance.
- [ ] Every building block in Section 6 has: name, responsibility, interfaces, and quality/performance characteristics.
- [ ] Every building block's responsibility traces to at least one SRS functional requirement.
- [ ] The building block view is hierarchical (Level 1, selected Level 2, optional Level 3).
- [ ] Every runtime scenario in Section 7 is architecturally relevant and includes error handling.
- [ ] The deployment view (Section 8) maps all building blocks to infrastructure elements.
- [ ] Every cross-cutting concept in Section 9 is architecturally significant and not generic boilerplate.
- [ ] Every quality scenario in Section 11 is specific and measurable with metrics/acceptance criteria.
- [ ] Every risk in Section 12 has likelihood, impact, mitigation, and owner.
- [ ] The software stack is consistent throughout the document (technology decisions, building blocks, deployment, ADRs).
- [ ] The glossary (Section 13) covers all architecture-specific terms used in the document.
- [ ] For 🟤🔵: existing system structure (Section 6.4) is documented with status and action for each block.
- [ ] For 🔵: migration strategy (Section 5.4), migration runtime scenarios (Section 7.3), legacy deployment (Section 8.4), migration concepts (Section 9.7), and migration ADRs (Section 10.4) are populated.
- [ ] No contradictions exist between sections (if they do, flag them explicitly).
- [ ] Every constraint in Section 3 is marked as Fixed / Negotiable and its impact on architecture is stated.
- [ ] The stakeholder table (Section 2.5) includes all relevant parties with influence and attitude.
- [ ] References (Section 2.7) include all preceding documents and external standards.

### Phase 4: Post-Generation Review

After the document is generated:

1. **Present the document** to the user.
2. **Highlight key architectural decisions made** during generation — where the skill made interpretive calls (e.g., choosing a specific decomposition pattern, inferring a quality goal target from vague NFRs, proposing an integration pattern not explicitly stated in the SRS), point them out so the user can verify.
3. **Present the architectural summary** clearly — architectural approach, top-level decomposition (number and names of building blocks), technology stack, key ADRs, quality goal achievement strategies, and top risks.
4. **Flag remaining uncertainties** — any areas where information was insufficient and assumptions were made. Indicate the risk each assumption poses to the architecture and suggest validation activities (e.g., proof-of-concept spikes, performance benchmarks, security assessments).
5. **Present the traceability** — show how building blocks map to SRS functional requirements, how quality goals map to architectural strategies, and how constraints map to architectural decisions. Highlight any gaps.
6. **Flag implicit architectural decisions** — decisions that were not explicitly stated in preceding documents but were inferred from requirements, constraints, or best practices. These are the most likely to be contested and should be reviewed carefully.
7. **Identify architectural risks** that require active mitigation — risks that are High or Very High likelihood or Major/Catastrophic impact. Suggest specific mitigation activities.
8. **Offer to refine** any section the user wants to adjust.
9. **Suggest next steps** — e.g., stakeholder architecture review, ADR review session, proof-of-concept for risky decisions, detailed design for specific building blocks, test strategy creation, infrastructure provisioning, CI/CD pipeline setup.

## Examples

### Example Question (Software Stack Alignment — Green Field)

---

**[Critical] Section 5.1 — Technology Decisions: Proposed Software Stack**

Based on the analysis of the SRS requirements, quality goals, and constraints, the following software stack is proposed for this Green Field project. Each choice traces to specific requirements and quality goals. Please review and confirm, challenge, or suggest alternatives for each.

| Layer | Proposed Technology | Rationale | Alternatives Considered | SRS/Quality Goal Trace |
|-------|-------------------|-----------|----------------------|----------------------|
| Language | TypeScript | Full-stack type safety; team expertise; ecosystem maturity for both backend and frontend | Python (weaker type safety), Go (steeper learning curve for current team), Java (heavier footprint) | QG-3 Maintainability, Constraint: team has 80% TypeScript experience |
| Backend Framework | NestJS | Structured, opinionated TypeScript framework with built-in DI, guards, interceptors; aligns with enterprise patterns | Express.js (too unstructured for team size), Fastify (less ecosystem), tRPC (too niche) | FR-001–FR-045 (API layer), QG-1 Performance, QG-3 Maintainability |
| Frontend Framework | React 18+ with Next.js | SSR/SSG for performance; component model aligns with team skills; large ecosystem | Vue.js/Nuxt (less team experience), Angular (heavier, less preferred), Svelte (less ecosystem) | FR-020–FR-035 (UI requirements), QG-1 Performance, QG-4 Usability |
| Primary Database | PostgreSQL 16 | Relational model fits the SRS data requirements (structured entities with relationships); mature; excellent JSON support for semi-structured data | MySQL (less feature-rich for complex queries), MongoDB (data is relational, not document-oriented), DynamoDB (vendor lock-in risk) | FR-007–FR-015 (data requirements), QG-2 Reliability, QG-5 Security |
| Cache Layer | Redis | In-memory caching for session data, frequently queried data, and rate limiting; pub/sub for real-time features | Memcached (no pub/sub, no persistence), Dragonfly (less mature) | NFR-P05 (response time < 200ms), NFR-A01 (session management) |
| Messaging | Apache Kafka | Event-driven decoupling for async workflows; durable message log for audit trail; supports exactly-once semantics | RabbitMQ (less throughput for event streaming), Redis Streams (less mature for this use case), AWS SQS (cloud lock-in) | FR-040–FR-042 (async processing), QG-1 Performance, QG-6 Flexibility |
| Cloud/Infrastructure | AWS (EKS) | Managed Kubernetes for container orchestration; wide service ecosystem; organizational standard | Azure AKS (less organizational experience), GCP GKE (less organizational presence), On-premises (against cloud-first strategy) | Constraint: cloud-first policy, QG-2 Reliability, QG-6 Flexibility |
| CI/CD | GitHub Actions + ArgoCD | GitOps deployment model; declarative infrastructure; aligns with existing GitHub workflow | Jenkins (legacy, higher maintenance), GitLab CI (different SCM platform), CircleCI (less control) | QG-3 Maintainability, organizational standard |
| Observability | OpenTelemetry + Grafana Stack | Vendor-neutral instrumentation; unified metrics/traces/logs; Grafana for visualization | Datadog (vendor lock-in, cost), ELK Stack (heavier operational burden), New Relic (cost) | QG-2 Reliability, QG-7 Observability requirement |
| Auth/Authz | Keycloak | Open-source IAM; OIDC/SAML support; RBAC and ABAC; self-hosted for data residency compliance | Auth0 (SaaS, data residency concerns), AWS Cognito (AWS lock-in), Okta (enterprise cost) | FR-001–FR-005 (auth requirements), NFR-S01 (data residency), QG-5 Security |

Suggested responses:
- *Option A*: "I confirm the proposed software stack — proceed with these technology choices in the architecture document."
- *Option B*: "I want to adjust specific technology choices — [specify which ones and preferred alternatives]."
- *Option C*: "I need more information to decide — provide deeper comparison of alternatives for [specific layers]."
- *Custom*: [your own answer]

---

### Example Question (Gap — No Quality Goals with Measurable Targets)

---

**[Critical] Section 2.4 & 11 — Quality Goals with Measurable Targets**

The SRS states non-functional requirements including "the system should be performant," "the system should be highly available," and "the system should be secure," but does not provide specific, measurable targets. The architecture cannot be designed to meet unquantified quality goals — every architectural mechanism (caching strategy, redundancy level, encryption standard) depends on specific targets. Without measurable targets, architectural decisions are arbitrary and unverifiable.

What are the specific, measurable quality goals the architecture must satisfy?

Suggested answers:
- *Option A*: "Performance: API p99 latency < 200ms under 500 concurrent users; page load time p95 < 2s. Availability: 99.9% uptime measured over rolling 30-day periods (excludes scheduled maintenance). Security: all data in transit encrypted with TLS 1.2+; all PII at rest encrypted with AES-256; OWASP Top 10 compliance verified by penetration test. Maintainability: mean time to change (MTTC) for a single-team feature < 5 days. These targets are based on user experience research, business impact analysis, and regulatory requirements."
- *Option B*: "Performance: initial target of p99 < 500ms under 100 concurrent users (Should Have), with a stretch goal of p99 < 200ms under 500 concurrent users (Could Have). Availability: 99.9% for business hours (08:00–20:00), 99.5% outside business hours. Security: comply with corporate security policy v4.2 (reference attached). Maintainability: no specific target yet — the architecture should support independent team deployment (each team can deploy their service independently). These targets should be validated through a performance testing sprint before architecture finalization."
- *Option C*: "We don't have specific targets yet, but the business case requires: (1) response time competitive with the market leader (measured via benchmarking sprint), (2) 99.9% availability to match the SLA offered to customers, (3) GDPR compliance for EU customer data. The architecture should propose specific targets for these based on industry benchmarks and organizational standards, flag them as assumptions, and note that a quality goal calibration workshop should be held before architecture review."
- *Custom*: [your own answer]

---

### Example Question (Contradiction — Requirements vs. Constraints)

---

**[Critical] Section 3 & 5 — Architectural Contradiction: Performance vs. Deployment Constraint**

The SRS requires NFR-P01 "The system shall process 10,000 orders per minute with p99 latency < 200ms," but the organizational constraint states "all new systems must deploy to the existing on-premises Kubernetes cluster with a maximum of 8 nodes, 32 CPU cores, and 128GB RAM total." Processing 10,000 orders/minute with sub-200ms latency likely requires horizontal scaling beyond 8 nodes, or at minimum requires a capacity analysis to verify feasibility. This creates a fundamental architectural contradiction — the performance requirement may not be achievable within the infrastructure constraint.

How should this contradiction between performance requirements and infrastructure constraints be resolved?

Suggested answers:
- *Option A*: "The infrastructure constraint is negotiable — request an exception to scale the Kubernetes cluster to 16 nodes for production. The architecture should be designed for horizontal scalability (stateless services, shared-nothing architecture) and the deployment view should show the scaled cluster. A capacity planning exercise should validate the node count needed for the target throughput. Present this as a conditional ADR: 'ADR-001: Horizontal scaling on Kubernetes — contingent on infrastructure expansion approval.'"
- *Option B*: "The performance requirement is a stretch goal, not a hard requirement for initial release. The architecture should be designed for horizontal scalability but the initial deployment targets 5,000 orders/minute on the existing 8-node cluster. The quality scenario (Section 11) should specify: 'Initial release: 5,000 orders/min at p99 < 200ms on 8 nodes. Target: 10,000 orders/min at p99 < 200ms — requires infrastructure expansion to 16+ nodes.' This separates the architecture design from the infrastructure constraint."
- *Option C*: "The architecture should optimize for maximum throughput within the 8-node constraint. Techniques: (1) event-driven processing with async order validation, (2) in-memory caching to reduce database load, (3) batch processing for non-critical order steps, (4) connection pooling and query optimization. A performance modeling exercise (using the USL or similar) should estimate achievable throughput before architecture finalization. If modeling shows the target is unreachable, escalate the constraint as a project risk."
- *Custom*: [your own answer]

---

### Example Question (Gap — No Top-Level Decomposition Defined)

---

**[Important] Section 5.2 & 6 — Top-Level Decomposition**

The SRS organizes functional requirements into feature areas (User Management, Order Processing, Inventory, Reporting, Notifications) and user stories are grouped by epics matching these areas. However, no preceding document specifies whether the system should be a monolith, microservices, or something in between. The top-level decomposition is the most fundamental architectural decision — it determines team structure, deployment independence, scalability model, and operational complexity. The user stories' epics suggest natural bounded contexts, but the team size and operational maturity may not support full microservices.

What top-level decomposition pattern should the architecture adopt?

Suggested answers:
- *Option A*: "Modular monolith with domain modules — a single deployable unit with strictly enforced module boundaries (one module per SRS feature area: User Management, Order Processing, Inventory, Reporting, Notifications). Each module has its own domain logic, data access, and API surface. The monolith provides simplicity of deployment and debugging, while the module boundaries prepare for future extraction into microservices if needed. This is appropriate for a team of 4–8 developers who don't yet need independent deployment. ADR-001: 'Modular Monolith with Domain Modules — prioritize simplicity and module boundaries over deployment independence.'"
- *Option B*: "Microservices architecture — one service per bounded context: User Service, Order Service, Inventory Service, Reporting Service, Notification Service. Each service is independently deployable and scalable. Communication via async events (Kafka) for cross-service workflows and sync REST/gRPC for queries. This requires DevOps maturity, observability investment, and a team of 10+ developers. ADR-001: 'Microservices with Domain-Driven Bounded Contexts — prioritize independent deployment and scaling over operational simplicity.'"
- *Option C*: "Backend-for-Frontend (BFF) with modular services — two BFF gateways (web and mobile) over a modular backend. The backend starts as a modular monolith but is structured so that the most volatile or highest-scale modules (Order Processing, Inventory) can be extracted as separate services early. The BFF pattern optimizes the frontend experience while allowing incremental decomposition. ADR-001: 'BFF with Incremental Service Extraction — start with a modular core, extract high-scale services as needed.'"
- *Custom*: [your own answer]

---

### Example Question (Implicit Architecture Decision — Authentication Pattern)

---

**[Important] Section 9.1 — Security Concept: Authentication Architecture**

The SRS defines FR-001 "The system shall authenticate users via corporate SSO (SAML 2.0)" and NFR-S01 "All API endpoints must require authentication." This implies an authentication architecture with: (1) a SAML Service Provider integration with the corporate IdP, (2) token issuance (JWT or opaque tokens) for API authentication, (3) token validation middleware for all API endpoints, (4) role/claim mapping from SAML assertions to application roles. However, no preceding document specifies the authentication architecture — the pattern for bridging SAML SSO to API authentication is an architectural decision that affects every building block.

What authentication architecture pattern should the system use?

Suggested answers:
- *Option A*: "SAML SSO for user-facing login → Keycloak as identity broker (translates SAML to OIDC/JWT) → JWT tokens for API authentication → token validation middleware in the API gateway and/or each service. Keycloak handles the SAML-to-OIDC bridge, user session management, and token refresh. All services validate JWTs locally (no introspection call per request). This is a standard enterprise pattern — ADR-002: 'Use Keycloak as Identity Broker with JWT for API Authentication.'"
- *Option B*: "SAML SSO for user-facing login → custom identity broker within the application (translates SAML assertions to internal session tokens) → session tokens for API authentication → session validation via shared Redis cache. Avoid introducing Keycloak as a new infrastructure dependency — the application handles the SAML integration directly. ADR-002: 'Custom SAML Integration with Redis-Backed Session Tokens.' Simpler infrastructure but more custom code to maintain."
- *Option C*: "Defer authentication architecture to implementation phase — the architecture document should specify the authentication requirements (SAML SSO integration, API authentication, role mapping) as a cross-cutting concern (Section 9.1) without prescribing the implementation pattern. The building block view should include an 'Identity & Access' building block with the required interfaces but without internal decomposition. An ADR for the specific pattern should be created during implementation when the team has more context."
- *Custom*: [your own answer]

---

### Example Question (Brown Field — Existing Architecture Understanding)

---

**[Critical] Section 6.4 & 3.4 — Existing System Architecture**

For this Brown Field enhancement, no documentation was found describing the existing system's architecture — its components, their responsibilities, dependencies, data model, or deployment model. The architecture document must understand the existing structure to specify how new/modified components fit into it. Without this, architectural decisions risk breaking undocumented dependencies or violating implicit contracts.

What is the existing system's architecture — its components, layers, dependencies, and data model?

Suggested answers:
- *Option A*: "The existing system is a layered monolith: Presentation Layer (React SPA), API Layer (Express.js REST API), Business Logic Layer (Node.js services), Data Access Layer (PostgreSQL via Sequelize). There are 4 main modules: User Management, Order Processing, Inventory, and Reporting. The database has 23 tables with foreign key relationships. I can provide the database schema, API endpoint list, and a high-level component diagram. The enhancement targets the Order Processing module specifically."
- *Option B*: "The existing system's architecture is largely tribal knowledge — there is no documentation. The architecture document should include a reverse-engineering phase where the current architecture is captured as Section 6.4 (Existing System Structure) with the status of each building block. The skill should propose an architecture based on the SRS requirements and codebase analysis, but flag all existing-structure assumptions as risks requiring validation. A spike for architecture documentation should precede the architecture review."
- *Option C*: "The existing system is a simple CRUD application with a React frontend and a Node.js/Express backend connected to PostgreSQL. The architecture is straightforward — no microservices, no message queues, no caching. The enhancement adds a workflow engine and notification system, which are net-new components that interact with the existing Order Processing module through its existing API. The existing architecture documentation can be found at [location]."
- *Custom*: [your own answer]

---

### Example Question (Modernization — Migration Strategy)

---

**[Critical] Section 5.4 — Migration Strategy**

The SRS specifies that the modernized system must maintain feature parity with the legacy system, but no preceding document defines the migration approach. The migration strategy determines the entire transition architecture — how the system looks during migration, how data flows between legacy and new, how users are migrated, and how rollback works. This is the most consequential decision for a modernization project.

What migration strategy should the architecture adopt?

Suggested answers:
- *Option A*: "Strangler Fig pattern — incrementally replace legacy components with new ones, routing traffic through an API gateway that directs requests to either the legacy or new system based on feature flags. Migration order: (1) Authentication & User Management, (2) Order Processing, (3) Inventory, (4) Reporting. Each migration step is independently deployable and rollback-capable. Data is migrated using CDC (Change Data Capture) to keep both systems synchronized during transition. The legacy system is decommissioned module by module as each migration step completes. ADR-M001: 'Strangler Fig Migration with CDC for Data Synchronization.'"
- *Option B*: "Phased parallel run — build the entire new system alongside the legacy system, run both in parallel for a validation period (e.g., 30 days), then cutover. During parallel run, all requests go to both systems; the legacy system's responses are authoritative, and the new system's responses are compared for parity validation. Data is migrated in a single ETL batch before the parallel run starts. Rollback: if parity validation fails, the new system is shut down and the legacy system continues. ADR-M001: 'Phased Parallel Run with ETL Data Migration.'"
- *Option C*: "Big bang cutover — build the new system with complete feature parity, migrate all data in a single weekend cutover, switch all traffic to the new system on Monday morning. This is the highest-risk approach but avoids the complexity of dual-running architecture. Rollback: maintain the legacy system in read-only mode for 2 weeks post-cutover; if critical issues arise, fail back to the legacy system within 4 hours. ADR-M001: 'Big Bang Cutover with Hot Standby Rollback.'"
- *Custom*: [your own answer]

---

### Example Question (Vague Quality Goal — Performance Target)

---

**[Important] Section 2.4 & 11.2 — Performance Quality Scenario**

The SRS states NFR-P01 "The system shall respond to user requests within an acceptable timeframe," which is not a measurable quality goal. The architecture must design for a specific performance target — the choice between 200ms and 2 seconds fundamentally changes the architectural approach (caching strategy, database indexing, async processing, CDN placement). Without a specific target, the architecture cannot justify its performance-related decisions.

What is the specific performance target the architecture must satisfy?

Suggested answers:
- *Option A*: "API response time p99 < 500ms for all CRUD operations under 200 concurrent users. Search queries p99 < 1s under the same load. Page load time p95 < 3s (including Time to Interactive). These targets are based on user experience research (500ms is perceived as instantaneous for API interactions, 3s is acceptable for full page loads). The architecture should include: Redis caching for frequently accessed data, database query optimization, connection pooling, and CDN for static assets."
- *Option B*: "Performance should match or exceed the current system's baseline: API p99 currently 1.2s, target p99 < 800ms (33% improvement). Page load currently 5s, target < 3s. The baseline is measured from the production system's monitoring data. The architecture should include: caching strategy (Section 9.4), database optimization, and async processing for long-running operations. These are Should Have targets — if the architecture cannot achieve them within budget, p99 < 1.2s (matching baseline) is acceptable."
- *Option C*: "No specific target exists yet — the architecture should design for 'competitive performance' with placeholder targets: API p99 < 1s under 100 concurrent users, page load p95 < 3s. These are documented as assumptions in Section 3. A performance testing sprint should calibrate realistic targets before the architecture is baselined. The architecture should be designed for horizontal scalability so performance can be improved by adding resources rather than redesigning."
- *Custom*: [your own answer]

---

## Anti-Patterns to Avoid

- **Don't generate the document without asking questions** — the architecture's value is in the rigorous analysis and justified decisions, not in filling a template.
- **Don't propose a software stack without user alignment** — technology choices are the most impactful architectural decisions and must be confirmed by the user.
- **Don't make arbitrary technology choices** — every technology decision must trace to specific SRS requirements, quality goals, or constraints. "I chose React because I like it" is not acceptable rationale.
- **Don't ask questions that existing documentation already answers** — read carefully and use available information directly.
- **Don't ask too many questions at once** — batch by priority, lead with critical questions (especially the software stack), offer to proceed with assumptions for lower-priority items.
- **Don't produce vague quality goals** — "The system shall be highly available" is not a quality goal. "The system shall maintain 99.9% uptime measured over rolling 30-day periods" is.
- **Don't skip the ADRs** — architecture decisions without ADRs are undocumented decisions. Every significant decision must have an ADR with alternatives, rationale, and consequences.
- **Don't skip the building block interfaces** — interfaces between building blocks are among the most critical architectural artifacts. Every building block must document what it exposes.
- **Don't skip the runtime view** — static decomposition alone is insufficient. The runtime view demonstrates how the architecture works in practice under real scenarios.
- **Don't skip the deployment view** — an architecture that isn't deployed isn't real. The deployment view must map building blocks to concrete infrastructure.
- **Don't produce generic cross-cutting concepts** — "Use HTTPS for security" is not an architecture-level concept. "All inter-service communication uses mTLS with certificates managed by cert-manager; API gateway enforces OAuth2 bearer token validation with JWKS rotation every 24 hours" is.
- **Don't duplicate content from the SRS** — the architecture document translates SRS requirements into architectural decisions; it does not restate them. Reference the SRS.
- **Don't mark sections [NOT APPLICABLE] just because they're hard to populate** — only mark them if they genuinely don't apply to the project type.
- **Don't write the Executive Summary first** — write it last, after all architectural analysis is complete and decisions are justified.
- **Don't forget 🟤🔵 sections** — for Brown Field and Modernization projects, the existing system structure, migration strategy, and transition architecture are essential, not optional.
- **Don't forget traceability** — every building block traces to SRS requirements; every ADR traces to quality goals or constraints; every quality scenario traces to NFRs.
- **Don't ignore trade-offs** — every architectural decision has consequences. Document what becomes easier AND what becomes more difficult.
- **Don't confuse architecture with detailed design** — the architecture document captures architecturally significant decisions; detailed design (class diagrams, method signatures, algorithm choices) is left to implementation teams unless it affects cross-cutting concerns.
- **Don't skip risk assessment** — unidentified architectural risks are the most dangerous kind. Every risk with Medium+ likelihood and Moderate+ impact must be documented with mitigation.
- **Don't forget organizational constraints** — team size, team skills, budget, timeline, and development process constrain architecture as much as technical requirements.

## Document Hierarchy Context

The Software Architecture document is the **fifth or sixth** formal document in the project lifecycle, depending on which preceding documents were produced. It builds upon and implements:

| Document | Relationship | Precedes Architecture? |
|----------|-------------|------------------------|
| **Viability Study** | Determines whether the project is feasible — the architecture must be consistent with the viability study's technical feasibility assessment and risk analysis | Yes — the architecture should address the viability study's identified risks and technical constraints |
| **Business Case** | Defines the investment case and recommended option — the architecture must be achievable within the budget and deliver the business case's benefit assumptions | Yes — the architecture's cost must be consistent with the business case's investment envelope |
| **Project Scope** | Defines delivery boundaries — the architecture must support the scope's delivery phases and MoSCoW priorities | Yes — the architecture's modularity must support incremental delivery within scope boundaries |
| **SRS** | Defines what the system must do — the architecture specifies how the system will satisfy those requirements | Yes — every architectural decision traces to SRS requirements |
| **User Stories** | Defines delivery units — the architecture's modularity and building blocks must support the stories' incremental delivery | Yes — building blocks should align with story epics to support independent delivery |

And it precedes:

| Document | Relationship | Follows Architecture? |
|----------|-------------|----------------------|
| **Detailed Design** | Elaborates building blocks into class-level design | Yes — detailed design derives from the architecture's building blocks and interfaces |
| **Sprint Backlogs** | Selects stories for sprint delivery — architecture determines technical dependencies and enabler stories | Yes — stories depend on architectural building blocks |
| **Test Plans** | Verifies quality scenarios from the architecture through test cases | Yes — test plans validate quality goals from Section 11 |
| **Infrastructure Provisioning** | Implements the deployment view (Section 8) | Yes — infrastructure is provisioned based on the deployment architecture |

When generating the architecture document, keep in mind that its primary output is a **complete, justified, and internally consistent set of architectural decisions** that the development team can use to guide implementation. The architecture document is the technical blueprint — it translates requirements into a concrete system structure, technology choices, and quality strategies that enable the team to build the right system in the right way.