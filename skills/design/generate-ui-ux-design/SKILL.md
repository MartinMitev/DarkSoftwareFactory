---
name: generate-ui-ux-design
description: Generates a UI/UX Design document. The skill deeply analyzes all available project information — the SRS's UI requirements, personas, non-functional requirements, the software architecture, brand guidelines, user research, existing design artifacts, and any informal UX inputs — to generate a UI/UX design document based on the template templates/design/ui-ux-design.md. The skill **proposes the design foundation** (design system, component library, accessibility target, visual direction) and aligns it with the user before finalizing. When gaps, unclear statements, or contradictions are detected in the source material, the skill asks targeted open questions with suggested valid answers before proceeding. The UI/UX design document specifies HOW users will experience the system — it translates the SRS's "what the system must do" into concrete screens, flows, interaction patterns, visual language, and measurable UX acceptance criteria.
---

# Skill: Generate UI/UX Design

## Description

Generates a complete, rigorous UI/UX Design document based on the template `templates/design/ui-ux-design.md`. The skill deeply analyzes all available project information — preceding analysis documents (viability study, business case, project scope, SRS with its user interface requirements, personas, and non-functional requirements), the Software Architecture document with its technology decisions, user stories, brand guidelines, existing design systems, user research, analytics, legacy UI references, stakeholder inputs, and any informal UX artifacts — to populate every applicable section with detailed, justified, traceable design decisions. The skill **proposes the design foundation** — design system approach, component library, accessibility target, visual direction, and navigation paradigm — and aligns it with the user before finalizing. When gaps, ambiguities, or contradictions are detected in the source material, the skill asks targeted open questions with suggested valid answers before proceeding. The UI/UX design document specifies HOW users will experience the system — it translates the SRS's "what the system must do" into concrete screens, user flows, interaction patterns, UI states, visual language, accessibility practices, and measurable UX acceptance criteria.

## Activation

When the user requests to create, generate, or draft a UI/UX design document, UX design specification, UI design document, user experience design, screen and flow specification, or design concept for a software project.

## Instructions

### Phase 1: Information Gathering & Deep Analysis

1. **Read the template** at `templates/design/ui-ux-design.md` to understand the full structure, all 16 sections, their subsections, expected content, and project-type applicability (🟢 🟤 🔵 ⚪). Pay special attention to:
   - The Metadata table — project name, type classification, UX/UI lead and designers.
   - The Executive Summary (Section 1) — must be written last, after all design decisions are made.
   - The project type classification (Section 2.2) — 🟢 Green Field, 🟤 Brown Field, 🔵 Software Modernization — and how it determines which sections are applicable.
   - The requirements overview (Section 2.4) — every design element must trace to at least one SRS requirement (FR, UC, NFR, or IR ID).
   - The UX quality goals (Section 2.5) — these drive design decisions and must be specific and measurable (task success rate, time-on-task, SUS score).
   - The design constraints (Section 3) — brand, technical/platform, compliance, and 🟤🔵 legacy UI constraints.
   - The screen inventory (Section 5.1) — the screen ID scheme (e.g., SCR-001) used throughout the document.
   - The user flows (Section 6.1) — success, alternative, and exception paths with screen references.
   - The state design (Section 6.3) — every screen must specify empty, loading, error, success, offline, and permission-denied states.
   - The design tokens (Section 8.1) — color contrast ratios must satisfy the accessibility targets (Section 9).
   - The UX metrics (Section 12) — measurable acceptance criteria tracing to flows, screens, and requirements.
   - The 🟤🔵-marked sections — legacy UI constraints, parity, transition UX, user retraining.

2. **Discover and read all existing project information:**
   - Search the workspace for any SRS documents (check `documentation`, `docs`, project folders, or any `.md` files with "requirements" or "srs" in the name). If found, read it thoroughly — this is the **most critical** preceding document for UI/UX design. Focus especially on:
     - Section 8.5 (User Interface Requirements) — the primary input: screens, platforms, interactions, navigation, error display, responsive and accessibility requirements.
     - Section 3.1/3.2 (User Personas, Actor Definitions) — who the design must serve.
     - Section 9 (Non-Functional Requirements) — usability, accessibility, compatibility, and localization NFRs with their measurable targets.
     - Section 5 (Use Cases) — the interactions that become user flows and screens.
     - Section 7 (Data Requirements) — the data displayed, created, and edited in the UI.
     - Section 11 (Migration & Transition Requirements) 🟤🔵 — feature parity, transition workflows, and user migration requirements that drive transition UX.
   - Search for the Software Architecture document (`software-architecture`, `architecture`). If found, read the sections that constrain UI/UX design: technology decisions (frontend framework, component library), building block view (frontend structure), cross-cutting concepts (security, error handling, observability affecting UI behavior), and deployment view (platforms). The UI/UX design must be **buildable within the architecture's technology decisions** — a design requiring native mobile features contradicts a web-only architecture.
   - Search for user story documents — stories reveal task flows, priorities, and delivery sequence that shape flow priority and screen phasing.
   - Search for any project scope documents — scope boundaries and MoSCoW priorities constrain what screens and flows are in the design.
   - Search for any business case documents — success criteria and benefit assumptions inform UX quality goals.
   - Search for brand guidelines, corporate design manuals, or existing design system documentation (tokens, component libraries, storybooks, pattern libraries).
   - Search for user research material: interview notes, survey results, analytics reports, support ticket summaries, prior usability test reports, competitive analyses.
   - Search for existing design artifacts: wireframes, mockups, prototypes, Figma/Sketch/Adobe XD files, design tokens files, icon sets.
   - Search for 🟤🔵 legacy UI references: screenshots, existing screen documentation, known usability complaints, user training materials — these establish the UX baseline that parity and improvement are measured against.
   - Search for accessibility and compliance documentation: WCAG conformance requirements, accessibility audits, regulations (European Accessibility Act, Section 508, BITV), and legal display requirements.
   - Search for localization requirements: supported languages, locales, RTL needs, translation workflows.
   - Search for any platform guidelines in use (Apple HIG, Material Design) and performance budgets (LCP targets, animation budgets) from the architecture.
   - Search for any stakeholder communication, meeting notes, or decision logs — these may reveal design constraints or preferences not captured in formal documents.

