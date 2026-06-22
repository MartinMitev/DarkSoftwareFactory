---
name: generate-user-stories
description: Generates a User Stories document (central overview) and individual user story documents (one per story). The skill deeply analyzes all available project information — existing documentation, codebase, stakeholder inputs, and any informal requirements artifacts — to decompose requirements into well-structured, estimable, and deliverable user stories organized by epics. User stories translate the SRS's "what the system must do" into the delivery team's "what do users need, in what order, and how do we deliver it incrementally?"
---

# Skill: Generate User Stories

## Description

Generates a complete, rigorous User Stories document (central overview) and individual user story documents (one per story) based on the template `templates/analysis/user-stories.md`. The skill deeply analyzes all available project information — preceding analysis documents (viability study, business case, project scope, SRS), existing documentation, codebase, stakeholder inputs, and any informal requirements artifacts — to decompose requirements into well-structured, estimable, and deliverable user stories organized by epics. When gaps, unclear statements, or contradictions are detected, the skill asks targeted open questions with suggested valid answers before proceeding. User stories translate the SRS's "what the system must do" into the delivery team's "what do users need, in what order, and how do we deliver it incrementally?"

## Activation

When the user requests to create, generate, or draft user stories, user story document, user story map, backlog, or story breakdown for a software project.

## Instructions

### Phase 1: Information Gathering & Deep Analysis

1. **Read the template** at `templates/analysis/user-stories.md` to understand the full structure, all 13 sections, their subsections, expected content, and project-type applicability (🟢 🟤 🔵 ⚪). Pay special attention to:
   - The user story format (Section 1.3) — "As a [persona], I want [action/capability], so that [benefit/value]." For 🟤🔵 modifying existing behavior: "…where currently [existing behavior]."
   - The story identification scheme (Section 1.4) — EP-XX for epics, US-XXX for stories, AC-XXX for acceptance criteria.
   - The story map structure (Section 2) — backbone of user activities with stories prioritized vertically and sequenced horizontally.
   - The acceptance criteria format (Section 5) — Given/When/Then (BDD/Gherkin) for behavioral criteria.
   - The Definition of Ready (Section 9.1) and Definition of Done (Section 9.2) — the gates for sprint entry and completion.
   - The story splitting guide (Section 10) — when and how to split stories.
   - The usage guide at the end — user stories answer "What do users need, in what order, and how do we deliver it incrementally?"

2. **Discover and read all existing project information:**
   - Search the workspace for any SRS documents (check `documentation`, `docs`, project folders, or any `.md` files with "requirements" or "srs" in the name). If found, read it thoroughly — this is the **most critical** preceding document for user stories. Every story must trace to at least one SRS requirement.
   - Search for any project scope documents (check `documentation`, `docs`, project folders, or any `.md` files with "project-scope" or "project_scope" in the name). If found, read it — the scope defines delivery boundaries, phases, and MoSCoW priorities that drive story prioritization and sequencing.
   - Search for any business case documents. If found, read it — the business case's success criteria and benefit assumptions inform story value propositions and priority.
   - Search for any viability study documents. If found, read it — the viability study's risk assessment informs story risk and sequencing.
   - Search for any existing user stories, backlog items, or feature lists — these may contain story drafts to refine.
   - Search for any architecture decision records (ADRs), README files, or technical documentation — these inform technical notes and dependencies.
   - Search for any configuration files (`package.json`, `pom.xml`, `build.gradle`, `docker-compose.yml`, etc.) that reveal the technology stack — this informs technical notes and constraints.
   - If a codebase exists, explore the directory structure to understand current modules, services, and integrations — this reveals existing behavior for 🟤🔵 stories.
   - Search for any stakeholder communication, meeting notes, user research, interview summaries, or survey data — these reveal user needs and personas.
   - Search for any API specifications (OpenAPI, Swagger, GraphQL schemas, gRPC proto files) — these reveal interface-related stories.
   - Search for any database schemas, data dictionaries, or entity-relationship diagrams — these reveal data-related stories.
   - Search for any UI/UX artifacts — wireframes, prototypes, design system references — these inform UI stories and acceptance criteria.
   - Search for any workflow diagrams, process models, or state machine definitions — these reveal workflow stories.
   - Search for any existing test plans or test case documents — these reveal implicit requirements to cover with stories.
   - Search for any incident reports, support ticket data, or bug databases — these reveal pain points that may need stories.

