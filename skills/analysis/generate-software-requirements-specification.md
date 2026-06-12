# Skill: Generate Software Requirements Specification

## Description

Generates a complete, rigorous Software Requirements Specification (SRS) based on the template `templates/analysis/software-requirements-specification.md`. The skill deeply analyzes all available project information — preceding analysis documents (viability study, business case, project scope), existing documentation, codebase, stakeholder inputs, and any informal requirements artifacts — to populate every applicable section with detailed, unambiguous, testable, and traceable requirements. When gaps, unclear statements, or contradictions are detected, the skill asks targeted open questions with suggested valid answers before proceeding. The SRS is the **authoritative source for what the system must do** — it specifies WHAT, not HOW.

## Activation

When the user requests to create, generate, or draft a Software Requirements Specification, SRS, requirements document, or requirements specification for a software project.

## Instructions

### Phase 1: Information Gathering & Deep Analysis

1. **Read the template** at `templates/analysis/software-requirements-specification.md` to understand the full structure, all 17 sections, their subsections, expected content, and project-type applicability (🟢 🟤 🔵 ⚪). Pay special attention to:
   - The requirement identification scheme (Section 2.6) — this defines how all requirements are numbered and traced.
   - The requirement quality criteria (Section 14.4) — every requirement must be necessary, unambiguous, testable, traceable, complete, consistent, feasible, and singular.
   - The usage guide at the end — requirements specify WHAT the system must do, not HOW.

2. **Discover and read all existing project information:**
   - Search the workspace for any viability study documents (check `documentation`, `docs`, project folders, or any `.md` files with "viability" in the name). If found, read it thoroughly — the SRS elaborates the viability study's recommendations into detailed requirements.
   - Search for any business case documents (check `documentation`, `docs`, project folders, or any `.md` files with "business-case" or "business_case" in the name). If found, read it — the SRS derives requirements from the approved investment option.
   - Search for any project scope documents (check `documentation`, `docs`, project folders, or any `.md` files with "project-scope" or "project_scope" in the name). If found, read it — the SRS elaborates each scope item into detailed, testable requirements. This is the most critical preceding document for the SRS.
   - Search for any existing requirements documents, user stories, backlog items, or feature lists.
   - Search for any architecture decision records (ADRs), README files, or technical documentation.
   - Search for any configuration files (`package.json`, `pom.xml`, `build.gradle`, `docker-compose.yml`, etc.) that reveal the technology stack, system boundaries, and integration points.
   - If a codebase exists, explore the directory structure to understand current modules, services, and integrations — this reveals existing behavior that must be specified or preserved.
   - Search for any stakeholder communication, meeting notes, user research, interview summaries, or survey data.
   - Search for any API specifications (OpenAPI, Swagger, GraphQL schemas, gRPC proto files).
   - Search for any database schemas, data dictionaries, or entity-relationship diagrams.
   - Search for any UI/UX artifacts — wireframes, prototypes, design system references.
   - Search for any compliance, security, or regulatory documentation (policies, audit reports, certifications, GDPR/HIPAA/PCI-DSS references).
   - Search for any existing test plans or test case documents — these reveal implicit requirements.
   - Search for any incident reports, support ticket data, or bug databases — these reveal undocumented requirements and pain points.
   - Search for any workflow diagrams, process models, or state machine definitions.

3. **Classify the project type** based on available evidence:
   - **Green Field (🟢)**: New product from scratch — SRS must define all user-system interactions, data models, and interfaces from zero. Full freedom in specifying behavior. All 🟢-marked sections are primary.
   - **Brown Field (🟤)**: Existing system enhancement — SRS must specify incremental changes against the existing baseline, preserve backward compatibility, and distinguish new behavior from existing. All 🟤-marked sections are primary.
   - **Software Modernization (🔵)**: Legacy system migration — SRS must specify feature parity requirements, migration-specific requirements, transition workflows, dual-running, and decommission. All 🔵-marked sections are primary.
   - If a preceding document (viability study, business case, or project scope) already classified the project type, adopt that classification unless new evidence contradicts it — note any contradiction as a question for Phase 2.
   - If classification is ambiguous, note this as a [Critical] question — the classification determines which sections apply and how requirements are framed.