3. **Classify the project type** based on available evidence:
   - **Green Field (🟢)**: New product from scratch — full freedom in visual language, interaction patterns, and design system creation. All 🟢-marked sections are primary. The design establishes the foundational UX patterns, design tokens, and component library.
   - **Brown Field (🟤)**: Existing system enhancement — the design must fit new screens and flows into the existing experience, preserve user-familiar patterns, and ensure new and existing screens feel coherent. All 🟤-marked sections are primary.
   - **Software Modernization (🔵)**: Legacy system migration — the design must preserve feature parity at the UI level, plan user transition and retraining, design transition states (dual-running UIs, feature-flagged rollouts), and specify which legacy screens are retired. All 🔵-marked sections are primary.
   - If a preceding document already classified the project type, adopt that classification unless new evidence contradicts it — note any contradiction as a question for Phase 2.
   - If classification is ambiguous, note this as a [Critical] question — the classification determines which sections apply and how the design is framed.

4. **Map existing information to template sections.** For each of the 16 sections and their subsections, determine:
   - **Covered**: Sufficient information exists to populate the section with evidence-based, design-level content.
   - **Partially Covered**: Some information exists but is incomplete, too vague for design specification (e.g., "the UI should be user-friendly" instead of concrete interactions and states), or lacks the detail needed for design decisions.
   - **Gap**: No information exists for this section.
   - **Contradiction**: Information from different sources conflicts (e.g., the SRS requires a mobile app experience but the architecture and constraints define a responsive web application only).

5. **Perform deep design-readiness analysis.** The UI/UX design document is a specification — it must be precise, justified, buildable, and internally consistent. Go beyond surface-level mapping:

   **Preceding document alignment checks:**
   - Do the SRS's UI requirements (Section 8.5) define the screens, platforms, and interactions precisely enough to design from, or are they too vague ("the system shall have a dashboard") to derive concrete screen designs?
   - Are the SRS's personas and actors complete enough to derive user flows, or are there use cases with actors that have no persona?
   - Do the SRS's usability and accessibility NFRs provide specific, measurable targets the design can be built and tested against, or are they vague ("user-friendly", "accessible")?
   - Does the architecture document constrain the UI coherently — frontend framework, component library, performance budgets, API contracts — or are there gaps between what the design needs and what the architecture provides?
   - Are the use cases' main, alternative, and exception flows complete enough to derive user flows with all branches, or do exception behaviors need clarification?
   - Are the user stories' priorities and delivery sequence consistent with a sensible screen and flow prioritization?
   - 🟤🔵: Is the legacy UI's behavior documented precisely enough to specify parity, or is there undocumented tribal knowledge about how users actually work with the current system?

   **Design decision readiness checks:**
   - Can the design vision and principles be derived from the business case, brand guidelines, and research, or are there too many degrees of freedom?
   - Can the information architecture (screen inventory, navigation model) be derived from the SRS feature areas and use cases, or are there ambiguities in how the product should be structured?
   - Can UX quality targets be set from NFRs and research baselines, or do they need calibration?
   - Can the visual direction be determined from brand guidelines and the existing design system, or is the visual language undefined?
   - Are there conflicting UX goals that require trade-off decisions (e.g., power-user efficiency vs. novice learnability, information density vs. clarity)?

   **Cross-view consistency pre-checks:**
   - Does every use case in the SRS have a screen and a flow in the design? Are there screens with no supporting requirement (design creep) or requirements with no screen (coverage gap)?
   - Do the personas cover all actors mentioned in use cases?
   - Does every screen in the inventory have all UI states specified (Section 6.3), and does every flow reference valid screen IDs?
   - Do the accessibility NFRs match the compliance constraints (Section 3.3) and the color contrast requirements of the design tokens (Section 8.1)?
   - Does the responsive design (Section 7.3) cover the platforms and devices stated in the SRS and architecture?
   - 🟤🔵: Do the migration UX requirements (dual-running, onboarding, retraining) have design counterparts in the transition sections?

   **Project-type-specific checks:**
   - 🟢 Green Field: Is there a brand guideline or design system to start from, or is the visual language fully open? What is the complete platform/device matrix? Who owns UI copy and empty-state content?
   - 🟤 Brown Field: Which existing screens, patterns, and components must be preserved for user familiarity? How will new screens stay coherent with the existing ones? What are the known usability complaints the redesign must fix?
   - 🔵 Modernization: What is the UI parity target per feature — full behavioral parity or intentional differences? How will users be transitioned and retrained? How will legacy and new screens be distinguishable during dual-running? Which screens are retired, and when?