3. **Classify the project type** based on available evidence:
   - **Green Field (🟢)**: All stories are net-new; full freedom in sequencing and splitting.
   - **Brown Field (🟤)**: Stories include new behavior, modifications to existing behavior, and regression-safe changes; must reference existing system behavior.
   - **Software Modernization (🔵)**: Stories include feature parity stories (behavior preservation), new platform stories, and migration transition stories; must reference legacy behavior.
   - If a preceding document (viability study, business case, project scope, or SRS) already classified the project type, adopt that classification unless new evidence contradicts it — note any contradiction as a question for Phase 2.
   - If classification is ambiguous, note this as a [Critical] question — the classification determines how stories are framed (net-new vs. modifying vs. parity) and which sections apply.

4. **Map existing information to template sections.** For each of the 13 sections and their subsections, determine:
   - **Covered**: Sufficient information exists to populate the section with evidence-based, story-level content.
   - **Partially Covered**: Some information exists but is incomplete, too high-level for story decomposition, or lacks user-value articulation.
   - **Gap**: No information exists for this section.
   - **Contradiction**: Information from different sources conflicts (e.g., SRS defines a requirement that the scope document excludes, or personas differ between documents).

5. **Perform deep story-readiness analysis.** User stories are delivery units — they must be small enough to estimate, specific enough to test, and valuable enough to deliver independently. Go beyond surface-level mapping:

   **Preceding document alignment checks:**
   - Does the SRS's functional requirements map cleanly to user stories, or are there requirements too compound to fit in a single story (must be split)?
   - Does the SRS's non-functional requirements map to story-level acceptance criteria, or are they too system-level to be verified per-story?
   - Are the project scope's delivery phases consistent with the story map's release alignment (Section 2.2)?
   - Are the business case's success criteria reflected in story-level value propositions and acceptance criteria?
   - Do the MoSCoW priorities in the scope/SRS translate consistently to story priorities?
   - Does the scope's out-of-scope items prevent certain stories from being written?

   **Story decomposition readiness checks:**
   - Can each SRS functional requirement be expressed as one or more user stories using the standard format? If a requirement doesn't naturally fit a user story (e.g., infrastructure, compliance), can it be reframed as an enabler story?
   - Are the user personas from the SRS complete enough to write stories for, or are there undefined personas?
   - Are the business rules from the SRS specific enough to derive acceptance criteria from, or are they too vague for Given/When/Then?
   - Are the use cases from the SRS decomposable into story-sized pieces, or do they span too much for a single sprint?
   - Are the data requirements from the SRS covered by stories, or do data entities need their own stories (e.g., data migration, data validation)?

   **Cross-story consistency checks:**
   - Do the identified epics group related stories that deliver a cohesive capability, or are they arbitrary?
   - Are story dependencies identifiable from the SRS's requirement dependencies and use case workflows?
   - Are there stories implied by the SRS's use cases or workflows that are not explicitly stated as requirements?
   - Are there stories implied by the architecture or integration landscape that are not in the SRS?
   - Do the NFRs from the SRS affect specific stories, and can they be expressed as story-level acceptance criteria?

   **Project-type-specific checks:**
   - 🟢 Green Field: Are all user-system interactions covered by stories, or are there gaps where the system must respond but no story exists? Are foundation/enabler stories included (auth, logging, error handling)?
   - 🟤 Brown Field: Are existing behavior baselines documented for every story that modifies existing functionality? Are regression-risk stories included? Are backward compatibility stories needed?
   - 🔵 Modernization: Are feature parity stories identified for every legacy feature that must be replicated? Are data migration stories included? Are transition/dual-running stories included? Are decommission stories included?

6. **Build a story readiness map** — for each section, tag readiness:
   - 🟢 **Story-Ready**: Information is detailed, user-value-articulated, and sufficient to write well-structured stories with acceptance criteria.
   - 🟡 **Partially Ready**: Information exists but needs decomposition into stories, user-value articulation, or acceptance criteria definition.
   - 🔴 **Not Ready**: Missing, too high-level, or based on unsupported assertions — cannot derive well-structured stories without clarification.

   Sections with 🔴 readiness are priority candidates for Phase 2 questions.

### Phase 2: Clarification Questions

Before generating the documents, ask the user targeted questions for every **Partially Covered**, **Gap**, **Contradiction**, or **Not Ready** area identified in Phase 1.

#### Question Design Principles

- **Ask open questions** that invite thoughtful responses and deeper thinking — not yes/no questions.
- **Always suggest 2–3 possible valid answers** for each question to help the user think through the options and to demonstrate understanding of the domain.
- **Contextualize each question** — briefly explain why the information matters for user stories and what happens if it remains unanswered (e.g., "Without this, the user story cannot define the persona's benefit, which means the story's value proposition is undefined and the team cannot prioritize it against other stories").
- **Group questions by template section** so the user can address them systematically.
- **Prioritize questions** — mark questions as:
   - **[Critical]**: Blocks story creation — user stories cannot be written for this area without this information. The story would be unverifiable or ambiguous.
   - **[Important]**: Affects the quality, completeness, or testability of stories. Stories can be drafted but will have gaps or weak acceptance criteria.
   - **[Optional]**: Refines the stories but does not block creation. Can be documented as an assumption with a validation plan.