4. **Map existing information to template sections.** For each of the 17 sections and their subsections, determine:
   - **Covered**: Sufficient information exists to populate the section with evidence-based, requirement-level content.
   - **Partially Covered**: Some information exists but is incomplete, too vague for requirement specification (e.g., "the system should be fast" instead of a measurable NFR), or lacks the detail needed for testable requirements.
   - **Gap**: No information exists for this section.
   - **Contradiction**: Information from different sources conflicts (e.g., scope document says "all users" but business case specifies "internal users only").

5. **Perform deep requirement-readiness analysis.** The SRS is a specification document — it must be precise, complete, and unambiguous. Go beyond surface-level mapping:

   **Preceding document alignment checks:**
   - Does the project scope's scope items map cleanly to functional requirement areas, or are there scope items too vague to derive requirements from?
   - Are the business case's success criteria measurable enough to derive acceptance criteria (Section 14.3) from?
   - If the viability study identified risks, are those risks reflected in constraints (Section 12) and the risk implications for requirements?
   - Are the project scope's out-of-scope items clear enough to prevent requirement creep? Are there borderline items that need clarification?
   - Do the MoSCoW priorities in the scope document translate consistently to requirement priorities in the SRS?

   **Requirement quality pre-checks:**
   - Is existing requirement information stated as WHAT the system must do, or does it leak into HOW (design decisions)? Design-level statements must be rephrased as requirements.
   - Are existing requirements singular (one capability per statement), or are they compound (multiple capabilities in one statement)? Compound requirements must be split.
   - Are existing requirements testable, or are they vague ("user-friendly", "fast", "secure")? Vague requirements must be clarified with measurable criteria.
   - Are there requirements implied by use cases or workflows that are not explicitly stated? Implicit requirements must be made explicit.
   - Are there requirements implied by data models or interfaces that are not captured? Data and interface constraints often carry implicit functional requirements.

   **Cross-domain consistency checks:**
   - Do the stated user personas (Section 3.1) cover all actors mentioned in use cases (Section 5) and interface requirements (Section 8)?
   - Do the functional requirements (Section 4) cover all business rules (Section 6), or are there rules without implementing requirements?
   - Do the data requirements (Section 7) cover all data entities referenced in functional requirements and use cases?
   - Do the interface requirements (Section 8) cover all external system interactions implied by the architecture or integration landscape?
   - Are the non-functional requirements (Section 9) consistent with the business case's performance and availability expectations?
   - Do the security requirements (Section 10) address all applicable regulations identified in the compliance matrix?
   - For 🟤🔵: Do the migration requirements (Section 11) align with the project scope's transition strategy?

   **Project-type-specific checks:**
   - 🟢 Green Field: Are all user-system interactions defined from scratch, or are there assumptions about "how things work" that aren't explicitly specified? Are there gaps in the data model that a Green Field project must fill completely?
   - 🟤 Brown Field: Is the existing system's behavior documented precisely enough to specify what changes and what stays? Are there undocumented behaviors (tribal knowledge) that need to be discovered? Are backward compatibility requirements explicit?
   - 🔵 Modernization: Is the feature parity target specified at the behavioral level (not just "same feature" but "same behavior under the same conditions")? Are there undocumented behaviors in the legacy system that parity verification would miss? Is the rollback strategy specified as a requirement?

6. **Build a requirement readiness map** — for each section, tag readiness:
   - 🟢 **Requirement-Ready**: Information is detailed, specific, and sufficient to write unambiguous, testable requirements.
   - 🟡 **Partially Ready**: Information exists but is too vague, incomplete, or needs decomposition into individual requirements.
   - 🔴 **Not Ready**: Missing, unquantified, or based on unsupported assertions — cannot derive testable requirements without clarification.

   Sections with 🔴 readiness are priority candidates for Phase 2 questions.

### Phase 2: Clarification Questions

Before generating the document, ask the user targeted questions for every **Partially Covered**, **Gap**, **Contradiction**, or **Not Ready** area identified in Phase 1.

#### Question Design Principles

- **Ask open questions** that invite thoughtful responses and deeper thinking — not yes/no questions.
- **Always suggest 2–3 possible valid answers** for each question to help the user think through the options and to demonstrate understanding of the domain.
- **Contextualize each question** — briefly explain why the information matters for the SRS and what happens if it remains unanswered (e.g., "Without this, the SRS cannot specify the data validation requirements, which means the system's data integrity behavior is undefined and untestable").
- **Group questions by template section** so the user can address them systematically.
- **Prioritize questions** — mark questions as:
  - **[Critical]**: Blocks requirement specification — the SRS cannot be generated for this section without this information. The requirement would be unverifiable or ambiguous.
  - **[Important]**: Affects the quality, completeness, or testability of requirements. Requirements can be drafted but will have gaps or weak acceptance criteria.
  - **[Optional]**: Refines the requirements but does not block specification. Can be documented as an assumption with a validation plan.
