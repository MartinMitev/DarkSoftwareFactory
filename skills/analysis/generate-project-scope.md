# Skill: Generate Project Scope Document

## Description

Generates a complete, high-quality Software Project Scope document based on the template `templates/analysis/project-scope.md`. The skill deeply analyzes all available project information (viability studies, business cases, existing documentation, codebase, stakeholder inputs) to populate every applicable section of the template. When gaps, unclear statements, or contradictions are detected, the skill asks targeted open questions with suggested valid answers before proceeding.

## Activation

When the user requests to create, generate, or draft a project scope document for a software project.

## Instructions

### Phase 1: Information Gathering & Analysis

1. **Read the template** at `templates/analysis/project-scope.md` to understand the full structure, all sections, and expected content.

2. **Discover and read all existing project information:**
   - Search the workspace for any viability study documents (check `documentation`, project folders, or any `.md` files with "viability" in the name).
   - Search for any business case documents (check `documentation`, project folders, or any `.md` files with "business-case" or "business_case" in the name).
   - Search for any existing requirements documents, architecture decision records (ADRs), README files, or project documentation.
   - Search for any configuration files (`package.json`, `pom.xml`, `build.gradle`, `docker-compose.yml`, etc.) that reveal the technology stack and system boundaries.
   - If a codebase exists, explore the directory structure to understand current modules, services, and integrations.
   - Search for any stakeholder communication, meeting notes, or decision logs.

3. **Classify the project type** based on available evidence:
   - **Green Field**: No existing codebase; new product being built from scratch.
   - **Brown Field**: Existing system being extended, refactored, or enhanced.
   - **Software Modernization**: Legacy system being migrated, re-platformed, or re-architected.
   - If classification is ambiguous, note this as a question for Phase 2.

4. **Map existing information to template sections.** For each section of the template, determine:
   - **Covered**: Sufficient information exists to populate the section.
   - **Partially Covered**: Some information exists but is incomplete or ambiguous.
   - **Gap**: No information exists for this section.
   - **Contradiction**: Information from different sources conflicts.

5. **Perform gap-contradiction analysis:**
   - Cross-reference the viability study's findings with the business case's recommendations — do they align on scope boundaries, project type, and key deliverables?
   - Check if the business case's recommended option matches the scope being defined — are there features or requirements implied by the business case that are not explicitly scoped?
   - Verify that the objectives in the business case are specific enough to derive scope items from — vague objectives create scope ambiguity.
   - Check if the current system assessment (for Brown Field / Modernization) is detailed enough to define feature parity expectations and migration scope.
   - Verify that cost estimates and resource constraints from the business case are consistent with the scope being proposed.
   - Identify any assumptions in preceding documents that, if wrong, would materially change the scope.

### Phase 2: Clarification Questions

Before generating the document, ask the user targeted questions for every **Partially Covered**, **Gap**, or **Contradiction** identified in Phase 1.

#### Question Design Principles

- **Ask open questions** that invite thoughtful responses, not yes/no questions.
- **Always suggest 2–3 possible valid answers** for each question to help the user think through the options and to demonstrate understanding of the domain.
- **Contextualize each question** — briefly explain why the information matters for the scope document and what happens if it remains unanswered.
- **Group questions by template section** so the user can address them systematically.
- **Prioritize questions** — mark questions as [Critical] (blocks scope definition), [Important] (affects scope quality), or [Optional] (refines scope but not blocking).
- **Reference the source** of the contradiction or gap (e.g., "The viability study assumes X, but the business case implies Y").
- **Do not ask questions that can be answered by reading existing documentation** — if the answer exists in a file the skill has already read, use that information directly.

#### Question Template

For each question, use this format:

---

**[Priority] Section X.Y — [Topic]**

[Context: Why this matters and what happens if unanswered]

[The open question]

Suggested answers:
- *Option A*: [description and implications for scope]
- *Option B*: [description and implications for scope]
- *Option C*: [description and implications for scope]
- *Custom*: [your own answer]