- **Reference the source** of the contradiction or gap (e.g., "The SRS defines FR-042 'password reset' but the project scope excludes 'self-service account management' — this creates a contradiction about whether password reset stories should be included").
- **Surface implicit stories** — when a use case, workflow, or data model implies a user need that isn't explicitly stated as a requirement, propose the implied story and ask the user to confirm, challenge, or refine it.
- **Challenge vague value propositions** — when existing information doesn't articulate *why* a user needs something, flag it and ask for the benefit/value.
- **Challenge overly large stories** — when a requirement or feature area is too large for a single story, suggest splitting approaches and ask which pattern to use.
- **Do not ask questions that can be answered by reading existing documentation** — if the answer exists in a file the skill has already read, use that information directly.
- **Distinguish between information that must be resolved now vs. information that can be documented as assumptions with validation plans** — for [Optional] questions, offer to proceed with a stated assumption.

#### Question Template

For each question, use this format:

---

**[Priority] Section X.Y — [Topic]**

[Context: Why this matters for user stories and what happens if unanswered]

[The open question]

Suggested answers:
- *Option A*: [description and implications for stories]
- *Option B*: [description and implications for stories]
- *Option C*: [description and implications for stories]
- *Custom*: [your own answer]

---

#### Minimum Required Questions by Project Type

**All project types** must resolve these before user stories can be generated:

- Who are the primary user personas, and what are their key goals with the system?
- What are the top-level feature areas (potential epics) the system must support?
- What are the MoSCoW priorities for the main feature areas?
- What is the delivery timeline and release strategy (MVP first, then phases)?
- What are the most critical user workflows that must be supported?
- What sprint length and team size are assumed for estimation?
- What is the project type classification and how should it affect story framing?

**Green Field (🟢) additional questions:**
- What are all the user-system interactions the system must support — every way a user initiates contact with the system?
- What foundation/enabler stories are needed before feature stories can be built (e.g., auth, logging, error handling, data models)?
- What constitutes the MVP — the minimum set of stories that delivers value to users?
- Are there stories for setting up the development environment, CI/CD, and infrastructure?

**Brown Field (🟤) additional questions:**
- For each story that modifies existing behavior, what is the precise current behavior that must be preserved or changed?
- What backward compatibility stories are needed (e.g., API versioning, data migration for schema changes)?
- What regression-risk stories are needed to ensure existing functionality isn't broken?
- Are there undocumented behaviors (tribal knowledge, workarounds) that need stories to preserve them?

**Software Modernization (🔵) additional questions:**
- What is the feature parity target at migration cutover — 100% behavioral parity, or is partial parity acceptable for specific features?
- For each feature being migrated, what are the parity stories (replicate behavior) vs. enhancement stories (new behavior)?
- What data migration stories are needed, and what data entities are in scope?
- What transition stories are needed (dual-running, feature flags, cutover, rollback)?
- What decommission stories are needed for the legacy system?
- What is the rollback strategy, and does it need a story?

### Phase 3: Document Generation

Once all critical and important questions are resolved, generate **two types of documents**:

1. **Individual User Story Documents** — one separate document per user story, saved in a dedicated folder.
2. **Central User Stories Overview Document** — the full document following the template structure.

#### Individual User Story Document Generation

For each user story, create a standalone document containing:

```markdown
# US-XXX: [Story Title]

## Story Statement

As a [persona], I want [action/capability], so that [benefit/value].

## Existing Behavior 🟤🔵

<!-- For Brown Field / Modernization: what the current system does -->
<!-- For Green Field: "N/A — net-new capability" -->

## Attributes

| Attribute | Value |
|-----------|-------|
| **Story ID** | US-XXX |
| **Epic** | EP-XX |
| **MoSCoW** | Must / Should / Could |
| **Story Points** | 1 / 2 / 3 / 5 / 8 / 13 |
| **Sprint / Release** | Sprint X / Release Y |
| **SRS Trace** | FR-XXX, NFR-XXX |
| **Dependencies** | US-XXX must be done first |
| **Technical Notes** | implementation hints |
| **Questions / Unknowns** | open questions |
| **Status** | Backlog |

## Acceptance Criteria

| AC ID | Criterion | Given | When | Then |
|-------|-----------|-------|------|------|
| US-XXX.AC-1 | description | precondition | action | expected result |
| US-XXX.AC-2 | description | precondition | action | expected result |

## Parity Information 🟤🔵

<!-- For Modernization/Brown Field stories only -->
| Attribute | Value |
|-----------|-------|
| **Legacy Feature** | name of legacy feature |
| **Legacy Behavior** | what the legacy system does |
| **New Behavior** | what the new system does |
| **Parity Level** | 100% / Partial |
| **Behavioral Differences** | intentional differences |
| **Verification Method** | parallel test / automated comparison / manual UAT |

## Story Splits

<!-- If this story was split from a larger story, reference the parent -->
<!-- If this story may need further splitting, note the trigger and suggested pattern -->
- **Parent Story**: N/A or US-XXX
- **Split Trigger**: N/A or "exceeds 8 points / more than 6 AC / multiple personas"
- **Suggested Split Pattern**: N/A or "by workflow step / by persona / by data"
```

#### Central User Stories Document Generation

Generate the central overview document following the template structure.

##### Generation Rules

1. **Use the template structure exactly** — follow `templates/analysis/user-stories.md` section by section, including all subsections.
2. **Replace all `<!-- -->` placeholders** with project-specific content derived from the analysis and user answers.
3. **Mark sections as [APPLICABLE] or [NOT APPLICABLE]** based on the project type classification. For [NOT APPLICABLE] sections, include a one-line rationale (e.g., "[NOT APPLICABLE] — Green Field project with no existing system to migrate").
4. **For 🟤🔵 sections**, populate them if the project type matches; otherwise mark [NOT APPLICABLE].
5. **Fill every table** with concrete, specific content — no placeholder values remaining in the final document.
6. **Write the Introduction (Section 1) and Story Map (Section 2) after** all stories are defined — these synthesize the story landscape and must reflect the complete story set.
7. **Every user story must follow the standard format**: "As a [persona], I want [action], so that [benefit]."
   - The persona must match a defined user persona (from SRS Section 3.1 or project scope).
   - The action must be specific and testable.
   - The benefit must articulate measurable or observable value.
   - For 🟤🔵: stories modifying existing behavior use the format: "As a [persona], I want [changed behavior], so that [improved value], where currently [existing behavior]."
8. **Every story must be singular** — one deliverable unit of user value per story. If a story contains "and" joining two distinct capabilities, split it.
9. **Every story must be estimable** — the team must be able to assign story points. If a story is too large or uncertain to estimate, flag it for splitting or a spike.
10. **Every story must be testable** — it must have at least one acceptance criterion in Given/When/Then format.
11. **Every story must trace to at least one SRS requirement** — populate the traceability matrix (Appendix C) to verify this. Every Must Have SRS requirement must trace to at least one story — gaps mean unplanned requirements.
12. **Every story must be prioritized** using MoSCoW (Must Have / Should Have / Could Have).
13. **Stories estimated at 8+ points should be flagged for splitting** per Section 10 — either split them or document why they cannot be split (with a plan to manage the risk).
14. **Stories with more than 6 acceptance criteria should be flagged for splitting** per Section 10.
15. **Ensure epics group related stories** that deliver a cohesive capability. Each epic should align with a feature area from the SRS or project scope.
16. **Ensure the story map (Section 2) covers the full scope** — every user activity from the SRS's use cases should appear in the story map backbone.
17. **Ensure dependencies (Section 7) are explicit** — hard dependencies, soft dependencies, and external dependencies must all be identified.
18. **For 🟤🔵: always specify existing/legacy behavior** in modifying and parity stories. Use the "where currently [existing behavior]" clause.
19. **For 🔵: populate migration & transition stories (Section 11)** with feature parity stories, data migration stories, transition stories, and decommission stories.
20. **Save the central document** to `documentation/user-stories.md` (suggested).
21. **Save individual user story documents** to `documentation/user-stories/US-XXX.md` (suggested — one file per story, where XXX is the zero-padded story number).
22. **Cross-reference between the central document and individual story documents** — the central document's detailed story specifications (Section 4.2) should link to the individual story files, and the individual files should reference their epic and the central document.

#### Acceptance Criteria Writing Guidelines

- Use Given/When/Then (BDD/Gherkin) format for behavioral criteria.
- Each criterion must be: testable, unambiguous, and independent.
- Every story must have at least one acceptance criterion.
- Must Have stories require comprehensive criteria covering: happy path, error handling, and edge cases.
- Could Have stories may have lighter criteria (happy path only).
- For 🟤🔵: parity criteria must specify the exact behavior from the legacy system that must be preserved.
- NFRs relevant to a story should be included as additional acceptance criteria (e.g., "Given 100 concurrent users, When search is performed, Then response time is < 200ms at p99").