6. **Propose the design foundation** based on the analysis. This is the design-level equivalent of the architecture's software stack — the decisions everything else builds on:

   - **Design system approach** — adopt an existing corporate/standard design system (e.g., Material, Carbon, Fluent, in-house system), extend one, or build new. Consider: architecture's component library, brand constraints 🟤🔵 existing UI.
   - **Component library & version** — which library implements the design system, its maturity, and the mapping to the architecture's frontend framework.
   - **UI framework alignment** — confirm the design is buildable with the architecture's chosen frontend framework and its capabilities/limitations.
   - **Design tooling** — where the design lives (Figma, Sketch, Adobe XD) and how tokens are managed (Figma tokens, Style Dictionary).
   - **Accessibility target** — standard and conformance level (e.g., WCAG 2.1 AA, EN 301 549), traced to SRS NFRs and compliance constraints.
   - **Visual direction** — typography, color philosophy, density, and the token source of truth.
   - **Navigation paradigm** — top-level navigation structure (sidebar, top bar, bottom tabs, hub-and-spoke) derived from the information architecture and platform conventions.
   - **Usability validation approach** — prototype fidelity, testing method, and participant sourcing.

   For each foundation decision, document: the choice, alternatives considered, rationale (tracing to SRS requirements, NFRs, architecture decisions, and constraints), and any constraints that drove the decision.

7. **Build a design readiness map** — for each section, tag readiness:
   - 🟢 **Design-Ready**: Information is detailed, specific, and sufficient to make justified design decisions.
   - 🟡 **Partially Ready**: Information exists but is too vague, incomplete, or needs design interpretation.
   - 🔴 **Not Ready**: Missing, unquantified, or based on unsupported assertions — cannot make design decisions without clarification.

   Sections with 🔴 readiness are priority candidates for Phase 2 questions.

### Phase 2: Clarification Questions & Design Foundation Alignment

Before generating the document, ask the user targeted questions for every **Partially Covered**, **Gap**, **Contradiction**, or **Not Ready** area identified in Phase 1. **Crucially, also present the proposed design foundation for user alignment.**

#### Question Design Principles

- **Ask open questions** that invite thoughtful responses and deeper thinking — not yes/no questions.
- **Always suggest 2–3 possible valid answers** for each question to help the user think through the options and to demonstrate understanding of the domain.
- **Contextualize each question** — briefly explain why the information matters for the design and what happens if it remains unanswered (e.g., "Without measurable UX targets, the design cannot be validated before implementation, and 'usability' remains an unverifiable claim").
- **Group questions by template section** so the user can address them systematically.
- **Prioritize questions** — mark questions as:
  - **[Critical]**: Blocks design decision-making — the design document cannot be generated for this section without this information. The decision would be arbitrary or unjustified.
  - **[Important]**: Affects the quality, justification, or consistency of design decisions. Decisions can be made but will have weak rationale or unverified assumptions.
  - **[Optional]**: Refines the design but does not block decision-making. Can be documented as an assumption with a validation plan.
- **Reference the source** of the contradiction or gap (e.g., "The SRS defines FR-042 requiring offline data entry, but the architecture and platform constraints list only a responsive web application — this creates a fundamental contradiction about the delivery platform").
- **Surface implicit design decisions** — when a requirement, use case, or workflow implies a design pattern that isn't explicitly stated, propose the implied design and ask the user to confirm, challenge, or refine it (e.g., a multi-step approval use case implies a wizard with progress saving and resume behavior).
- **Challenge UX-unfriendly requirements** — when existing information contains requirements that produce poor user experiences (e.g., mandatory 15-field forms without grouping, error messages without recovery guidance, disproportionate approval chains), flag them and ask for clarification or redesign.
- **Do not ask questions that can be answered by reading existing documentation** — if the answer exists in a file the skill has already read, use that information directly.
- **Distinguish between information that must be resolved now vs. information that can be documented as assumptions with validation plans** — for [Optional] questions, offer to proceed with a stated assumption.

#### Design Foundation Alignment Questions

Present the proposed design foundation as a dedicated question block. For each foundation decision:

- State the proposal.
- State the rationale (tracing to SRS requirements, NFRs, architecture decisions, and constraints).
- State the alternatives considered and why they were rejected.
- Ask the user to confirm, challenge, or suggest alternatives.
- If the user's team has specific expertise, preferences, or brand commitments that differ from the proposal, adjust the recommendation.

Format the design foundation question as:

---

**[Critical] Sections 2.3, 3.2, 8 & 9 — Design Foundation**

Based on the analysis of the SRS requirements, the architecture's technology decisions, the brand constraints, and the NFRs, the following design foundation is proposed. Each choice traces to specific requirements and constraints. Please review and confirm, challenge, or suggest alternatives for each.

| Element | Proposal | Rationale | Alternatives Considered | Trace |
|---------|----------|-----------|------------------------|-------|
| Design System | [e.g., extend in-house DS v2.3] | [rationale] | [alt1, alt2] | [FR/NFR/Architecture refs] |
| Component Library | [library + version] | [rationale] | [alt1, alt2] | [Architecture decision, NFR refs] |
| UI Framework Alignment | [framework from architecture] | [rationale] | [alt1, alt2] | [Architecture Section 5.1] |
| Design Tooling | [e.g., Figma + Style Dictionary tokens] | [rationale] | [alt1, alt2] | [workflow constraints] |
| Accessibility Target | [e.g., WCAG 2.1 AA] | [rationale] | [alt1, alt2] | [NFR-xxx, regulation] |
| Visual Direction | [e.g., corporate brand tokens, 8px spacing grid] | [rationale] | [alt1, alt2] | [brand guidelines] |
| Navigation Paradigm | [e.g., persistent sidebar + contextual breadcrumbs] | [rationale] | [alt1, alt2] | [use case structure] |
| Usability Validation | [e.g., moderated remote tests, 5 users/round] | [rationale] | [alt1, alt2] | [NFR-xxx, UX goals] |

Suggested responses:
- *Option A*: "I confirm the proposed design foundation — proceed with these decisions in the design document."
- *Option B*: "I want to adjust specific foundation decisions — [specify which ones and preferred alternatives]."
- *Option C*: "I need more information to decide — provide deeper comparison of alternatives for [specific elements]."
- *Custom*: [your own answer]

---

#### Question Template