- **Reference the source** of the contradiction or gap (e.g., "The project scope defines 'user management' as a scope item, but no information was found about what user management capabilities are required").
- **Surface implicit requirements** — when a use case, workflow, or data model implies a requirement that isn't explicitly stated, propose the implied requirement and ask the user to confirm, challenge, or refine it.
- **Challenge vague requirements** — when existing information contains untestable statements (e.g., "the system shall be user-friendly", "the system shall perform well"), flag them explicitly and ask for measurable criteria.
- **Challenge design-as-requirement** — when existing information specifies HOW instead of WHAT (e.g., "use React for the frontend", "store data in PostgreSQL"), ask whether this is a genuine constraint (Section 12) or a design decision that should not be in the SRS.
- **Do not ask questions that can be answered by reading existing documentation** — if the answer exists in a file the skill has already read, use that information directly.
- **Distinguish between information that must be resolved now vs. information that can be documented as assumptions with validation plans** — for [Optional] questions, offer to proceed with a stated assumption.

#### Question Template

For each question, use this format:

---

**[Priority] Section X.Y — [Topic]**

[Context: Why this matters for the SRS and what happens if unanswered]

[The open question]

Suggested answers:
- *Option A*: [description and implications for requirements]
- *Option B*: [description and implications for requirements]
- *Option C*: [description and implications for requirements]
- *Custom*: [your own answer]

---

#### Minimum Required Questions by Project Type

**All project types** must resolve these before the SRS can be generated:

- What is the core purpose of the system — what problem does it solve for whom?
- Who are the primary user personas and what are their key goals with the system?
- What are the top-level feature areas the system must support?
- What are the MoSCoW priorities for the main feature areas?
- What are the most critical non-functional requirements (performance, availability, security)?
- What external systems does the system need to integrate with?
- What are the applicable regulatory or compliance requirements?
- What are the key constraints (technical, business, timeline)?

**Green Field (🟢) additional questions:**
- What are all the user-system interactions the system must support — every way a user initiates contact with the system?
- What is the complete data model — what entities does the system manage, what are their attributes, and how do they relate?
- What are the system boundaries — where does the system end and the external world begin?
- What is the complete set of business rules the system must enforce?
- What are the complete set of states and workflows the system must manage?

**Brown Field (🟤) additional questions:**
- What is the precise existing system behavior that must be preserved (baseline)?
- What specific behavior changes are required — what does the system do now that must change, and what must it do instead?
- What backward compatibility constraints apply — which existing APIs, data formats, integrations, and user workflows must remain unchanged?
- What undocumented behaviors exist in the current system (tribal knowledge, workarounds, implicit rules) that the enhancement must account for?
- What is the impact of the enhancement on existing users who are not the target of the new features?

**Software Modernization (🔵) additional questions:**
- What is the feature parity target at migration cutover — 100% behavioral parity, or is partial parity acceptable for specific features?
- For each feature being migrated, what is the expected behavioral difference (if any) between the legacy and target system?
- What is the data migration scope — which entities, which date ranges, what transformations?
- What is the rollback strategy if the migration fails — how does the system revert to the legacy system and what is the maximum rollback window?
- What undocumented behaviors exist in the legacy system that parity verification would miss?
- What is the dual-running period (if applicable) and what data consistency requirements exist between the two systems during transition?

### Phase 3: Document Generation

Once all critical and important questions are resolved, generate the Software Requirements Specification document.

#### Generation Rules

