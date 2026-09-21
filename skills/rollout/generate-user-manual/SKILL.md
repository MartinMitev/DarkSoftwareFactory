---
name: generate-user-manual
description: Generates a comprehensive, evidence-based User Manual for a software application using the repository template `templates/rollout/user-manual.md`. This skill should be used when end-user documentation is needed for a release, onboarding, or support reference. It deeply analyzes existing project documentation (`documentation/`) and the codebase to extract actual user-visible behavior (features, UI areas, workflows, roles, settings, error messages, shortcuts, accessibility), asks targeted open questions with suggested valid answers whenever it detects gaps, unclear statements, or contradictions, and populates every applicable template section.
---

# Skill: Generate User Manual

## Description

Generates a complete User Manual based on the template `templates/rollout/user-manual.md`. The skill deeply analyzes all available project information — existing documentation in `documentation/` (business case, project scope, SRS, user stories, UI/UX design, architecture, test concept) and the codebase itself — to describe the application **as it is actually built**: its features, user interface, procedures, roles, settings, error messages, and support paths.

The evidence hierarchy for describing shipped behavior is:

1. **Implemented code behavior** — what the application actually does (highest authority for "how it works").
2. **Baselined project documents** — what the system is intended to do and why (authority for purpose, outcomes, terminology, scope).
3. **User answers** — clarifications obtained through questions (authority for gaps and judgment calls).

When documents and code disagree (e.g., a documented feature that is not implemented, or an implemented capability that no document mentions), that is a **contradiction** — it must become a question, never a silent choice.

When gaps, unclear statements, or contradictions are detected, the skill asks targeted open questions with suggested valid answers before generating. The User Manual is written from the **user's point of view**: what users can do, how to do it, and what to do when something fails — never internal architecture.

## Activation

When the user requests to create, generate, or draft a user manual, user guide, end-user documentation, how-to documentation, or application support documentation.

**Loading constraints:** This skill needs a live, responsive user for Phase 2 (clarification questions). Do not run it in non-interactive contexts (CI pipelines, scheduled runs, autonomous loops). If invoked there and blocking questions exist, produce a draft with explicitly flagged assumptions instead of guessing, and surface the questions for the user to answer later.

## Instructions

### Phase 1: Information Gathering & Deep Analysis

1. **Read the template** at `templates/rollout/user-manual.md` to understand the full structure: the 13 numbered sections, their subsections, the "Expected content" guidance comments, the repeatable blocks (feature sub-sections in Section 4, admin tasks in Section 7, scenarios in Section 8, platforms in Section 2.2), and the `[OPTIONAL]` sections (7 Administration Guide, 10 Keyboard Shortcuts and Accessibility).