For each non-foundation question, use this format:

---

**[Priority] Section X.Y — [Topic]**

[Context: Why this matters for the design and what happens if unanswered]

[The open question]

Suggested answers:
- *Option A*: [description and implications for the design]
- *Option B*: [description and implications for the design]
- *Option C*: [description and implications for the design]
- *Custom*: [your own answer]

---

#### Minimum Required Questions by Project Type

**All project types** must resolve these before the design document can be generated:

- What is the core purpose of the product — what problem does it solve for whom, and what does success look like for users?
- What is the project type classification (🟢 🟤 🔵) and what are its design implications?
- What are the top 3–5 UX quality goals with specific, measurable targets (task success rate, time-on-task, SUS, error rate)?
- What is the accessibility compliance level, and is it driven by law or by policy?
- What is the proposed design foundation, and does the user align with it?
- What are the primary user tasks, in priority order, that the flows (Section 6.1) must cover?
- What is the navigation paradigm and top-level information structure?
- Which platforms and devices are in scope, and what is the browser/device support matrix?
- How will the design be validated (usability testing approach, participants, metrics)?
- What are the key UX risks and how will they be mitigated?

**Green Field (🟢) additional questions:**
- What is the design system starting point — build new, adopt a standard system, or extend a corporate system?
- What brand assets and visual direction inputs exist (logos, colors, typography, tone of voice), and who owns them?
- What is the complete screen inventory implied by the SRS feature areas, and are there gaps?
- Who writes and approves UI copy, including empty states, error messages, and onboarding content?
- What are the foundational UX patterns to establish before feature screens (forms, tables, modals, feedback, navigation)?

**Brown Field (🟤) additional questions:**
- What is the existing UI baseline — screens, interaction patterns, keyboard shortcuts, terminology — that users depend on?
- Which existing usability complaints (from research, analytics, support tickets) must the redesign fix, and which patterns must be preserved to avoid retraining?
- How will new screens stay visually and behaviorally coherent with existing screens that are not redesigned?
- What are the constraints from the existing component library or design system during the transition?
- What is the impact of the redesign on existing users who are not the target of the new features?

**Software Modernization (🔵) additional questions:**
- What is the UI parity target per feature — full behavioral parity, partial parity with intentional improvements, or capability parity (same information achievable through better means)?
- How will users be transitioned — retraining plan, onboarding content, in-product guidance, parallel access to legacy and new UIs?
- How will legacy and new screens be distinguishable during dual-running, and how is user confusion prevented?
- Which legacy screens are retired, on what schedule, and what guidance screens replace them during transition?
- How will UX parity be verified — parallel task testing, SUS comparison against the legacy baseline, task success benchmarks?

### Phase 3: Document Generation

Once all critical and important questions are resolved and the design foundation is aligned with the user, generate the UI/UX Design document.

#### Generation Rules

1. **Use the template structure exactly** — follow `templates/design/ui-ux-design.md` section by section, including all subsections.
2. **Replace all `<!-- -->` placeholders** with project-specific content derived from the analysis and user answers.
3. **Mark sections as [APPLICABLE] or [NOT APPLICABLE]** based on the project type classification. For [NOT APPLICABLE] sections, include a one-line rationale (e.g., "[NOT APPLICABLE] — Green Field project with no legacy UI to constrain the design").
4. **For 🟤🔵 sections**, populate them if the project type matches; otherwise mark [NOT APPLICABLE].
5. **Fill every table** with concrete, specific content — no placeholder values remaining in the final document.
6. **Write the Executive Summary (Section 1) last** — after all other sections are complete, synthesize the design vision, top UX goals, platforms, accessibility level, constraints, and risks.
7. **Every design element must be traceable** — each screen, flow, and pattern traces to at least one SRS requirement (FR, UC, NFR, or IR ID) in the trace columns. Design elements without requirements are flagged as scope creep; requirements without design elements are coverage gaps to report.
8. **The design must be buildable within the architecture** — every design decision must be consistent with the architecture's frontend framework, component library, performance budgets, and API contracts. Where the design needs something the architecture doesn't provide, flag it explicitly as a cross-document issue rather than silently assuming it.
9. **Every user flow (Section 6.1) must include**: actor/persona, trigger, complete main success scenario with screen references, alternative flows, and exception flows with error presentation and user recovery. Exception flows are mandatory — a flow without error handling is incomplete.
10. **Every screen must have all states specified** (Section 6.3) — empty, loading, error, success, partial data, and where applicable offline and permission-denied. A screen without states is not fully designed.
11. **Every color token (Section 8.1) must state its contrast ratio** against its standard background and the WCAG level it passes — these must satisfy the accessibility targets (Section 9.1).
12. **Every UX metric (Section 12) must be specific and measurable with a measurement method** — avoid "the UI shall be easy to use." Write "task success rate ≥ 90% for the top 3 tasks in moderated usability testing with 5 participants per persona."
13. **Prefer relevance over completeness for wireframes and mockups (Section 7)** — fully specify important, risky, complex, or high-traffic screens; simple or standard screens may reference the design system and be documented more briefly.
14. **Cross-reference between sections** — when content in one section depends on another, reference it (e.g., "The empty-state illustration is specified in Section 8.3; the empty-state copy standard in Section 5.3; the state table entry in Section 6.3").
15. **For 🟤🔵: always distinguish existing from new/redesigned/retired screens** — use the Change Type columns (Section 5.1, 6.1, 8.2) and the Legacy UI Constraints (Section 3.4), Terminology Parity (Section 5.3), and Design Technical Debt (Section 14.3) sections.
16. **For 🔵: populate the migration UX content** — transition states (Section 6.3), rollout UX phasing (Section 13), parity verification method (Section 11.2), and baseline-relative metrics (Section 12).
17. **The usability findings loop (Section 11.2) must close** — every finding must map to a design change with status (open / changed / deferred). Findings without design responses are open risks (Section 14.2).
18. **Keep the tone actionable for implementation** — the document is a handoff specification. Every statement should be verifiable by a developer or tester (Section 13 handoff items).
19. **Save the generated document** to `documentation/ui-ux-design.md` (suggested).