#### Quality Checks Before Delivery

After generating all documents, perform these self-checks:

- [ ] Every section of the central document is either populated with project-specific content or marked [NOT APPLICABLE] with rationale.
- [ ] No `<!-- -->` placeholders remain in the central document (except the document status, date, and sign-off fields that require human input).
- [ ] Every user story has an individual document file in the `documentation/user-stories/` folder.
- [ ] Every individual story document contains: story statement, attributes, acceptance criteria, and traces.
- [ ] The story map (Section 2) covers all user activities from the SRS use cases.
- [ ] The release-aligned story map (Section 2.2) is consistent with the project scope's delivery phases.
- [ ] Story map traceability (Section 2.3) shows complete coverage — no gaps.
- [ ] Every epic in Section 3 groups related stories and traces to SRS feature areas.
- [ ] Every story in Section 4 follows the standard format and is singular, estimable, and testable.
- [ ] Every story traces to at least one SRS requirement (Appendix C).
- [ ] Every SRS Must Have requirement traces to at least one story — no uncovered Must Have requirements.
- [ ] Every acceptance criterion is in Given/When/Then format and is testable.
- [ ] NFRs from the SRS are mapped to affected stories (Section 6) and integrated as ACs where appropriate.
- [ ] Story dependencies (Section 7) are explicit — hard, soft, and external.
- [ ] Critical path stories (Section 7.2) are identified with risk and mitigation.
- [ ] Stories ≥ 8 points or > 6 ACs are flagged for splitting (Section 10).
- [ ] The Definition of Ready (Section 9.1) and Definition of Done (Section 9.2) are concrete and actionable.
- [ ] For 🟤🔵: existing behavior is specified in all modifying stories.
- [ ] For 🔵: migration & transition stories (Section 11) are populated with parity, data migration, transition, and decommission stories.
- [ ] Story points are assigned using Fibonacci (1, 2, 3, 5, 8, 13).
- [ ] MoSCoW priorities are consistent with the SRS/project scope priorities.
- [ ] The change control process (Section 12) defines approval authority at each impact level.
- [ ] No contradictions exist between sections (if they do, flag them explicitly).
- [ ] Individual story documents and the central document are cross-referenced.

### Phase 4: Post-Generation Review

After all documents are generated:

1. **Present the central document** and explain the individual story document structure.
2. **Highlight key judgments made** during generation — where the skill made interpretive calls (e.g., decomposing a compound requirement into multiple stories, choosing story splitting patterns, inferring implicit stories from use cases, assigning MoSCoW priorities where they were unspecified, grouping stories into epics), point them out so the user can verify.
3. **Present the story summary** clearly — total story count, total story points, epic distribution, MoSCoW distribution, stories per release/phase.
4. **Flag remaining uncertainties** — any areas where information was insufficient and assumptions were made. Indicate the risk each assumption poses to the stories and suggest validation activities.
5. **Present the traceability coverage** — show the traceability matrix from Appendix C, highlighting any gaps that remain (stories without requirements, requirements without stories).
6. **Flag implicit stories discovered** — any stories that were not explicitly stated in preceding documents but were inferred from use cases, data models, business rules, or workflows. These are the most likely to be contested and should be reviewed carefully.
7. **Identify stories at risk of splitting** — any stories ≥ 8 points or > 6 ACs that were included but should be considered for decomposition.
8. **Offer to refine** any section or individual story the user wants to adjust.
9. **Suggest next steps** — e.g., backlog refinement session, sprint planning, architecture design (using `templates/design/software-architecture.md`), test plan creation from acceptance criteria, stakeholder review of story priorities, estimation workshop.

## Examples

### Example Question (Gap — No SRS Exists)

---

**[Critical] Section 4 & 5 — User Stories and Acceptance Criteria**

No Software Requirements Specification was found for this project. The SRS is the primary source for user stories — every story must trace to at least one SRS requirement. Without it, stories risk being untraceable, incomplete, or misaligned with system requirements. The user stories document translates the SRS's "what the system must do" into delivery-sized units.

What are the detailed requirements this project must satisfy, and how can they be decomposed into user stories?