2. **Discover and read all existing project documentation:**
   - Start with `documentation/` (or the project's established docs folder) — read every `.md` file found there.
   - Search the workspace by name pattern for the canonical Dark Software Factory artifacts: business case, project scope, software requirements specification (SRS), user stories, UI/UX design document, software architecture, test concept, project risk profile, project plan.
   - Search for supporting material: README files, architecture decision records (ADRs), changelogs/release notes, existing user-facing documentation, knowledge base articles, training material.
   - Search for API specifications (OpenAPI/Swagger/GraphQL schemas) — they document commands, parameters, and error responses users may encounter.
   - Search for localization/i18n resource files — they contain the exact user-visible labels, messages, and terminology.
   - If preceding documents classify the project type (Green Field / Brown Field / Modernization), adopt it; for Brown Field 🟤 and Modernization 🔵 projects, pay special attention to existing-system behavior that must be described (upgraded workflows, migrated features, changed UI).

3. **Analyze the codebase for user-visible behavior.** This is the step that separates an evidence-based manual from a paraphrased requirements document. Extract, for each area, the actual shipped behavior:

   | Code Artifact | What to Extract | Feeds Template Section |
   |---------------|-----------------|------------------------|
   | Routes, pages, screens, navigation definitions | Screen inventory, navigation paths, main UI areas, global elements | 3.1–3.3 |
   | Feature controllers, handlers, use-case modules, feature flags | Core feature inventory and actual capability behavior | 4.1–4.x |
   | Authentication guards, RBAC/permission checks, role enums | Role definitions and real permission outcomes | 6.1–6.2 |
   | User-facing settings, preferences, notification config | Advanced settings areas, reversibility | 5.x |
   | Admin routes, admin controllers, admin-only operations | Administration task inventory | 7.x |
   | Error/validation message strings, i18n catalogs | Exact error texts users can encounter | 9.2 |
   | Keybinding definitions, shortcut configs | Keyboard shortcuts per context | 10 |
   | ARIA attributes, accessibility config, contrast themes | Accessibility features and known limitations | 10 |
   | State machines, workflow/process definitions | End-to-end workflows and their steps | 8.x |
   | Domain models, entity names, enum values | Glossary terms and abbreviations | 11 |
   | `package.json`, app manifests, installer/CI configuration | Version, supported platforms, distribution channels, update mechanism | 1.2, 2.1, 2.2 |
   | Onboarding/first-run flows, wizards, setup scripts | First login and activation procedure | 2.3, 2.4 |

   Analysis rules:
   - **Trace real procedures**: follow an actual route/flow from start state to end state before writing steps for it. Do not write steps from imagination.
   - **Capture exact strings**: UI element names, button labels, and error messages come from code/i18n files — not from documentation paraphrases.
   - **Note the absence of evidence**: if a template section requires information no code or document contains (support channels, SLAs, screenshot sources, licensing), record it as a Gap.

4. **Map existing information to template sections.** For each of the 13 sections, classify readiness:
   - **Covered**: Sufficient evidence exists to write accurate, user-level content.
   - **Partially Covered**: Information exists but is incomplete or too vague for step-level procedures (e.g., a feature name without its workflow, a role without its permissions).
   - **Gap**: No information exists.
   - **Contradiction**: Sources conflict (e.g., SRS describes a workflow the code implements differently; scope lists a feature the code does not contain; code contains a capability no document mentions).

5. **Build a section readiness map** — tag each section 🟢 Ready, 🟡 Partially Ready, 🔴 Not Ready. Sections with 🔴/🟡 readiness, and every Contradiction, are priority candidates for Phase 2 questions.

### Phase 2: Clarification Questions

Before generating the document, ask the user targeted questions for every **Partially Covered**, **Gap**, **Contradiction**, or **Not Ready** area identified in Phase 1.

#### Question Design Principles

- **Ask open questions** that invite thoughtful responses — not yes/no questions.
- **Always suggest 2–3 possible valid answers** for each question to help the user think through the options and to demonstrate understanding of the application.
- **Contextualize each question** — briefly explain why it matters for the manual and what happens if it remains unanswered (e.g., "Without the role definitions, the permission matrix in Section 6.2 cannot be written, and every procedure would have to hedge with 'if you have permission'.")
- **Group questions by template section** so the user can address them systematically.
- **Prioritize questions**:
  - **[Critical]**: Blocks generation of the section — the manual would be wrong or unusable without the answer (e.g., version/platform coverage, planned-vs-shipped conflicts).
  - **[Important]**: Affects quality and completeness — content can be drafted but will carry gaps or assumptions (e.g., support SLAs, screenshot provisioning).
  - **[Optional]**: Refinement only — can proceed with a stated assumption and a validation action.
- **Reference the source** of the gap or contradiction (document name/section, or code file/route).
- **Surface implicit behavior** — when the code implies a user capability that no document describes, propose it and ask whether to document it, exclude it (internal/undocumented feature), or flag it for a product decision.
- **Challenge stale documentation** — when a document describes behavior that contradicts the code, state both readings explicitly and ask which is authoritative.
- **Do not ask questions that can be answered by reading existing documentation or code** — if the answer exists in a file already read, use it directly.
- **Distinguish what must be resolved now from what can be recorded as an assumption with a validation plan** — for [Optional] questions, offer to proceed with the assumption.

#### Question Template

For each question, use this format:

---

**[Priority] Section X.Y — [Topic]**

[Context: Why this matters for the manual and what stays undefined if unanswered. Cite the source document or code location of the gap/contradiction.]

[The open question]

Suggested answers:
- *Option A*: [description and implications for the manual]
- *Option B*: [description and implications for the manual]
- *Option C*: [description and implications for the manual]
- *Custom*: [your own answer]

---

#### Minimum Required Questions for Any User Manual

Resolve these before generating unless they are fully answerable from existing evidence:

- Who are the primary audiences/roles of the manual, and what experience level should the writing assume (novice, general business user, expert)?
- Which application version(s) and platforms does the manual cover — and does the current codebase represent that version?
- What are the top user tasks ranked by frequency/importance (drives feature ordering in Section 4)?
- How is the application accessed or installed per platform (URL, app store, installer, CLI)?
- Should administration features be documented in this manual (Section 7 applies) or excluded to a separate admin guide?
- What support channels, response expectations, and escalation paths exist?
- Who provides screenshots, in what format, and when — or should the manual ship with formatted placeholders?
- How should planned-but-unimplemented features be treated — excluded, or documented as roadmap?
- Is the manual customer-facing or internal (affects tone, Classification in Metadata, and legal notices in 13.3)?

### Phase 3: Document Generation

Once all critical and important questions are resolved, generate the User Manual.

#### Generation Rules

1. **Use the template structure exactly** — follow `templates/rollout/user-manual.md` section by section, including all subsections and the "Expected content" guidance in each section.
2. **Replace all `<!-- -->` placeholders** with project-specific content derived from the analysis and user answers. No placeholder may remain except fields intended for human input (Document Status, dates, sign-off).
3. **Stay evidence-based**: for key statements, note the source (document name/section or code file/route). Where an assumption had to be made, mark it inline and list it in the review (Phase 4).
4. **Write from the user's point of view**: task-oriented, benefits-first, plain language. Describe WHAT users can do and HOW — not how the system is built. Never expose architecture internals, stack names, or implementation details unless users need them to operate the application (e.g., browser requirements).
5. **Write procedures users can execute**: numbered steps, one action per step, exact UI element names verified against code/i18n strings, alternate paths (shortcut, context menu, drag) where they exist, and the expected result after each non-obvious step.
6. **Handle the `[OPTIONAL]` sections explicitly** (7 Administration Guide, 10 Keyboard Shortcuts and Accessibility): apply them with content, or remove them entirely — removal requires updating the Table of Contents and noting the rationale in the revision history. Never leave them present-but-empty.
7. **Use the repeatable blocks consistently**: one feature sub-section per Section 4.1 Feature Index row (4.2, 4.3, ...), ordered by importance/frequency of use; one sub-section per platform in 2.2; per admin task in 7.x; per scenario in 8.x.
8. **Populate the permission matrix from actual code checks** — allowed/not allowed/partial must reflect what the application enforces, not what documents claim; footnote any partial permissions.
9. **Populate the error message reference from actual message strings** — exact text/code, plain-language meaning, user action, transient vs. persistent. If resolutions are unknown, say what to collect when escalating (cross-reference Section 12).
10. **Leave formatted screenshot placeholders** if screenshots were not provided (e.g., `Screenshot: <window name>, <annotated state>`), per the template's Document Conventions.
11. **Keep the Feature Index (4.1) and feature sub-sections consistent** — every indexed feature has a sub-section; every sub-section is indexed.
12. **Make the reading guide by role (6.3) concrete** — required reading, role-relevant sections, and skippable sections per role, so the manual doubles as an onboarding path.
13. **Write Section 1 (Introduction) last** — after all other sections are complete, synthesize purpose, audience, conventions, and related documentation.
14. **Initialize the revision history (13.2)** with the generation date and a summary of what was produced and from which sources.
15. **Save the generated document** to an appropriate location, default: `documentation/user-manual.md`.

#### Quality Checks Before Delivery

After generating the document, perform these self-checks:

- [ ] Every section is populated with project-specific content, or (for `[OPTIONAL]` sections) explicitly applied or removed with rationale.
- [ ] No `<!-- -->` placeholders remain (except Document Status, dates, and sign-off fields).
- [ ] The Table of Contents is valid: all anchors resolve, and it matches the final section set (updated if any `[OPTIONAL]` section was removed).
- [ ] The Feature Index (4.1) matches the feature sub-sections 1:1.
- [ ] Every procedure's UI element names, commands, and error texts match code/i18n evidence.
- [ ] The permission matrix (6.2) is consistent with the role definitions (6.1) and with code-enforced checks.
- [ ] Terminology is consistent with the Glossary (11) and the Document Conventions (1.3).
- [ ] All cross-references between sections are valid (e.g., troubleshooting entries point to existing sections).
- [ ] Every user-visible error message found in code appears in the Error Message Reference (9.2) — or the gap is flagged.
- [ ] Metadata is complete: application name, version covered, platforms, audience roles, classification.
- [ ] The revision history (13.2) is initialized and consistent with the Metadata Baseline Version.
- [ ] No contradictions remain unflagged: doc-vs-code conflicts resolved by user answers or marked as assumptions.

### Phase 4: Post-Generation Review

After the document is generated:

1. **Present the document** to the user.
2. **Highlight key judgments made** during generation — interpretive calls such as task ordering, feature-to-section mapping, procedure phrasing, or `[OPTIONAL]` section decisions — so the user can verify them.
3. **List the assumptions** with their risk: what content rests on assumptions rather than evidence, what could be wrong, and how to validate each assumption (e.g., run through the procedure, check the role matrix in a test tenant).
4. **Flag undocumented features discovered in code** — capabilities implemented but absent from all documentation. These are the most likely to need a product decision (document, hide, or remove).
5. **Summarize the evidence coverage**: which sections were generated purely from code, which from documents, which from user answers, and which carry placeholders (screenshots).
6. **Offer to refine** any section the user wants adjusted.
7. **Suggest next steps**:
   - Verify the manual with documentation test cases (`templates/testing/documentation-test-cases.md`).
   - Capture and insert the screenshots (replace placeholders, keep the annotation convention).
   - Coordinate release timing with `shipping-and-launch` so the manual ships with the version it describes.
   - Establish the update workflow: the manual must be revised every release (revision history, Section 13.2).

## Examples

### Example Question (Contradiction — Documented but Unimplemented Feature)

---

**[Critical] Section 4.2 — [Feature Name]: Planned vs. Shipped**

The SRS (Section 4.2.5) specifies a "Bulk Import" capability as a Must Have, and the project scope lists it as a scope item — but no import UI, route, or handler exists in the codebase, and no feature flag references it. The User Manual must describe the application as it is; documenting an unimplemented feature would mislead users. Conversely, excluding it silently would lose track of a promised capability.

How should Bulk Import be treated in this manual?

Suggested answers:
- *Option A*: "Exclude it — Bulk Import is not part of this release. The manual covers the current version only; import capability will be added in the manual when it ships. Record this in Known Issues (13.1) as 'planned for vX.Y, not yet available' so support has a reference answer."
- *Option B*: "Document it as roadmap — add a short note in the import/export area of Section 5 stating Bulk Import is coming in an upcoming release, without procedures. This manages user expectations but risks readers assuming it already works."
- *Option C*: "Document it fully with procedures — the feature is implemented on a branch about to merge; the manual should target the release, not the current trunk. I will confirm the merge and version number before you write the procedures."
- *Custom*: [your own answer]

---

### Example Question (Gap — Undocumented Implemented Capability)

---

**[Important] Section 4 — Undocumented Feature: [Capability Name]**

While analyzing the codebase, the skill found a fully implemented capability that no project document mentions: [describe, e.g., a data export endpoint exposed in the UI, a hidden keyboard shortcut, a workspace-sharing flow]. It is user-visible (reachable from [route/menu]) but absent from the SRS, user stories, and UI/UX design document. Writing it into the manual makes the manual more complete but may expose functionality that is not yet supported or approved for customers.

Should this capability be documented, and if so, at what level?

Suggested answers:
- *Option A*: "Document it fully as a core feature — it is stable, tested, and intended for users. Add it to the Feature Index (4.1) with its own how-to sub-section, including the procedure traced from the code."
- *Option B*: "Document it minimally — mention it in the feature overview as an advanced capability without step-level procedures, marked as experimental/beta. Full documentation follows once it is officially released."
- *Option C*: "Do not document it — it is internal/undocumented functionality (e.g., a power-user escape hatch or a feature still behind a flag). Note it in Known Issues (13.1) as 'undocumented capability' so the product owner can decide later."
- *Custom*: [your own answer]

---

### Example Question (Contradiction — Terminology Mismatch)

---

**[Important] Sections 6.1, 9.2 — Terminology: Role and Message Names**

The SRS and user stories consistently use the role names "Editor" and "Reviewer", but the code enforces roles named `contributor` and `approver` (auth guard definitions), and the UI permission dialog displays "Contributor" and "Approver". The manual must use the names users actually see in the interface; otherwise procedures will reference buttons and labels that do not exist for them. The same mismatch affects two error messages whose code wording differs from the docs.

Which terminology is authoritative for the manual?

Suggested answers:
- *Option A*: "The code/UI wording is authoritative — the manual uses 'Contributor' and 'Approver' everywhere, and the Glossary (11) maps them to the older document terms. The SRS and user stories should be updated in a follow-up."
- *Option B*: "The document wording is authoritative — the UI is about to be re-labeled to 'Editor'/'Reviewer' before release; the manual targets the released UI. I will confirm the re-labeling ships with this version."
- *Option C*: "Both are shown — the manual uses the UI labels in procedures, and the Glossary lists both names with a note about the upcoming rename, so readers of older material are not confused."
- *Custom*: [your own answer]

---

## Anti-Patterns to Avoid

- **Don't document aspirational behavior** — the manual describes the application as built. A documented-but-unimplemented feature must become a question, not a section.
- **Don't invent UI element names, commands, or error texts** — every label, shortcut, and message must be verified against code or i18n strings.
- **Don't write procedures from imagination** — trace the actual route/flow first; if the flow cannot be traced, mark the procedure as unverified.
- **Don't dump architecture into the manual** — components, databases, and frameworks belong to the architecture document; users need outcomes and actions.
- **Don't generate without questions** — gaps and contradictions must surface; a confidently wrong manual is worse than an explicit open question.
- **Don't ask what the sources already answer** — read documentation and code carefully first.
- **Don't leave `[OPTIONAL]` sections present-but-empty** — apply them with content or remove them and fix the Table of Contents.
- **Don't copy requirements language verbatim** — "The system shall..." is SRS language; the manual says "You can..." and "To do X, ...".
- **Don't forget the Feature Index consistency** — index rows and feature sub-sections must match 1:1, and ordering should reflect importance, not the order features were discovered in code.

## Document Hierarchy Context

The User Manual is a **rollout-phase artifact**: it is generated when the application is ready for users and maintained for every release. It builds upon:

| Document | Relationship |
|----------|--------------|
| **Software Requirements Specification** | Source of intended behavior, feature inventory, business rules, and role definitions — verified against shipped code |
| **User Stories** | Source of user goals, task flows, and acceptance criteria — raw material for procedures and scenarios |
| **UI/UX Design Document** | Source of information architecture, screen layouts, design system, accessibility targets — basis for the UI Overview |
| **Software Architecture** | Context for deployment model, platforms, integrations, and environment requirements |
| **Test Concept / Test Cases** | Evidence of validated behavior; the basis for describing reliable procedures |

And it feeds forward:

| Artifact | Relationship |
|----------|--------------|
| **Documentation test cases** | Verify the manual: procedures, accuracy, completeness |
| **Support/knowledge base** | The troubleshooting and error reference sections feed support tooling |
| **Release process** | The manual is versioned and revised with every release (13.2 Revision History) |

## Resources

### Template

The canonical template lives at `templates/rollout/user-manual.md` and is referenced directly — do not copy it into this skill, so the skill and template cannot drift apart. If the template evolves, update this skill's section references to match.

### scripts/

Optional: no scripts are required for this skill.

### references/

Optional: store organization-specific material such as support-portal policies, SLA tables, screenshot storage conventions, or terminology glossaries to reuse across projects.