#### Screen & Flow Writing Guidelines

- Each screen has a single primary purpose — if a screen serves two unrelated purposes, split it.
- Primary actions are visually dominant and limited (one primary action per view where possible); secondary and tertiary actions are clearly distinguished.
- Every step in a flow identifies the user action, the system response, and the screen (SCR ID) — steps without screen references cannot be implemented or tested.
- Error messages follow the Section 5.3 content standards: state what happened, why, and what the user can do next — never blame the user.
- Forms are designed with progressive disclosure: only required fields visible by default, advanced options grouped, inline validation on blur with field-level error text.
- 🟤🔵: flows that change from the legacy system include a change description and a user transition note (what users must learn differently).

#### Design Token & Component Writing Guidelines

- Tokens are semantic, not literal — "color-surface", "color-text-primary", "spacing-md" — and map to the brand values.
- Each token's contrast ratio is measured against its actual standard usage background, not an idealized one.
- Components specify all interactive states (default, hover, active, focus, disabled, error, loading) — a component missing states will be implemented inconsistently.
- 🟤🔵: components reused from the existing library are marked as reused; components intentionally changed are marked with the change and its user impact.

#### Accessibility Writing Guidelines

- Targets are stated as verifiable criteria with validation methods (automated audit + manual screen-reader matrix + assistive-technology user testing where required).
- Accessibility is written into the practices (Section 9.2) as design rules, not as a post-hoc checklist.
- 🟤🔵: known accessibility gaps of the legacy system are documented as targets the redesign must close.

#### Quality Checks Before Delivery

After generating the document, perform these self-checks:

- [ ] Every section is either populated with project-specific content or marked [NOT APPLICABLE] with rationale.
- [ ] No `<!-- -->` placeholders remain (except the document status, date, and sign-off fields that require human input).
- [ ] The Executive Summary (Section 1) accurately reflects the full document — design vision, top UX goals, platforms, accessibility level, constraints, and risks are correctly summarized.
- [ ] The project type classification in Section 2.2 is consistent with how 🟢🟤🔵 sections are handled throughout the document.
- [ ] Every screen in the inventory (Section 5.1) traces to at least one SRS requirement, and every UI-relevant SRS requirement traces to at least one screen or flow.
- [ ] Every flow (Section 6.1) includes main success, alternative, and exception paths with valid screen references.
- [ ] Every screen has all UI states specified (Section 6.3), including offline and permission-denied where applicable.
- [ ] Every interaction pattern (Section 6.2) has a behavior specification, not just a name.
- [ ] The navigation model (Section 5.2) covers global, local, and contextual navigation and matches the screen hierarchy.
- [ ] Every color token (Section 8.1) has a contrast ratio that satisfies the accessibility targets (Section 9.1).
- [ ] The accessibility targets (Section 9.1) are verifiable, with named validation methods.
- [ ] The responsive design (Section 7.3) covers all platforms and devices in the SRS and architecture.
- [ ] Every UX metric (Section 12) has a target, a measurement method, and traces to a flow, screen, or NFR.
- [ ] The usability test plan (Section 11.2) specifies tasks, participants, metrics, and the findings → design-change loop.
- [ ] The handoff section (Section 13) lists all design artifacts, component mappings, and the implementation Definition of Done.
- [ ] Every risk (Section 14.1) has likelihood, impact, mitigation, and owner; every open issue (Section 14.2) has a decision deadline and owner.
- [ ] The design foundation is consistent throughout the document (tokens, components, framework, accessibility target in Sections 3, 5–9, and 13).
- [ ] No contradictions exist between sections or with the SRS/architecture (if they do, flag them explicitly).
- [ ] For 🟤🔵: existing screens have Change Type, legacy constraints are documented, and terminology parity or rename plans exist.
- [ ] For 🔵: transition states, rollout UX phasing, parity verification, and screen retirement schedules are populated.
- [ ] The glossary (Section 15) covers all design-specific terms used in the document, including 🟤🔵 legacy terminology mappings.

### Phase 4: Post-Generation Review

After the document is generated:

1. **Present the document** to the user.
2. **Highlight key design judgments made** during generation — where the skill made interpretive calls (e.g., deriving a navigation paradigm from use case structure, splitting a compound screen, inferring empty-state behavior, choosing flow priorities where they were unspecified), point them out so the user can verify.
3. **Present the design summary** clearly — design vision and principles, screen inventory (count and structure), key flows, design foundation, accessibility level, validation approach, and top UX risks.
4. **Flag remaining uncertainties** — any areas where information was insufficient and assumptions were made. Indicate the risk each assumption poses to the design and suggest validation activities (usability tests, contrast audits, prototype validation with users).
5. **Present the traceability** — show how screens and flows map to SRS requirements, how UX goals map to design decisions, and highlight coverage gaps (requirements without design, design without requirements).
6. **Flag implicit design decisions** — decisions that were not explicitly stated in preceding documents but were inferred from requirements, use cases, or best practices. These are the most likely to be contested and should be reviewed carefully.
7. **Flag cross-document issues** — where the design requires something the architecture or SRS doesn't provide (or contradicts them), so they can be resolved before implementation.
8. **Identify UX risks** that require active mitigation — risks with High likelihood or Major impact. Suggest specific mitigation activities.
9. **Offer to refine** any section the user wants to adjust.
10. **Suggest next steps** — e.g., stakeholder design review, usability test round 1, handoff to frontend implementation, design system implementation, user training/onboarding material creation, test concept creation for UX acceptance criteria.