---

#### Minimum Required Questions by Project Type

**All project types** must resolve these before document generation can proceed:
- What is the precise scope statement? (What will be delivered, for whom, by when — in one sentence)
- What are the MoSCoW priorities for the top-level scope items?
- What are the most important explicit out-of-scope items?
- What is the Definition of Done for this project?
- What are the acceptance criteria for the primary deliverable?

**Green Field (🟢) additional questions:**
- What defines the Minimum Viable Product (MVP) vs. later releases?
- What is the system boundary — where does the new system end and the external world begin?
- Which technology and architecture decisions are already made vs. still open?

**Brown Field (🟤) additional questions:**
- What is the baseline version of the existing system that scope is measured against?
- Which existing features must be preserved unchanged, which must be modified, and which are being retired?
- What backward compatibility constraints apply?

**Software Modernization (🔵) additional questions:**
- What is the feature parity target — 100% parity at cutover, or is partial parity acceptable for some features?
- What is the migration approach (big bang, phased, parallel run, strangler fig)?
- What is the legacy decommission timeline and criteria?
- What is the rollback strategy if the migration fails?

### Phase 3: Document Generation

Once all critical and important questions are resolved, generate the project scope document.

#### Generation Rules

1. **Use the template structure exactly** — follow `templates/analysis/project-scope.md` section by section.
2. **Replace all `<!-- -->` placeholders** with project-specific content derived from the analysis and user answers.
3. **Mark sections as [APPLICABLE] or [NOT APPLICABLE]** based on the project type classification. For [NOT APPLICABLE] sections, include a one-line rationale (e.g., "[NOT APPLICABLE] — Green Field project with no existing system to migrate").
4. **For 🟤🔵 sections**, populate them if the project type matches; otherwise mark [NOT APPLICABLE].
5. **Fill every table** with concrete, specific content — no placeholder values remaining in the final document.
6. **Write the Executive Summary last** — after all other sections are complete.
7. **Ensure full traceability**: every scope item in Section 4.2 must trace to a project objective (Section 3.2), a requirement (Section 5), a deliverable (Section 9), and a work package (Section 10). Populate the Scope Traceability Matrix (Section 10.3) to verify this.
8. **Be specific, not vague** — write "Reduce order processing time from 45 seconds to under 5 seconds (p99)" not "Improve performance."
9. **Include measurable acceptance criteria** wherever possible — use numbers, percentages, and thresholds.
10. **Cross-reference preceding documents** — when content derives from the viability study or business case, reference them (e.g., "As identified in the Business Case Section 7.1, the primary tangible benefit is...").
11. **Do not repeat analysis from preceding documents** — reference and summarize rather than duplicating. The scope document translates recommendations into delivery boundaries.
12. **Save the generated document** to an appropriate location, suggested: `docs/project-scope.md` or alongside the business case.

#### Quality Checks Before Delivery

After generating the document, perform these self-checks:

- [ ] Every section is either populated with project-specific content or marked [NOT APPLICABLE] with rationale.
- [ ] No `<!-- -->` placeholders remain (except the document status and date fields that require human input).
- [ ] The Scope Traceability Matrix (Section 10.3) is complete — every scope item traces to requirement(s), deliverable(s), and work package(s).
- [ ] No contradictions exist between this scope document and the business case or viability study (if they exist, flag them explicitly).
- [ ] All MoSCoW priorities are assigned to scope items (Section 4.2) and requirements (Section 5.1).
- [ ] Scope exclusions (Section 12) are explicit and include rationale — not just "not included" but why.
- [ ] The Definition of Done (Section 11.2) is concrete and measurable.
- [ ] The scope change control process (Section 14) defines clear authority levels.
- [ ] The document is internally consistent — scope items, phases, deliverables, and WBS all align.
- [ ] The Executive Summary accurately reflects the full document content.