1. **Use the template structure exactly** — follow `templates/analysis/software-requirements-specification.md` section by section, including all subsections.
2. **Replace all `<!-- -->` placeholders** with project-specific content derived from the analysis and user answers.
3. **Mark sections as [APPLICABLE] or [NOT APPLICABLE]** based on the project type classification. For [NOT APPLICABLE] sections, include a one-line rationale (e.g., "[NOT APPLICABLE] — Green Field project with no existing system to migrate").
4. **For 🟤🔵 sections**, populate them if the project type matches; otherwise mark [NOT APPLICABLE].
5. **Fill every table** with concrete, specific content — no placeholder values remaining in the final document.
6. **Write the Executive Summary (Section 1) last** — after all other sections are complete, synthesize the requirement counts, priorities, high-risk areas, and key constraints.
7. **Every functional requirement must follow the format**: "The system shall [verb] [object] [condition/constraint]." — this makes each requirement a testable statement.
8. **Every requirement must be singular** — one capability per requirement statement. If a statement contains "and" joining two distinct capabilities, split it into two requirements.
9. **Every requirement must be unambiguous and testable** — avoid vague language. Write "The system shall validate email format using RFC 5322" not "The system shall validate email." Write "The system shall respond to search queries within 200ms at p99 under 100 concurrent users" not "The system shall be fast."
10. **Every requirement must be traceable** — each requirement must trace to a source (scope item, business objective, regulation) and forward to a verification method. Populate the traceability matrices (Section 13).
11. **Every requirement must be prioritized** using MoSCoW (Must Have / Should Have / Could Have / Won't Have This Time).
12. **Distinguish WHAT from HOW** — the SRS specifies what the system must do, not how it is implemented. If a requirement specifies a technology, framework, or architecture, flag it and determine whether it is a genuine constraint (belongs in Section 12) or a design decision (does not belong in the SRS).
13. **For 🟤🔵 requirements that modify existing behavior**, always reference the existing behavior and specify only the delta. Use the format:
    - **Existing Behavior**: What the current system does.
    - **Required Change**: What changes and what stays the same.
    - **Backward Compatibility**: Whether existing behavior must be preserved for any users or integrations.
14. **Cross-reference between sections** — when content in one section depends on another, reference it (e.g., "As specified in BR-003 (Section 6.1), the system must enforce the 30-day return window; FR-047 implements this rule").
15. **Populate the requirement identification scheme (Section 2.6)** before writing requirements — this ensures consistent numbering throughout.
16. **Ensure business rules (Section 6) are implemented by functional requirements (Section 4)** — every business rule must trace to at least one FR. Every decision table must reference the business rules it implements.
17. **Ensure data requirements (Section 7) cover all entities referenced in functional requirements and use cases** — if an FR references an entity, that entity must be specified in Section 7.
18. **Ensure interface requirements (Section 8) cover all external system interactions** — if a use case or FR involves an external system, an interface requirement must exist.
19. **Ensure the verification & validation section (Section 14) specifies how each requirement category is verified** — every requirement must have a verification method.
20. **Ensure the change control process (Section 15) is realistic and actionable** — it must define who approves what at which impact level.
21. **Save the generated document** to an appropriate location, suggested: `documentation/software-requirements-specification.md` or `docs/srs.md`.

#### Requirement Writing Guidelines

- Use "The system shall..." for functional requirements — this makes each requirement a testable statement.
- Use precise, measurable language: "within 200ms (p99)" not "fast"; "99.9% availability" not "highly available."
- One requirement per statement: "The system shall validate the email format" and "The system shall send a confirmation email" are two requirements, not one.
- Avoid design in requirements: "The system shall store passwords using bcrypt with 12 rounds" is a design decision, not a requirement. "The system shall securely store authentication credentials in accordance with NIST SP 800-63B" is a requirement.
- Distinguish mandatory from optional: use MoSCoW consistently.
- For 🟤🔵: when modifying existing behavior, always reference the existing behavior and specify only the delta to avoid ambiguity.
- Every non-functional requirement must have a target value and a measurement method — "The system shall be available" is not a requirement. "The system shall maintain 99.9% uptime measured over rolling 30-day periods, excluding scheduled maintenance windows" is.

#### Quality Checks Before Delivery

After generating the document, perform these self-checks:

- [ ] Every section is either populated with project-specific content or marked [NOT APPLICABLE] with rationale.
- [ ] No `<!-- -->` placeholders remain (except the document status, date, and sign-off fields that require human input).
- [ ] The Executive Summary (Section 1) accurately reflects the full document — total requirement counts, priority distribution, high-risk areas, and key constraints are correct.
- [ ] The project type classification in Section 2.2 is consistent with how 🟢🟤🔵 sections are handled throughout the document.
- [ ] Every functional requirement follows the "The system shall..." format.
- [ ] Every requirement is singular — no compound requirements containing "and" for distinct capabilities.
- [ ] Every requirement is testable — each has a verification method defined (demo / test / inspection / analysis).
- [ ] Every requirement is prioritized with MoSCoW.
- [ ] Every requirement is traceable — forward to design/test (Section 13.1) and backward to source/scope item (Section 13.2).
- [ ] No orphan requirements exist — every requirement traces to a source.
- [ ] No uncovered scope items exist — every scope item has implementing requirements.
- [ ] Business rules (Section 6) are implemented by functional requirements — every BR traces to at least one FR.
- [ ] Data requirements (Section 7) cover all entities referenced in functional requirements and use cases.
- [ ] Interface requirements (Section 8) cover all external system interactions implied by use cases, FRs, or architecture.
- [ ] Non-functional requirements (Section 9) have measurable targets and measurement methods.
- [ ] Security requirements (Section 10) address all applicable regulations in the compliance matrix.
- [ ] Migration requirements (Section 11) are populated for 🔵🟤 projects with feature parity specifications and rollback strategies.
- [ ] Constraints (Section 12) are marked as fixed / limited / negotiable.
- [ ] Assumptions (Section 12.3) have impact statements if proven wrong.
- [ ] The traceability coverage report (Section 13.3) shows 100% coverage targets and flags any gaps.
- [ ] The verification approach (Section 14.1) covers every requirement category.
- [ ] The requirement quality criteria (Section 14.4) are applied — no requirement violates any criterion.
- [ ] The change control process (Section 15) defines approval authority at each impact level.
- [ ] No contradictions exist between sections (if they do, flag them explicitly in the document).
- [ ] For 🟤🔵: existing behavior and required change are explicitly distinguished — no ambiguity about what changes and what stays.

### Phase 4: Post-Generation Review

After the document is generated:

1. **Present the document** to the user.
2. **Highlight key judgments made** during generation — where the skill made interpretive calls (e.g., decomposing a vague scope item into specific requirements, inferring an implicit requirement from a use case, choosing MoSCoW priorities where they were unspecified), point them out so the user can verify.
3. **Present the requirement summary** clearly — total functional requirements, total non-functional requirements, MoSCoW distribution, high-risk requirement areas, and key constraints.
4. **Flag remaining uncertainties** — any areas where information was insufficient and assumptions were made. Indicate the risk each assumption poses to the requirement specification and suggest validation activities.
5. **Present the traceability coverage** — show the coverage report from Section 13.3, highlighting any gaps that remain.
6. **Flag implicit requirements discovered** — any requirements that were not explicitly stated in preceding documents but were inferred from use cases, data models, business rules, or workflows. These are the most likely to be contested and should be reviewed carefully.
7. **Offer to refine** any section the user wants to adjust.
8. **Suggest next steps** — e.g., stakeholder review, architecture design (using `templates/design/software-architecture.md`), test plan creation, backlog creation from requirements, requirement prioritization workshop.

## Examples

### Example Question (Gap — No Functional Requirements for Scope Item)

---

**[Critical] Section 4.2 — Functional Requirements for [Feature Area]**

The project scope defines "User Management" as a Must Have scope item, but no detailed requirements were found for what user management capabilities the system must provide. The SRS cannot specify requirements for a scope item without understanding the expected behavior — what can users do, what can administrators do, what are the rules?

What specific user management capabilities must the system support?

Suggested answers:
- *Option A*: "Full CRUD user lifecycle: administrators shall create, read, update, and deactivate user accounts. Users shall self-register with email verification, update their profile, reset their password, and view their login history. Role-based access control with 3 predefined roles (Admin, Editor, Viewer). Account deactivation (not deletion) with audit trail."
- *Option B*: "Minimal user management: system administrator provisions users manually (no self-registration). Users can update their profile and reset their password. Single role (User vs. Admin). No self-registration, no login history, no account deactivation — these are deferred to a later release."
- *Option C*: "Federated identity: the system does not manage user accounts internally. It integrates with the corporate SSO (SAML 2.0) for authentication and receives user attributes (name, email, role) from the identity provider. User management is out of scope — the system consumes identity from the IdP. Functional requirements should specify the SSO integration and attribute mapping."
- *Custom*: [your own answer]

---

### Example Question (Vague Requirement — Non-Testable NFR)

---

**[Important] Section 9.2 — Performance Requirements for Search**

The project scope states the system "should have fast search," which is not a testable requirement. The SRS must specify measurable performance targets with load profiles and measurement methods. Without this, there is no way to verify whether the performance requirement is met, and no way to design the system to meet it.

What are the specific performance requirements for search functionality?

Suggested answers:
- *Option A*: "Search API p99 latency < 200ms under 100 concurrent users with a dataset of up to 500K records. Search page load time p95 < 1 second. Indexed fields: name, description, tags, date range. Faceted search response time p99 < 500ms. These are Must Have targets based on user experience research showing 200ms as the threshold for perceived instantaneous response."
- *Option B*: "Search performance should meet the current system's baseline (p99 ~1.5s) as a minimum, with a target of p99 < 500ms. The current system's search is the top user complaint — the target should represent a meaningful improvement. Load profile: 50 concurrent users, 100K records. This is a Should Have — if the target cannot be met within the timeline, the baseline improvement is acceptable."
- *Option C*: "We don't have specific performance targets yet. The SRS should specify placeholder targets (p99 < 1s for search, 50 concurrent users) as Should Have, flag them as assumptions, and note that a performance testing sprint should calibrate realistic targets before architecture design is finalized."
- *Custom*: [your own answer]

---

### Example Question (Contradiction — Scope Boundary Conflict)

---

**[Critical] Section 8.2 — API Requirements: CRM Integration**

The business case includes "CRM integration" as a benefit driver, and the project scope lists "CRM data sync" as a scope item, but the scope document's exclusions section states "CRM-side modifications are out of scope." This creates a contradiction: if the CRM system cannot be modified to receive data, how does the "sync" work? The SRS must resolve whether the integration is unidirectional (push to CRM), bidirectional (requiring CRM changes), or deferred.

What is the CRM integration requirement — what data flows in which direction, and who is responsible for each side?

Suggested answers:
- *Option A*: "Unidirectional: the system pushes customer and order data to the CRM via its existing REST API. The CRM already has an inbound API that accepts this data — no CRM-side modifications are needed. The integration is fully within scope. FR: The system shall push customer profile updates and order status changes to the CRM within 5 minutes of the change occurring."
- *Option B*: "Bidirectional: the system pushes data to the CRM AND reads account details from the CRM to enrich user profiles. The CRM has existing APIs for both directions — no CRM-side modifications needed. FR: The system shall retrieve account details from the CRM API within 2 seconds of user login, and shall push order events to the CRM within 5 minutes."
- *Option C*: "Deferred: CRM integration is out of scope for the initial release. The system shall expose outbound webhooks for customer and order events, but no active push to CRM. CRM consumption of these webhooks is a separate project. A manual data export (CSV) bridges the gap in the interim."
- *Custom*: [your own answer]

---

### Example Question (Implicit Requirement — Undiscovered Business Rule)

---

**[Important] Section 6.1 — Business Rules for Order Processing**

While analyzing the order workflow, the skill identified an implicit business rule that is not documented anywhere: when an order contains items from multiple warehouses, the system must either split the shipment or route it through a single warehouse. This decision affects inventory management, shipping cost calculation, and customer notification logic. No preceding document specifies which behavior is required.

When an order contains items from multiple warehouses, what should the system do?

Suggested answers:
- *Option A*: "Split the order into separate shipments per warehouse — each shipment has its own tracking, delivery estimate, and fulfillment workflow. The customer receives one order confirmation but multiple shipping notifications. Business rule: when items are in different warehouses, the system shall create one fulfillment order per warehouse, each with independent shipping calculations and tracking."
- *Option B*: "Route the entire order through the warehouse with the most items (or nearest to the customer) — items are transferred between warehouses internally before shipment. The customer receives one shipment. Business rule: the system shall assign the order to the optimal warehouse based on item availability and shipping distance, with internal transfers handled by the warehouse management system."
- *Option C*: "Present the choice to the customer at checkout — show delivery estimates and costs for split vs. single shipment, and let the customer decide. Business rule: when items span multiple warehouses, the system shall present shipment options (split or consolidated) with estimated delivery dates and costs, and fulfill according to the customer's selection."
- *Custom*: [your own answer]

---

### Example Question (Brown Field — Undocumented Existing Behavior)

---

**[Important] Section 4.2 — [Feature Area]: Existing Behavior Baseline**

For a Brown Field enhancement to the discount system, no documentation was found about the current discount calculation behavior. The business case references "discount rules" and the scope item says "enhance discount engine," but without understanding the current behavior, the SRS cannot specify what changes and what stays. Undocumented existing behavior is a major risk for Brown Field projects — the enhancement may break implicit rules that users depend on.

What is the current discount system behavior, and what are the known undocumented rules (tribal knowledge)?

Suggested answers:
- *Option A*: "The current system applies percentage-based discounts only, with a maximum discount cap of 30%. There are 5 discount types: loyalty, volume, seasonal, employee, and promotional. The discount stacking rule is: only one discount type per order, the highest applicable discount wins. There is an undocumented workaround where customer service can apply a manual discount override of up to 50% with manager approval — this must be preserved. I can provide the current discount rule documentation and the manual override process."
- *Option B*: "The discount system is largely tribal knowledge — the code has complex conditional logic with no documentation. The enhancement should include a reverse-engineering phase where the current discount behavior is captured as business rules (Section 6.1) with the Change Type 'preserved.' The SRS should specify that the existing discount behavior must be documented and verified as a prerequisite for the enhancement requirements. Any behavioral differences discovered during reverse-engineering must be flagged as potential breaking changes."
- *Option C*: "The current system has a simple discount model: percentage discounts with no stacking. The enhancement adds conditional discounts (buy X get Y, tiered discounts, bundle discounts) which are net-new. The existing behavior is preserved for simple discounts; the new discount types are additive. No undocumented behaviors are known, but the SRS should specify regression tests for the existing discount calculation to detect any accidental behavior changes."
- *Custom*: [your own answer]

---

### Example Question (Modernization — Feature Parity Ambiguity)

---

**[Critical] Section 11.1 — Feature Parity for [Feature]**

The project scope states "100% feature parity at cutover" for the reporting module, but the legacy system produces reports in a legacy format (RTF) that the modernized system is not expected to support. The modernized system will produce PDF and XLSX instead. This is a behavioral difference from the legacy system — is this acceptable, or must RTF output be preserved for parity? The SRS must specify parity at the behavioral level, not just at the feature level.

For the reporting module, what is the precise parity target — must the modernized system replicate the legacy behavior exactly, or are specific behavioral differences acceptable?

Suggested answers:
- *Option A*: "Partial parity for report formats — the modernized system must produce the same report content and data, but output format is modernized: PDF and XLSX replace RTF. This is an intentional, approved behavioral difference. Users are notified and trained on the new formats. Parity is measured on content accuracy, not format replication. MR requirement: The system shall produce all reports currently available in the legacy system with identical data content, delivered in PDF and XLSX format instead of RTF."
- *Option B*: "Full parity including RTF format during the dual-running period — both systems produce reports, and the legacy system's RTF output must be available until all consumers migrate to PDF/XLSX. After the dual-running period, RTF is retired. This adds a format requirement during transition that is removed after decommission. MR requirement: During the transition period, the system shall produce reports in RTF format for backward compatibility; after decommission, RTF support is retired."
- *Option C*: "Format parity is not the right measure — the reporting module is being redesigned with a self-service report builder that supersedes the legacy system's fixed-format reports. Parity is measured by user capability: can users get the same information? Yes, through more flexible means. The SRS should specify capability parity (the same data is accessible in reports) rather than format parity (the same file format is produced)."
- *Custom*: [your own answer]

---

### Example Question (Design-as-Requirement — Technology Specification)

---

**[Important] Section 12.1 — Technical Constraint vs. Design Decision**

Several existing documents state "the system shall use React for the frontend" and "the system shall use PostgreSQL for the database." These are design decisions, not requirements — the SRS specifies WHAT the system must do, not HOW. However, if these are genuine organizational constraints (approved technology standards, corporate mandates), they belong in Section 12.1 as constraints rather than as functional requirements.

Are the technology specifications (React, PostgreSQL) genuine constraints, or are they design decisions that should not be in the SRS?

Suggested answers:
- *Option A*: "These are genuine organizational constraints — the corporate technology standard mandates React for all new frontends and PostgreSQL for all relational data stores. They are non-negotiable. Add them to Section 12.1 as fixed constraints: 'Frontend must be implemented using React (corporate UI standard v3.2)' and 'Relational data must be stored in PostgreSQL (corporate database standard v2.1)'. They do NOT become functional requirements — the system does not 'shall use React'; rather, the implementation must conform to the stated constraint."
- *Option B*: "These are design decisions informed by the architecture, not constraints. React is the preferred frontend framework based on team skills, but it could be substituted if a better option emerges. PostgreSQL is the default database choice but not mandated. Do NOT include them in the SRS as requirements or constraints — they belong in the architecture design document. If the user wants to constrain the technology, they should be added to Section 12.1 as limited-flexibility constraints."
- *Option C*: "React is a fixed constraint (corporate standard) but PostgreSQL is a design decision (team preference, not mandated). Add React to Section 12.1 as a fixed constraint; leave PostgreSQL out of the SRS — it's a design decision. The SRS specifies data requirements (Section 7) and non-functional requirements (Section 9) that the database must meet, but does not prescribe which database product."
- *Custom*: [your own answer]

---

## Anti-Patterns to Avoid

- **Don't generate the document without asking questions** — the SRS's value is in the rigorous analysis and precise specification, not in filling a template.
- **Don't ask questions that existing documentation already answers** — read carefully and use available information directly.
- **Don't ask too many questions at once** — batch by priority, lead with critical questions, offer to proceed with assumptions for lower-priority items.
- **Don't produce vague requirements** — "The system shall be user-friendly" is not a requirement. "The system shall complete the checkout process in 3 steps or fewer with no more than 2 clicks per step" is.
- **Don't write design as requirements** — "The system shall use microservices" is architecture, not a requirement. "The system shall support independent deployment and scaling of the order processing capability" is a requirement (the "shall" describes a capability, not an implementation).
- **Don't create compound requirements** — "The system shall validate the email and send a confirmation" is two requirements. Split them.
- **Don't skip the traceability matrix** — it is the primary quality mechanism for the SRS. Every requirement must trace to a source and forward to a verification method.
- **Don't duplicate content from preceding documents** — the SRS elaborates scope items into detailed requirements; it does not restate the business case or viability study. Reference them.
- **Don't mark sections [NOT APPLICABLE] just because they're hard to populate** — only mark them if they genuinely don't apply to the project type.
- **Don't skip the requirement quality criteria check** — every requirement must be necessary, unambiguous, testable, traceable, complete, consistent, feasible, and singular (Section 14.4).
- **Don't write the Executive Summary first** — write it last, after all requirements are defined and counts are known.
- **Don't forget to populate the requirement identification scheme (Section 2.6)** — this defines the numbering system used throughout the document and must be established before writing requirements.
- **Don't conflate the SRS with the project scope** — the project scope defines boundaries; the SRS defines detailed behavior within those boundaries. The SRS elaborates scope items into testable requirements; it does not redefine scope.
- **Don't produce unmeasurable non-functional requirements** — "high availability", "good performance", "strong security" are meaningless in an SRS. Every NFR must have a target value, measurement method, and (for 🟤🔵) a baseline.
- **Don't skip the change control process (Section 15)** — once baselined, the SRS is the authoritative source. Changes must go through a defined process.
- **Don't ignore implicit requirements** — use cases, workflows, and data models often imply requirements that are not explicitly stated. Make them explicit in the SRS.

## Document Hierarchy Context

The Software Requirements Specification is the **third or fourth** formal document in the project lifecycle, depending on which preceding documents were produced. It builds upon and elaborates:

| Document | Relationship | Precedes SRS? |
|----------|-------------|---------------|
| **Viability Study** | Determines whether the project is feasible — the SRS defines the detailed requirements for the viable system | Yes — the SRS should be consistent with the viability study's technical feasibility assessment and project type classification |
| **Business Case** | Defines the investment case and recommended option — the SRS derives requirements from the approved option | Yes — the SRS should be consistent with the business case's success criteria and benefit assumptions |
| **Project Scope** | Defines delivery boundaries — the SRS elaborates each scope item into detailed, testable requirements | Yes — the SRS elaborates within the scope boundaries; it does not redefine them |

And it precedes:

| Document | Relationship | Follows SRS? |
|----------|-------------|---------------|
| **Software Architecture** | Implements the SRS's requirements through architectural decisions | Yes — architecture derives from requirements |
| **Test Plans** | Verifies the SRS's requirements through test cases | Yes — every requirement must be testable |
| **Sprint Backlogs** | Decomposes SRS requirements into implementable work items | Yes — requirements feed into development |

When generating the SRS, keep in mind that its primary output is a **complete, unambiguous, testable, and traceable set of requirements** that the system must satisfy. The SRS is the authoritative source for system behavior — design and implementation decisions are derived from this document. If a project scope exists, the SRS should elaborate each scope item into detailed, testable requirements rather than repeating scope-level descriptions.