## Examples

### Example Question (Design Foundation Alignment — Green Field)

---

**[Critical] Sections 2.3, 3.2, 8 & 9 — Design Foundation**

Based on the analysis of the SRS requirements (FR-001–FR-045), the architecture's frontend decision (React 18 + Next.js), the brand guidelines, and NFR-U01 (accessibility conformance), the following design foundation is proposed. Please review and confirm, challenge, or suggest alternatives for each.

| Element | Proposal | Rationale | Alternatives Considered | Trace |
|---------|----------|-----------|------------------------|-------|
| Design System | Extend Material Design 3 with a corporate theme layer | Mature components, comprehensive accessibility support, large ecosystem, matches React architecture | Build new system (6+ months effort, high risk), adopt Carbon (enterprise-look mismatch with brand) | NFR-U02 (time-to-market), brand guidelines v3.1 |
| Component Library | MUI v6 (Material for React) | Native React/Next.js compatibility; TS support; theming via CSS variables | Chakra (smaller ecosystem), shadcn/ui (copy-in model, higher maintenance) | Architecture Section 5.1 (React decision) |
| Design Tooling | Figma + Style Dictionary tokens | Live collaboration; token export to CSS variables; matches team tooling | Sketch (macOS-only handoff), XD (declining ecosystem) | Team workflow constraint |
| Accessibility Target | WCAG 2.1 AA, verified per release | NFR-U01 mandates AA; EAA compliance required for EU market | WCAG 2.2 AA (adds focus target rules — recommended for phase 2), AAA (not practical for all content) | NFR-U01, Section 508/EAA |
| Visual Direction | Corporate brand palette + Inter typeface, 8px spacing grid | Brand manual specifies palette; Inter is open-license with variable weights | Brand typeface licensing pending — fallback system font stack | Brand guidelines v3.1 |
| Navigation Paradigm | Persistent sidebar (desktop) → bottom tabs (mobile), contextual breadcrumbs | Use case structure has 5 top-level areas; supports deep workflows with orientation | Top bar only (insufficient for 5 areas), hub-and-spoke (more clicks for frequent tasks) | UC-001–UC-023 structure, UX-QG-1 (task efficiency) |
| Usability Validation | Moderated remote tests, 5 users per round, 3 rounds | Standard sample for qualitative findings; remote matches distributed users | Unmoderated panel (cheaper but shallower), lab tests (cost) | UX-QG-2 (SUS ≥ 75) |

Suggested responses:
- *Option A*: "I confirm the proposed design foundation — proceed with these decisions in the design document."
- *Option B*: "I want to adjust specific foundation decisions — [specify which ones and preferred alternatives]."
- *Option C*: "I need more information to decide — provide deeper comparison of alternatives for [specific elements]."
- *Custom*: [your own answer]

---

### Example Question (Gap — No Measurable UX Goals)

---

**[Important] Sections 2.5 & 12 — UX Quality Goals with Measurable Targets**

The SRS states NFR-U02 "the system should be intuitive and user-friendly," but provides no measurable targets. The design cannot be validated against unquantified goals — "user-friendly" cannot be tested, and every design trade-off (information density, number of steps, progressive disclosure) depends on specific targets. Without measurable goals, the UX Metrics section (Section 12) has no acceptance criteria and the usability tests (Section 11.2) have nothing to verify.

What are the specific, measurable UX quality goals the design must satisfy?

Suggested answers:
- *Option A*: "Task success: ≥ 90% of trained users complete the top 3 frequent tasks without assistance in moderated testing. Efficiency: median time-on-task < 60s for each of those tasks. Learnability: first-time users complete the top task within 3 minutes with no more than 2 missteps. Satisfaction: SUS ≥ 75 after first-week usage. Error: < 5% of form submissions rejected by validation. These targets derive from the business case's productivity assumptions and industry benchmarks (SUS 68 = average)."
- *Option B*: "Match or exceed the current system's measured baseline: task success currently 72%, target ≥ 85%; median time-on-task currently 140s, target < 90s; SUS currently 58, target ≥ 70. Baselines from the analytics report and the legacy SUS survey (n=40). These are Should Have targets — parity-plus improvements prioritized by the top user complaints (search speed, multi-step order entry)."
- *Option C*: "No calibrated targets exist yet. The design should adopt industry-standard placeholder targets (task success ≥ 90%, SUS ≥ 75, time-on-task < 90s for top tasks), document them as assumptions, and schedule a target calibration workshop with stakeholders before usability round 1. The usability test plan should collect baseline data in round 1 to calibrate phase-2 targets."
- *Custom*: [your own answer]

---

### Example Question (Contradiction — Platform Conflict Between SRS and Architecture)

---

**[Critical] Sections 3.2, 5.1 & 7.3 — Platform Contradiction: Offline Mobile Data Entry vs. Web-Only Architecture**

The SRS defines FR-042: "The system shall allow field staff to record inspection results without network connectivity and synchronize when reconnected." However, the architecture's deployment view and technology decisions specify a responsive web application only, and the constraint list states "no native mobile apps for the initial release." This is a fundamental contradiction: offline data entry on mobile devices requires either a native app, an installable PWA with offline storage, or a scope reduction. The design cannot specify screens, states (offline!), and flows for this requirement without resolving the platform question.

How should the offline data entry requirement be resolved?