### Phase 4: Post-Generation Review

After the document is generated:

1. **Present the document** to the user.
2. **Highlight key decisions made** during generation — where the skill made judgment calls based on available information, point them out so the user can verify.
3. **Flag remaining uncertainties** — any areas where information was insufficient and reasonable assumptions were made.
4. **Offer to refine** any section the user wants to adjust.
5. **Suggest next steps** — e.g., stakeholder review, baselining, backlog creation from the WBS.

## Examples

### Example Question (Gap — No Business Case Exists)

**[Critical] Section 3.1 — Business Context**

No business case or viability study was found for this project. The business context is essential for defining scope boundaries and priorities — without it, scope may not align with strategic objectives.

What is the primary business problem or opportunity this project addresses, and what strategic objective does it support?

Suggested answers:
- *Option A*: "Reduce operational costs by automating the manual invoice processing workflow, supporting the strategic objective of 20% OpEx reduction by FY2027."
- *Option B*: "Enable a new revenue stream by launching a self-service customer portal, supporting the strategic objective of digital channel expansion."
- *Option C*: "Eliminate compliance risk by replacing the end-of-life legacy billing system, supporting the strategic objective of regulatory compliance."
- *Custom*: [your own answer]

### Example Question (Contradiction — Feature Parity Disagreement)

**[Important] Section 4.4 — Feature Parity Scope**

The viability study recommends "100% feature parity at cutover" (Section 5.4), but the business case's cost estimate implies a phased approach where only 80% of features are migrated in Phase 1. These two positions contradict each other — the scope document must resolve this.

What is the feature parity expectation at the initial go-live?

Suggested answers:
- *Option A*: "100% feature parity at go-live — all existing features must be available before users switch. This increases Phase 1 scope and timeline but eliminates dual-running complexity."
- *Option B*: "80% feature parity at go-live — critical features migrate first, remaining 20% delivered in Phase 2 with dual-running for those features. This reduces Phase 1 scope but introduces dual-running cost and complexity."
- *Option C*: "Feature parity is not the right measure — the modernized system reimagines several workflows. Parity is measured by user capability, not feature-by-feature replication. Define a capability parity matrix instead."
- *Custom*: [your own answer]

### Example Question (Partial Information — Unclear Scope Boundaries)

**[Important] Section 7.1 — System Boundary Definition**

The business case mentions integration with the CRM system but does not specify whether CRM modifications are within this project's scope or the responsibility of the CRM team. This affects the scope of integration work and delivery dependencies.

Is the CRM integration within this project's scope (build and modify both sides), or is it an external dependency (CRM team adapts their side)?

Suggested answers:
- *Option A*: "CRM integration is in scope — this project owns both the new system's API and the CRM adaptation work. This increases scope but gives us full control over the integration timeline."
- *Option B*: "CRM integration is split — this project builds the new system's API; the CRM team is responsible for consuming it. The CRM work is a dependency tracked in Section 13.3, not a scope item."
- *Option C*: "CRM integration is out of scope for this phase — the new system will expose APIs, but CRM consumption is deferred to a separate project. A manual workaround bridges the gap temporarily."
- *Custom*: [your own answer]

## Anti-Patterns to Avoid

- **Don't generate the document without asking questions** — the skill's value is in the analysis and clarification, not just template filling.
- **Don't ask questions that the existing documentation already answers** — read carefully first.
- **Don't ask too many questions at once** — batch by priority, lead with critical questions, offer to proceed with assumptions for lower-priority items.
- **Don't produce vague scope items** — "Improve the system" is not a scope item; "Add real-time order status tracking with push notifications for 5 order states" is.
- **Don't skip the traceability matrix** — it is the primary quality mechanism for the scope document.
- **Don't duplicate content from the viability study or business case** — reference and summarize.
- **Don't mark sections [NOT APPLICABLE] just because they're hard** — only mark them if they genuinely don't apply to the project type.