Suggested answers:
- *Option A*: "An SRS exists but is located elsewhere — I can provide the path or content. The skill should read it and derive stories from its functional requirements, use cases, and business rules."
- *Option B*: "No SRS exists yet. The skill should generate the user stories based on the project scope and business case, noting each story's traceability to scope items rather than SRS requirements. The SRS traceability column (Appendix C) will show 'Scope Item: SI-XX' instead of 'FR-XXX'. A recommendation to create the SRS first should be included."
- *Option C*: "No SRS exists and the project scope is the most detailed document available. The skill should derive stories from the scope's deliverables and requirements sections, but flag this as a risk — stories without SRS traceability may miss implicit requirements. Each story should include a 'Questions / Unknowns' field noting that SRS traceability is pending."
- *Custom*: [your own answer]

---

### Example Question (Partial Information — Vague Persona)

---

**[Important] Section 4.2 — Story Persona Definition**

The SRS defines "User" as the primary persona but does not distinguish between different user roles (e.g., admin, end-user, manager). User stories require specific personas to articulate distinct value propositions — "As a user, I want to manage settings" is vague; "As an administrator, I want to configure system-wide settings" vs. "As an end-user, I want to customize my preferences" are precise and testable.

What are the distinct user personas and their key goals with the system?

Suggested answers:
- *Option A*: "Three personas: (1) Administrator — manages system configuration, user accounts, and audit logs; (2) Manager — views reports, approves requests, and manages team assignments; (3) End User — performs daily tasks, submits requests, and views own data. Each persona has distinct permissions and workflows. Stories should be written for each persona separately."
- *Option B*: "Two personas: (1) Admin — full system access including configuration and user management; (2) User — self-service capabilities including profile management, task execution, and report viewing. Manager role is deferred to a later release — current stories focus on Admin and User."
- *Option C*: "The SRS's 'User' persona is intentionally generic at this stage. The stories should use 'User' as the persona initially, but include a note in each story's 'Questions / Unknowns' field identifying that persona refinement is needed. An epic for 'Role-Based Access Control' should be added to formalize personas in a future sprint."
- *Custom*: [your own answer]

---

### Example Question (Contradiction — Scope vs. SRS)

---

**[Critical] Section 4 & Appendix C — Story Coverage vs. Scope Exclusions**

The SRS includes FR-025 "The system shall provide a real-time notification system for order status changes," but the project scope document explicitly excludes "real-time notifications" from Phase 1 and lists them as "Won't Have This Time." This contradiction affects whether stories for FR-025 should be written as Must Have, Could Have, or excluded entirely. The user stories document must resolve this — either the SRS is authoritative (stories are written) or the scope is authoritative (stories are deferred).

Should stories for the real-time notification feature be included in the current scope, or are they explicitly deferred?

Suggested answers:
- *Option A*: "Scope is authoritative — real-time notifications are Won't Have This Time. Do not write stories for FR-025 in this iteration. Note in Appendix C that FR-025 is 'In Scope — Deferred' with traceability to the scope document's exclusion. The SRS requirement remains valid but is not planned for delivery now. If the SRS needs updating, that is a separate change control action."
- *Option B*: "SRS is authoritative — the requirement exists and must be covered by stories. However, given the scope exclusion, write the stories as 'Could Have' with a note that they are planned for a future release. The story map (Section 2.2) assigns them to Phase 2 or later. This ensures traceability while respecting the scope boundary."
- *Option C*: "The contradiction must be resolved by the Product Owner — I will include stories for FR-025 but flag them as 'Blocked — scope contradiction' in the status field. The stories are written for traceability but cannot enter a sprint until the scope/SRS conflict is resolved through change control."
- *Custom*: [your own answer]

---

### Example Question (Implicit Story — Undiscovered Enabler)

---

**[Important] Section 4.2 — Foundation/Enabler Stories**

While analyzing the SRS use cases, the skill identified that multiple feature stories depend on user authentication and authorization, but no explicit requirement or story exists for the authentication foundation. Without an authentication enabler story, multiple feature stories would be blocked and undeliverable. Enabler stories are critical for Green Field projects — they establish the foundation that feature stories build upon.

Should foundation/enabler stories be included, and which ones are needed before feature stories can proceed?

Suggested answers:
- *Option A*: "Yes — include enabler stories as a dedicated epic 'EP-01: Foundation & Infrastructure' with stories for: user authentication, authorization/RBAC, error handling framework, logging/observability, and database schema setup. These are Must Have and must be delivered in Sprint 1–2 before feature stories can proceed. Each enabler story should trace to the NFRs in the SRS that require these foundations."
- *Option B*: "Yes — but minimize enabler stories to only what is strictly necessary: authentication and authorization. Other foundations (logging, error handling) should be incorporated as acceptance criteria within feature stories rather than separate stories. This keeps the backlog focused on user-visible value while still delivering the necessary infrastructure."
- *Option C*: "Authentication is handled by the corporate SSO — no enabler story needed. Authorization is covered by the SRS's FR-001 through FR-005. Include a single enabler story for 'SSO Integration' that covers the authentication/authorization foundation. Other infrastructure is handled by the DevOps team and is not in the product backlog."
- *Custom*: [your own answer]