Suggested answers:
- *Option A*: "PWA with offline storage — the architecture adds a service worker with IndexedDB offline queue and background sync. The design specifies the offline UI states (Section 6.3): a persistent offline banner, locally cached forms, sync status indicators, and conflict-resolution screens for data changed both locally and remotely. This requires an architecture amendment (flagged as a cross-document issue) but keeps the web-only stack. The design should only proceed with this option once the architecture team confirms the service worker scope."
- *Option B*: "Scope reduction with a bridge solution — the initial release supports online-only data entry; field staff record results on paper forms and enter them on return to connectivity. The design adds an efficient bulk-entry screen (batch import of paper results) as the bridge, and FR-042 is re-planned for a later phase as a PWA enhancement. The SRS requirement is marked 'deferred' with a documented scope decision."
- *Option C*: "Native companion app for field staff only — a minimal iOS/Android app covering inspection recording and sync, while the main product remains web. This contradicts the current architecture constraint, so the constraint must be renegotiated. The design document should specify the companion app's screens and flows and mark the architecture conflict as a blocking issue for the project decision board."
- *Custom*: [your own answer]

---

### Example Question (Implicit Design Decision — Wizard Flow Implied by Use Case)

---

**[Important] Sections 6.1 & 6.2 — Approval Workflow: Wizard Flow Implied**

The SRS defines UC-014 "Submit budget request for approval" with a main scenario of 6 steps including entering line items, attaching justification documents, and routing to two sequential approvers, plus alternative flows for saving incomplete requests and recalling submissions. No document specifies how this multi-step, resumable interaction is presented. The use case implies a wizard-like interaction with draft persistence and recall — but a wizard is only one option, and the choice affects data loss prevention, validation timing, and the approval status screens.

How should the multi-step budget request interaction be designed?

Suggested answers:
- *Option A*: "Stepped wizard with draft autosave — 4 steps (Requester & Period, Line Items, Justification, Review & Submit), each validated before proceeding, autosave on every step with a 'resume draft' entry point on the dashboard. Recall is a status action on the submitted request with an audit trail. This fits the sequential nature of the use case and protects against data loss. Flow: FLOW-007 (submit), FLOW-008 (recall), with states for draft, submitted, in approval, recalled."
- *Option B*: "Single-page form with section anchoring — one long page with anchored sections, inline validation, autosave, and a sticky summary sidebar showing completeness and approver routing live. Fewer steps and better overview for experienced users, but higher cognitive load for first-time users; mitigate with a first-run guided tour. Fits the power-user persona P2 (70% of submissions)."
- *Option C*: "Defer the pattern decision — the design document specifies the required capabilities (step validation, autosave, resume, recall with audit) as acceptance criteria (Section 12) and marks the concrete pattern (wizard vs. single-page) as an open issue (Section 14.2) to be resolved by A/B testing in usability round 2. Prototype both variants."
- *Custom*: [your own answer]

---

### Example Question (Brown Field — Legacy UX Parity Ambiguity)

---

**[Critical] Sections 3.4, 5.3 & 14 — Legacy UI Constraints: Undocumented Keyboard Workflow**

For this Brown Field enhancement of the order entry system, research and support tickets show that experienced order clerks (persona P1, ~60% of order volume) rely on undocumented keyboard workflows in the legacy UI: tab-order shortcuts, a quick-code field for products, and Enter-to-submit. No formal documentation of these patterns exists — they are tribal knowledge. The enhancement redesigns the order entry screen, and the SRS says the redesign "must not slow down experienced users," but this is untestable as stated. The design cannot proceed without knowing exactly which legacy behaviors constitute the efficiency baseline and whether they must be preserved.

Which legacy interaction patterns must be preserved in the redesigned order entry screen, and how is "not slowing down experienced users" measured?

Suggested answers:
- *Option A*: "Preserve and formalize the keyboard workflow: the redesign must support tab-order navigation, product quick-codes, and Enter-to-submit, plus a keyboard shortcut map documented in the help center (fixing the tribal-knowledge problem). Measure efficiency: median order entry time ≤ legacy baseline (112s, measured from analytics) with ≥ 90% task success. The redesign adds the same efficiency via modern patterns (command palette, autosuggest) but the legacy fast paths remain functional during transition."
- *Option B*: "Redesign the workflow with modern efficiency patterns and accept a transition period: replace quick-codes with autosuggest search (fewer memorized codes, faster onboarding of new clerks), keep tab-order and Enter-to-submit. Accept a temporary slowdown for P1 users during retraining (target: within 2 weeks, P1 median time ≤ 125s, converging to ≤ 112s within 6 weeks). Provide in-product migration tips on first use. This is an intentional, managed behavioral change with a measured transition plan."
- *Option C*: "Dual-path during transition: the redesigned screen offers both the legacy fast paths (quick-code field, keyboard submit) and the new autosuggest flow; usage analytics track which path each user takes. After 8 weeks, evaluate adoption data and retire the least-used path. The design document specifies both paths in Section 6.2 with their retirement plan in Section 13."
- *Custom*: [your own answer]

---

### Example Question (Modernization — UI Parity Target)

---

**[Critical] Sections 11.2, 13 & 14 — UI Parity Target for Migrated Features**

The project scope states "100% feature parity at cutover" for the customer portal migration, but the modernized portal intentionally replaces the legacy navigation structure (nested menu tree, 4 levels deep) with a flat information architecture and global search, and legacy reports render in a fixed table format that the new system renders responsively. These are intentional behavioral differences — yet users have 12 years of navigation habit. The SRS requires parity verification, but the parity target is ambiguous: must users be able to perform identical actions in identical ways, or achieve identical outcomes through better means?

What is the precise UI parity target for the migrated portal features?

Suggested answers:
- *Option A*: "Capability parity with a managed transition — all legacy capabilities must be achievable in the new portal (measured by a task matrix: each legacy task executable with equal or better success rate), but the path may differ (flat navigation + search instead of menu tree; responsive reports instead of fixed tables). Verification: parallel task testing of the 25 most frequent legacy tasks, with success rate and time-on-task compared against the legacy baseline. Users receive task-mapping training materials ('How to do X in the new portal')."
- *Option B*: "Full behavioral parity for the top 10 frequent tasks, capability parity for the long tail — the most business-critical workflows (order tracking, invoice download, address change) keep familiar structures and terminology to minimize retraining for the majority of traffic; less frequent features may change paths. Verification: behavioral tests for the top 10, capability tests for the rest."
- *Option C*: "Strict behavioral parity as a hard requirement — every migrated feature behaves identically to the legacy UI (including the nested navigation and fixed-format reports). The redesign is limited to visual refresh and technology change. This minimizes user risk and retraining but forfeits the UX improvements that motivated part of the modernization business case — flag the trade-off for the decision board."
- *Custom*: [your own answer]

---

## Anti-Patterns to Avoid

- **Don't generate the document without asking questions** — the design's value is in the rigorous analysis and justified decisions, not in filling a template.
- **Don't propose the design foundation without user alignment** — the design system, accessibility target, and visual direction are the most consequential design decisions and must be confirmed by the user.
- **Don't design outside the architecture's constraints** — a design that requires native mobile features, real-time collaboration, or performance the architecture doesn't deliver is not implementable. Flag cross-document issues instead of assuming them away.
- **Don't produce vague UX goals** — "intuitive", "user-friendly", and "modern look" are not design goals. "Task success ≥ 90% for the top 3 tasks in moderated testing" is.
- **Don't skip exception flows** — a flow without error presentation and user recovery is an incomplete design, not a shortcut.
- **Don't skip UI states** — a screen without empty, loading, and error states will be implemented inconsistently. State design is part of the screen, not an afterthought.
- **Don't specify colors without contrast ratios** — every color token must state its contrast ratio and WCAG conformance against its actual usage background.
- **Don't treat accessibility as a checklist at the end** — accessibility targets are design constraints that shape tokens, components, and flows from the start.
- **Don't ask questions that existing documentation already answers** — read carefully and use available information directly.
- **Don't ask too many questions at once** — batch by priority, lead with critical questions (especially the design foundation), offer to proceed with assumptions for lower-priority items.
- **Don't duplicate content from the SRS** — the design document translates requirements into screens, flows, and visual language; it does not restate them. Reference the SRS with IDs.
- **Don't mark sections [NOT APPLICABLE] just because they're hard to populate** — only mark them if they genuinely don't apply to the project type.
- **Don't present hi-fi mockups before structure is validated** — validate information architecture and flows with lo-fi artifacts and prototypes first; the document should reflect this sequence.
- **Don't write the Executive Summary first** — write it last, after all design analysis is complete and decisions are justified.
- **Don't forget 🟤🔵 sections** — for Brown Field and Modernization projects, legacy constraints, parity targets, terminology mapping, transition states, and user retraining are essential, not optional.
- **Don't design decoration-only motion** — every animation must have a purpose (orientation, feedback, continuity) and a reduced-motion fallback.
- **Don't skip the usability validation plan** — a design without a validation approach cannot demonstrate that it meets its UX goals; Section 11 is not optional filler.
- **Don't ignore user transition 🟤🔵** — a technically correct redesign that strands existing users without guidance, retraining, or preserved fast paths is a UX failure.

## Document Hierarchy Context

The UI/UX Design document is the **sixth or seventh** formal document in the project lifecycle, depending on which preceding documents were produced. It builds upon and elaborates:

| Document | Relationship | Precedes UI/UX Design? |
|----------|-------------|------------------------|
| **Viability Study** | Determines whether the project is feasible — the design must respect the viability study's user-facing assumptions | Yes — the design should be consistent with the viability study's user and market assumptions |
| **Business Case** | Defines the investment case — the design must support the benefit assumptions (e.g., productivity gains imply measurable task efficiency targets) | Yes — UX quality goals should trace to business case success criteria |
| **Project Scope** | Defines delivery boundaries — the design covers only in-scope screens and flows, phased per delivery plan | Yes — the screen inventory and flow priorities respect scope boundaries and MoSCoW |
| **SRS** | Defines what the system must do — the design specifies how users will do it. Sections 8.5 (UI requirements), 3.1/3.2 (personas/actors), 5 (use cases), and 9 (NFRs) are the primary inputs | Yes — every design element traces to SRS requirements |
| **User Stories** | Define delivery units — story flows and priorities shape flow prioritization and screen phasing | Yes — flows should align with story sequences |
| **Software Architecture** | Defines how the system is built — the frontend framework, component library, performance budgets, and API contracts constrain what the design can specify | Yes — the design must be buildable within the architecture's technology decisions |

And it precedes:

| Document | Relationship | Follows UI/UX Design? |
|----------|-------------|----------------------|
| **Frontend Implementation** | Implements the screens, flows, tokens, and components as specified | Yes — implementation derives from the design specification and handoff (Section 13) |
| **Sprint Backlogs** | Decompose the design into implementable work items per screen/flow | Yes — stories depend on specified screens and flows |
| **Usability Test Cases / Test Concept** | Verify the UX acceptance criteria (Section 12) and accessibility targets (Section 9) | Yes — test cases derive from flows, states, and metrics |
| **User Training & Rollout Materials** | Onboard users to the new experience 🟤🔵 | Yes — training content derives from flows, terminology, and transition design |

When generating the UI/UX design document, keep in mind that its primary output is a **complete, justified, buildable, and internally consistent design specification** that developers can implement and testers can verify. The design document is the user-facing blueprint — it translates requirements into concrete screens, flows, interaction patterns, and visual language that enable the team to build the right experience in the right way.