---

### Example Question (Story Splitting — Compound Requirement)

---

**[Important] Section 10 — Story Splitting for Compound Requirement**

The SRS defines FR-015 "The system shall allow users to create, read, update, and delete project records." This is a compound requirement covering four distinct user actions (CRUD), each with different acceptance criteria, error cases, and permissions. A single story covering all four actions would likely be 13+ points and exceed the splitting threshold. The user stories document must split this into right-sized stories.

How should the CRUD requirement for project records be split into user stories?

Suggested answers:
- *Option A*: "Split by workflow step (Section 10.2): US-001 (Create project), US-002 (Read/view project), US-003 (Update project), US-004 (Delete project). Each story is independent and estimable (2–3 points each). Create is Must Have (without it, no projects exist); Read is Must Have (users cannot see projects); Update is Should Have; Delete is Could Have (soft-delete may suffice initially). US-001 and US-002 are on the critical path."
- *Option B*: "Split into two stories: US-001 (Create and Read project records — the minimum to have projects at all, 5 points, Must Have) and US-002 (Update and Delete project records — the management lifecycle, 5 points, Should Have). This is fewer stories but each is larger. If either exceeds 8 points during estimation, split further."
- *Option C*: "Split by persona: US-001 (Admin creates/manages project records — all CRUD operations for administrators, 5 points, Must Have) and US-002 (Team member views project records — read-only for end users, 2 points, Must Have). This aligns stories with distinct personas and their different permission levels."
- *Custom*: [your own answer]

---

### Example Question (Modernization — Feature Parity Story)

---

**[Critical] Section 11.1 — Feature Parity Stories**

The SRS specifies that the modernized system must maintain feature parity with the legacy reporting module, but the legacy system produces reports in RTF format while the new system is expected to produce PDF and XLSX. The parity story must specify whether RTF format is part of the parity target or whether the format change is an intentional behavioral difference. Without this, the parity acceptance criteria cannot be written.

For the reporting module parity story, what is the precise parity target?

Suggested answers:
- *Option A*: "Partial parity — the modernized system must produce the same report content and data, but output format is modernized: PDF and XLSX replace RTF. This is an intentional, approved behavioral difference. The parity story's acceptance criteria should specify: 'Given the same input parameters as the legacy system, When the report is generated, Then the report contains identical data content in PDF or XLSX format.' Parity is measured on content accuracy, not format replication."
- *Option B*: "Full parity during dual-running — both systems produce reports during the transition period, and the new system must also produce RTF for backward compatibility until all consumers have migrated to PDF/XLSX. After decommission, RTF is retired. The parity story includes a temporary RTF output requirement with a removal story in the decommission epic."
- *Option C*: "Capability parity, not format parity — the modernized system provides a self-service report builder that supersedes the legacy system's fixed-format reports. The parity story should specify: 'Given a user who previously used legacy Report X, When they use the report builder, Then they can access the same data and produce equivalent or superior reports.' This reframes parity as user capability rather than feature replication."
- *Custom*: [your own answer]

---

### Example Question (Brown Field — Existing Behavior Baseline)

---

**[Important] Section 4.2 — Existing Behavior for Modification Story**

The SRS specifies FR-032 "The system shall enhance the discount calculation to support tiered pricing," but no documentation describes the current discount calculation behavior. For a Brown Field project, the modifying story must reference the existing behavior using the "where currently [existing behavior]" clause. Without understanding the current behavior, the story cannot specify what changes and what stays, creating risk of breaking existing functionality.

What is the current discount calculation behavior that the story must reference and preserve?

Suggested answers:
- *Option A*: "The current system applies percentage-based discounts only, with a maximum discount cap of 30%. There are 5 discount types: loyalty, volume, seasonal, employee, and promotional. Stacking rule: only one discount type per order, the highest applicable discount wins. The story should use the format: 'As a pricing manager, I want to add tiered pricing discounts, so that volume buyers receive automatic price breaks, where currently the system applies only percentage-based discounts with a 30% cap and no stacking.' The existing behavior is preserved for simple discounts; tiered pricing is additive."
- *Option B*: "The discount calculation behavior is largely tribal knowledge — the code has complex conditional logic with no documentation. The skill should write the story with 'Questions / Unknowns: Existing discount behavior must be documented before this story can enter a sprint (DoR not met — spike needed).' A prerequisite spike story should be added: 'As a developer, I want to document the current discount calculation behavior, so that the enhancement story has a clear existing behavior baseline.'"
- *Option C*: "The current system has a simple discount model: percentage discounts with no stacking. The enhancement adds tiered discounts as net-new behavior — the existing calculation is preserved unchanged for simple discounts. The story format: 'As a pricing manager, I want tiered pricing discounts, so that volume buyers receive automatic price breaks, where currently the system supports only flat percentage discounts with no tiered logic.' Regression test stories should be added to verify the existing calculation is unchanged."
- *Custom*: [your own answer]

---

## Anti-Patterns to Avoid

- **Don't generate documents without asking questions** — the user stories' value is in the rigorous analysis and story decomposition, not in filling a template.
- **Don't ask questions that existing documentation already answers** — read carefully and use available information directly.
- **Don't ask too many questions at once** — batch by priority, lead with critical questions, offer to proceed with assumptions for lower-priority items.
- **Don't produce vague story statements** — "As a user, I want the system to work well" is not a story. "As a customer, I want to reset my password via email verification, so that I can regain access without contacting support" is.
- **Don't write stories without acceptance criteria** — every story must have at least one Given/When/Then criterion. A story without AC is not estimable or testable.
- **Don't create stories that span multiple personas** — if a story serves two different user roles with different needs, split by persona (Section 10.2).
- **Don't leave compound stories unsplit** — "The system shall support CRUD for project records" is 4 stories, not 1. Use the splitting patterns in Section 10.
- **Don't skip the traceability matrix** — it is the primary quality mechanism. Every story traces to a requirement; every Must Have requirement traces to a story.
- **Don't duplicate content from preceding documents** — the user stories document translates SRS requirements into delivery units; it does not restate the SRS. Reference the SRS.
- **Don't mark sections [NOT APPLICABLE] just because they're hard to populate** — only mark them if they genuinely don't apply to the project type.
- **Don't forget enabler/foundation stories** — Green Field projects need infrastructure stories before feature stories can proceed.
- **Don't forget regression stories** for 🟤🔵 — every modification to existing behavior needs verification that existing functionality still works.
- **Don't forget data migration stories** for 🔵 — data migration is a separate set of stories, not acceptance criteria on feature stories.
- **Don't conflate user stories with technical tasks** — "Set up the CI/CD pipeline" is a task, not a user story. "As a developer, I want automated build and deployment on every commit, so that I can deliver working software faster and with confidence" is a story.
- **Don't assign story points without understanding the scope** — if the story is too uncertain to estimate, flag it for a spike.
- **Don't skip the Definition of Ready** — no story enters a sprint until it meets the DoR criteria.
- **Don't skip the Definition of Done** — no story is considered complete until all DoD criteria pass.
- **Don't skip individual user story documents** — the central document is an overview; each story must have its own detailed document for sprint-level use.
- **Don't write the story map before defining all stories** — the story map is a synthesis of the story landscape, not a planning input. Define stories first, then organize them into the map.

## Document Hierarchy Context

The User Stories document is the **fifth** formal document in the project lifecycle (after viability study, business case, project scope, and SRS). It builds upon and elaborates:

| Document | Relationship | Precedes User Stories? |
|----------|-------------|------------------------|
| **Viability Study** | Determines whether the project is feasible — user stories translate viable features into delivery units | Yes — user stories should be consistent with the viability study's risk assessment and project type classification |
| **Business Case** | Defines the investment case and recommended option — user stories derive value propositions from the business case's benefit assumptions | Yes — story priorities should align with the business case's success criteria |
| **Project Scope** | Defines delivery boundaries — user stories elaborate each scope item into deliverable stories within those boundaries | Yes — stories must not exceed scope boundaries; out-of-scope items should not have stories |
| **SRS** | Defines what the system must do — user stories translate SRS requirements into delivery-sized units that the team can plan, estimate, and ship incrementally | Yes — every story must trace to at least one SRS requirement |

And it precedes:

| Document | Relationship | Follows User Stories? |
|----------|-------------|----------------------|
| **Software Architecture** | Implements user stories through architectural decisions | Yes — architecture enables the stories |
| **Sprint Backlogs** | Selects stories for sprint delivery based on capacity and priority | Yes — stories populate the backlog |
| **Test Plans** | Verifies acceptance criteria from user stories through test cases | Yes — every AC generates test cases |

When generating user stories, keep in mind that their primary output is a **complete, well-structured, estimable, and traceable set of user stories** organized by epics, mapped to releases, and supported by acceptance criteria that the team can plan, estimate, and deliver sprint by sprint. The central document provides the overview and governance; the individual story documents provide sprint-level detail.