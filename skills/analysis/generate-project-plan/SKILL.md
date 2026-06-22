---
name: generate-project-plan
description: Generates a Software Project Plan. The skill deeply analyzes all available project information — existing documentation, codebase, stakeholder inputs, and any organizational standards — to populate a detailed, executable project framework. The project plan is the **authoritative execution document** — it defines HOW the project will be executed, monitored, and controlled, translating the "what and why" from preceding documents into "how, when, by whom, with what resources, under what governance."
---
# Skill: Generate Project Plan

## Description

Generates a complete, rigorous Software Project Plan based on the template `templates/analysis/project-plan.md`. The skill deeply analyzes all available project information — preceding analysis documents (viability study, business case, project scope, SRS), existing documentation, codebase, stakeholder inputs, and any organizational standards — to populate every applicable section of the template with a detailed, executable project framework. When gaps, ambiguities, or contradictions are detected in the source material, the skill asks targeted open questions with suggested plausible, context-aware answers before proceeding. The project plan is the **authoritative execution document** — it defines HOW the project will be executed, monitored, and controlled, translating the "what and why" from preceding documents into "how, when, by whom, with what resources, under what governance."

## Activation

When the user requests to create, generate, or draft a project plan, project execution plan, delivery plan, or implementation plan for a software project.

## Instructions

### Phase 1: Information Gathering & Deep Analysis

1. **Read the template** at `templates/analysis/project-plan.md` to understand the full structure, all 20 sections, their expected content, and project-type applicability (🟢 🟤 🔵 ⚪). Pay special attention to:
   - The Executive Summary (Section 1) — must be written last and stand alone as a readable overview.
   - The project type classification (Section 2.2) — determines which sections apply and how they are framed.
   - The delivery methodology (Section 2.3) — the methodology must be consistent with the project type, organizational maturity, and preceding document recommendations.
   - The schedule and timeline (Section 7) — must be consistent with scope, resources, and budget.
   - The budget and cost management (Section 8) — must align with the business case's investment case.
   - The risk register (Section 10) — must reflect risks from preceding documents AND execution-specific risks.
   - The transition and migration plan (Section 17) — critical for 🟤🔵 projects, [NOT APPLICABLE] for 🟢.

2. **Discover and read all existing project information:**
   - Search the workspace for any viability study documents (check `documentation`, `docs`, project folders, or any `.md` files with "viability" in the name). If found, read it thoroughly — the project plan must be consistent with the viability study's feasibility assessment and project type classification.
   - Search for any business case documents (check `documentation`, `docs`, project folders, or any `.md` files with "business-case" or "business_case" in the name). If found, read it thoroughly — the project plan's budget, timeline, and resource assumptions must align with the business case's approved investment option.
   - Search for any project scope documents (check `documentation`, `docs`, project folders, or any `.md` files with "project-scope" or "project_scope" in the name). If found, read it thoroughly — the project plan's scope summary, deliverables, and priorities must reference and align with the scope document.
   - Search for any SRS documents (check `documentation`, `docs`, project folders, or any `.md` files with "requirements" or "srs" in the name). If found, read it — the project plan's quality strategy and testing approach derive from the SRS's requirement specifications.
   - Search for any user story documents (check `documentation`, `docs`, project folders, or any `.md` files with "user-stories" or "user_stories" in the name). If found, read it — the project plan's sprint cadence and release plan must be consistent with the story estimates and priorities.
   - Search for any existing project plans, delivery plans, or implementation plans.
   - Search for any architecture decision records (ADRs), README files, or technical documentation — these inform the technical approach and environment requirements.
   - Search for any configuration files (`package.json`, `pom.xml`, `build.gradle`, `docker-compose.yml`, etc.) that reveal the technology stack, system boundaries, and infrastructure needs.
   - If a codebase exists, explore the directory structure to understand current modules, services, and integrations — this informs the technical environment and existing system considerations for 🟤🔵.
   - Search for any stakeholder communication, meeting notes, decision logs, or executive summaries — these inform governance, communication, and stakeholder management.
   - Search for any financial data — budget documents, cost reports, vendor pricing, cloud cost estimates, staffing rate cards.
   - Search for any organizational standards — project management methodology, governance frameworks, quality standards, security policies.
   - Search for any compliance, regulatory, or audit documentation — these inform compliance requirements and procurement constraints.
   - Search for any vendor contracts, procurement documents, or SaaS agreements — these inform vendor management and procurement sections.
   - Search for any existing team information — org charts, team rosters, skills inventories, availability calendars.

3. **Classify the project type** based on available evidence:
   - **Green Field (🟢)**: Building new software from scratch — project plan focus: establishing delivery processes from scratch, defining the complete technology stack, building the team for net-new development, defining the full release strategy, no migration or backward-compatibility concerns. Sections 17 is [NOT APPLICABLE].
   - **Brown Field (🟤)**: Extending or enhancing an existing system — project plan focus: coordinating with existing system operations, managing backward compatibility, regression risk planning, impact on existing users and workflows, integration with existing CI/CD and release trains.
   - **Software Modernization (🔵)**: Migrating or re-architecting a legacy system — project plan focus: migration planning, dual-running coordination, feature parity verification, legacy decommission scheduling, data migration timelines, rollback planning, transition governance.
   - If a preceding document (viability study, business case, or project scope) already classified the project type, adopt that classification unless new evidence contradicts it — note any contradiction as a question for Phase 2.
   - If classification is ambiguous, note this as a [Critical] question — the classification determines which sections apply and how the plan is structured.

4. **Map existing information to template sections.** For each of the 20 sections and their subsections, determine:
   - **Covered**: Sufficient information exists to populate the section with evidence-based, execution-ready content.
   - **Partially Covered**: Some information exists but is incomplete, lacks execution detail, or needs validation.
   - **Gap**: No information exists for this section.
   - **Contradiction**: Information from different sources conflicts (e.g., business case says 12 months, scope document implies 18 months).

5. **Perform deep execution-readiness analysis.** The project plan is an execution document — it must be specific, actionable, and internally consistent. Go beyond surface-level mapping:

   **Preceding document alignment checks:**
   - Does the business case's approved budget match the project plan's budget overview (Section 8)? If the business case says €500K and the plan's budget breakdown sums to €380K, there is a gap.
   - Does the business case's timeline align with the project plan's schedule (Section 7)? If the business case projects 12-month delivery but the plan's phase timeline sums to 16 months, there is a contradiction.
   - Does the project scope's MoSCoW priorities align with the plan's scope prioritization (Section 4.3) and release plan (Section 7.3)? Must Have scope must map to Release 1.
   - Does the project scope's deliverable list align with the plan's major deliverables (Section 4.2)?
   - Does the viability study's risk assessment align with the plan's risk register (Section 10)? Viability risks should appear in the plan's risk register with execution-level detail added.
   - If a SRS exists, do its non-functional requirements inform the plan's quality criteria (Section 9.5) and testing strategy (Section 9.2)?
   - If user stories exist, do their estimates inform the plan's sprint cadence and velocity assumptions (Section 7.4)?

   **Internal consistency checks:**
   - Does the team composition (Section 12.1) match the resource assumptions in the schedule (Section 7.4) and budget (Section 8.2)?
   - Does the sprint cadence (Section 7.4) produce enough capacity to deliver the scope within the timeline (Section 7.1)?
   - Does the budget by phase (Section 8.2) align with the delivery phases (Section 7.1)?
   - Does the risk budget allocation (Section 10.3) align with the contingency reserve in the budget (Section 8.1)?
   - Are the governance meetings (Section 5.1) consistent with the communication plan (Section 11.1) and reporting schedule (Section 11.2)?
   - Are the RACI assignments (Section 6.2) consistent with the decision framework (Section 5.2) and the core team roles (Section 6.1)?
   - Does the deployment approach (Section 18.1) support the release plan (Section 7.3) and schedule (Section 7.1)?
   - For 🟤🔵: Does the transition strategy (Section 17.1) align with the delivery phases (Section 7.1) and the legacy decommission plan (Section 17.4)?

   **Execution feasibility checks:**
   - Is the velocity assumption (Section 7.4) realistic given the team composition (Section 12.1) and skill development plan (Section 12.3)?
   - Is the schedule feasible given the resource calendar (Section 12.2) and known time-off / holiday reductions?
   - Is the budget realistic given the staffing rates, infrastructure costs, and vendor pricing?
   - Are the stage-gate criteria (Section 5.3) achievable and measurable?
   - Are the quality targets (Section 9.4) realistic given the testing strategy (Section 9.2) and team skills?
   - Is the communication plan (Section 11.1) realistic given the stakeholder landscape (Section 16.1)?
   - Are the risk mitigation actions (Section 10.2) feasible within the budget and timeline?

   **Project-type-specific checks:**
   - 🟢 Green Field: Is Sprint 0 / Inception (Section 7.1) adequately planned for team setup, tooling, and environment provisioning? Is the release strategy (Section 18) appropriate for a new product? Is the team composition (Section 12.1) sufficient for net-new development?
   - 🟤 Brown Field: Is the plan coordinating with existing system operations (Section 5.1)? Are regression risks (Section 10.2) adequately addressed? Is the deployment approach (Section 18.1) compatible with existing release trains?
   - 🔵 Modernization: Is the transition plan (Section 17) comprehensive? Is dual-running (Section 17.3) costed and scheduled? Is the cutover runbook (Section 17.5) detailed enough? Is the legacy decommission plan (Section 17.4) tied to measurable prerequisites?

6. **Build an execution readiness map** — for each section, tag readiness:
   - 🟢 **Execution-Ready**: Information is detailed, specific, and sufficient to write an actionable, internally consistent plan section.
   - 🟡 **Partially Ready**: Information exists but needs validation, execution-level detail, or consistency verification.
   - 🔴 **Not Ready**: Missing, unquantified, or based on unsupported assertions — cannot derive an execution plan without clarification.

   Sections with 🔴 readiness are priority candidates for Phase 2 questions.

### Phase 2: Clarification Questions

Before generating the document, ask the user targeted questions for every **Partially Covered**, **Gap**, **Contradiction**, or **Not Ready** area identified in Phase 1.

#### Question Design Principles

- **Ask open questions** that invite thoughtful responses — not yes/no questions.
- **Always suggest 2–3 plausible, context-aware answers** for each question to help the user think through the options and to demonstrate understanding of the domain. Each suggested answer should include its implications for the project plan.
- **Contextualize each question** — briefly explain why the information matters for project execution and what happens if it remains unanswered (e.g., "Without this, the project plan cannot define the sprint cadence or estimate the number of sprints required, which means the schedule and budget are unanchored").
- **Group questions by template section** so the user can address them systematically.
- **Prioritize questions** — mark questions as:
  - **[Critical]**: Blocks the execution plan — the project plan cannot define how the project will be executed without this. Examples: project type, delivery methodology, team composition, budget, timeline.
  - **[Important]**: Affects the quality and credibility of the execution plan. Examples: governance structure, quality targets, risk mitigation, communication approach.
  - **[Optional]**: Refines the plan but does not block generation. Can be documented as an assumption with a validation plan. Examples: specific tooling choices, detailed resource calendar, procurement timeline.
- **Reference the source** of the contradiction or gap (e.g., "The business case estimates a 12-month delivery timeline, but the scope document's deliverable list implies at least 18 months of work at the assumed velocity").
- **Challenge execution optimism** — if the timeline seems too aggressive for the scope, if the budget seems too low for the team size, or if the velocity assumptions seem inflated for a new team, flag this explicitly and ask for substantiation.
- **Do not ask questions that can be answered by reading existing documentation** — if the answer exists in a file the skill has already read, use that information directly.
- **Distinguish between information that must be resolved now vs. information that can be documented as assumptions with validation plans.** For [Optional] questions, offer to proceed with a stated assumption.

#### Question Template

For each question, use this format:

---

**[Priority] Section X.Y — [Topic]**

[Context: Why this matters for project execution and what happens if unanswered]

[The open question]

Suggested answers:
- *Option A*: [description and implications for the project plan]
- *Option B*: [description and implications for the project plan]
- *Option C*: [description and implications for the project plan]
- *Custom*: [your own answer]

---

#### Minimum Required Questions by Project Type

**All project types** must resolve these before the project plan can be generated:

- What is the project name and project type classification (Green Field, Brown Field, Software Modernization)?
- What delivery methodology will be used (e.g., Scrum, SAFe, Kanban, Hybrid), and why was it selected?
- What is the total approved budget, and how is it split between CapEx and OpEx?
- What is the target delivery timeline (start date, key milestone dates, end date)?
- Who is the project sponsor, product owner, and project manager?
- What is the team composition — how many people, which roles, internal vs. external?
- What are the top 3–5 risks that could derail the project?
- What are the critical dependencies on other projects, teams, or vendors?
- What is the sprint/iteration length and assumed velocity?
- What is the deployment and release strategy?

**Green Field (🟢) additional questions:**
- What is the Sprint 0 / Inception plan — how will the team, tooling, and environments be set up before feature delivery begins?
- What is the MVP definition and how does it map to the first release?
- What is the complete technology stack and who makes architecture decisions?
- What is the release strategy for a new product — how will early releases be validated with users?
- What is the team ramp-up plan — how will a new team reach productive velocity?

**Brown Field (🟤) additional questions:**
- How will the project coordinate with existing system operations and production support?
- What is the regression risk mitigation strategy — how will existing functionality be protected?
- How does the project integrate with existing CI/CD pipelines and release trains?
- What backward compatibility constraints exist, and how do they affect the delivery timeline?
- What is the impact on existing users who are not the target of the enhancements?

**Software Modernization (🔵) additional questions:**
- What is the migration approach — big bang, phased, parallel run, or strangler fig?
- What is the feature parity target at cutover — 100% parity, or is partial parity acceptable?
- What is the dual-running period and its cost impact?
- What is the data migration scope, approach, and timeline?
- What is the rollback strategy if the migration fails, and what is the maximum rollback window?
- What is the legacy decommission timeline and what prerequisites must be met before decommission can begin?
- What is the cutover decision authority — who decides to proceed with the switchover, and who decides to rollback?

### Phase 3: Document Generation

Once all critical and important questions are resolved, generate the project plan document.

#### Generation Rules

1. **Use the template structure exactly** — follow `templates/analysis/project-plan.md` section by section, including all 20 sections and their subsections.
2. **Replace all `<!-- -->` placeholders** with project-specific content derived from the analysis and user answers.
3. **Mark sections as [APPLICABLE] or [NOT APPLICABLE]** based on the project type classification. For [NOT APPLICABLE] sections, include a one-line rationale (e.g., "[NOT APPLICABLE] — Green Field project with no existing system to migrate").
4. **For 🟤🔵 sections**, populate them if the project type matches; otherwise mark [NOT APPLICABLE] with rationale.
5. **Fill every table** with concrete, specific content — no placeholder values remaining in the final document.
6. **Write the Executive Summary (Section 1) last** — after all other sections are complete, synthesize the project's execution framework into a concise, standalone overview.
7. **Be specific, not vague** — write "2-week sprints starting every other Tuesday, with 40 story points/sprint velocity assumption for a team of 6 FTEs (4 developers, 1 QA, 1 DevOps)" not "Agile with regular sprints."
8. **Ensure internal consistency** — the schedule, budget, team, and scope must all be mutually consistent. If the plan says 40 points/sprint and the scope has 400 points of Must Have work, then at least 10 sprints are needed for Must Have alone. If the budget only covers 8 sprints of team cost, there is a gap that must be resolved.
9. **Cross-reference preceding documents** — when content derives from the business case, project scope, or viability study, reference them (e.g., "As defined in the Business Case Section 8.1, the approved investment is €500K CapEx over 12 months").
10. **Do not repeat analysis from preceding documents** — reference and summarize rather than duplicating. The project plan translates their recommendations into an executable framework.
11. **Make every section actionable** — the project plan must tell the team HOW to execute, not just WHAT the project is about. Governance, decision frameworks, escalation protocols, and communication plans must be specific enough to follow on Day 1 of the project.
12. **Populate the RACI matrix (Section 6.2)** with specific names or roles for every activity — a RACI with blank columns is not actionable.
13. **Populate the risk register (Section 10.2)** with risks from preceding documents AND execution-specific risks (e.g., key person dependency, vendor delay, environment provisioning delay, scope creep, team velocity below assumption).
14. **For 🟤🔵**: Populate the transition plan (Section 17) with specific cutover steps, rollback triggers, and decision authorities. The cutover runbook (Section 17.5) must be detailed enough to execute under pressure.
15. **For 🟤🔵**: Ensure the dual-running cost (Section 17.3) is reflected in the budget (Section 8.2) and the schedule (Section 7.1).
16. **For 🟢**: Ensure Sprint 0 / Inception is adequately detailed — team onboarding, tooling setup, environment provisioning, and architecture baseline must be planned before feature delivery can begin.
17. **Save the generated document** to an appropriate location, suggested: `documentation/project-plan.md` or `docs/project-plan.md`.

#### Quality Checks Before Delivery

After generating the document, perform these self-checks:

- [ ] Every section is either populated with project-specific content or marked [NOT APPLICABLE] with rationale.
- [ ] No `<!-- -->` placeholders remain (except the document status, date, and sign-off fields that require human input).
- [ ] The Executive Summary (Section 1) accurately reflects the full document — project type, delivery approach, key milestones, budget, team size, top risks, and critical dependencies are correct.
- [ ] The project type classification (Section 2.2) is consistent with how 🟢🟤🔵 sections are handled throughout the document.
- [ ] The delivery methodology (Section 2.3) is consistent with the sprint cadence (Section 7.4) and ceremonies.
- [ ] The budget overview (Section 8.1) total matches the sum of budget by phase (Section 8.2).
- [ ] The team composition (Section 12.1) is consistent with the budget staffing costs and the schedule velocity assumptions.
- [ ] The schedule phases (Section 7.1) and milestones (Section 7.2) are internally consistent and achievable.
- [ ] The release plan (Section 7.3) maps scope to releases consistently with the scope prioritization (Section 4.3).
- [ ] The RACI matrix (Section 6.2) has exactly one Accountable assignment per activity and no R+A conflicts.
- [ ] The risk register (Section 10.2) includes risks from preceding documents AND execution-specific risks.
- [ ] The risk budget allocation (Section 10.3) aligns with the budget's contingency reserve (Section 8.1).
- [ ] The governance structure (Section 5.1) and decision framework (Section 5.2) are consistent with the escalation protocol (Section 11.3).
- [ ] The communication plan (Section 11.1) and reporting schedule (Section 11.2) are consistent with governance cadence (Section 5.1).
- [ ] The deployment approach (Section 18.1) is consistent with the release plan (Section 7.3).
- [ ] The quality targets (Section 9.4) are measurable and consistent with the testing strategy (Section 9.2).
- [ ] For 🟤🔵: The transition strategy (Section 17.1) is consistent with the schedule (Section 7.1) and budget (Section 8.2).
- [ ] For 🟤🔵: The dual-running cost (Section 17.3) is reflected in the budget.
- [ ] For 🟤🔵: The legacy decommission plan (Section 17.4) has measurable prerequisites.
- [ ] For 🟤🔵: The cutover runbook (Section 17.5) has specific timelines, responsibilities, and rollback triggers.
- [ ] For 🟢: Sprint 0 / Inception is detailed with team setup, tooling, and environment provisioning.
- [ ] The change control process (Section 14.1) defines clear authority levels (Section 14.2).
- [ ] The issue management process (Section 15.1) defines priority levels with response times (Section 15.2).
- [ ] The stakeholder register (Section 16.1) and engagement plan (Section 16.2) are consistent.
- [ ] No contradictions exist between sections (if they do, flag them explicitly in the document).
- [ ] If preceding documents exist, the project plan is consistent with their key parameters (budget, timeline, scope, risks).

### Phase 4: Post-Generation Review

After the document is generated:

1. **Present the document** to the user.
2. **Highlight key judgments made** during generation — where the skill made interpretive calls (e.g., choosing a velocity assumption, estimating sprint counts, inferring governance structure from organizational context, balancing budget allocation across phases), point them out so the user can verify.
3. **Present the execution framework summary** clearly — delivery approach, key milestones, total budget, team size, top risks, and critical dependencies.
4. **Flag execution risks** — areas where the plan's assumptions are most fragile and which variables most affect the plan's viability. For example: "The plan assumes 40 points/sprint velocity, but with a new team the ramp-up period may take 3–4 sprints at 60–70% capacity. If velocity doesn't reach 40 by Sprint 5, the MVP milestone (M2) is at risk."
5. **Highlight internal consistency checkpoints** — where sections depend on each other and a change in one section requires updating others (e.g., "If the team size changes, update: Section 7.4 velocity, Section 8.2 budget by phase, Section 12.1 team composition, and Section 8.1 budget overview").
6. **Offer to refine** any section the user wants to adjust.
7. **Suggest next steps** — e.g., stakeholder review, governance activation, team mobilization, Sprint 0 planning, risk workshop, budget approval, baseline the plan.

## Examples

### Example Question (Gap — No Preceding Documents Found)

---

**[Critical] Section 2.1 & 4.1 — Project Purpose and Scope Statement**

No viability study, business case, or project scope document was found for this project. The project plan translates the "what and why" from these documents into "how, when, by whom" — without them, the plan lacks the foundational context that makes execution meaningful. The plan risks being a collection of empty tables rather than an actionable framework.

What is this project's purpose, scope, and the business context that drives it? What has already been decided about what will be delivered and why?

Suggested answers:
- *Option A*: "Preceding documents exist but are located elsewhere — I can provide the path or content. The project plan should read them and align its execution framework with their recommendations. The plan references them in Section 2.4 (Document Hierarchy) and builds upon their conclusions."
- *Option B*: "No formal preceding documents exist, but the project's purpose and scope have been discussed and agreed in stakeholder meetings. I can describe the project's goals, expected deliverables, and key constraints. The project plan should document these in Sections 3 and 4, flag them as 'not yet formally baselined,' and recommend that a project scope document be created as a priority to formalize the scope before the plan is baselined."
- *Option C*: "This project is early-stage with no formal analysis yet. The project plan should focus on the Sprint 0 / Inception phase as the primary near-term deliverable, with the understanding that the full plan will be elaborated after the scope and business case are completed. Sections 3, 4, 7, 8, and 10 should be populated with best-current-understanding content marked as 'Draft — pending formal scope definition.' The plan should explicitly state that baselining is deferred until preceding documents are approved."
- *Custom*: [your own answer]

---

### Example Question (Contradiction — Timeline vs. Scope)

---

**[Critical] Section 7.1 & 7.4 — Delivery Phases vs. Sprint Capacity**

The business case projects a 12-month delivery timeline, but the project scope defines 320 story points of Must Have scope and 180 points of Should Have scope. At an assumed velocity of 40 points/sprint with 2-week sprints, the Must Have scope alone requires 8 sprints (16 weeks), and the full scope requires ~13 sprints (26 weeks) of pure development time. Adding Sprint 0, testing phases, buffer, and hardening, the realistic timeline is 10–12 months for Must Have + Should Have — consistent with the business case. However, if the velocity assumption is for a new team (ramp-up period), the first 3–4 sprints may only achieve 60–70% velocity, extending the timeline to 13–14 months.

Is the 12-month timeline a hard constraint, or is it a target that can flex based on actual delivery velocity?

Suggested answers:
- *Option A*: "The 12-month timeline is a hard constraint driven by a contractual obligation / regulatory deadline / market window. The plan must include risk mitigation for schedule overrun: (1) prioritize Must Have scope for delivery within 10 months, (2) include a schedule reserve of 4 weeks, (3) plan for scope reduction if velocity does not reach 40 points by Sprint 5, and (4) define a decision point at Sprint 8 where the timeline is reassessed and Should Have scope may be deferred to protect the 12-month constraint."
- *Option B*: "The 12-month timeline is a target, not a constraint. The plan should use 12 months as the target but include a range: 10 months (optimistic, velocity exceeds assumption), 12 months (expected), 14 months (pessimistic, velocity below assumption or scope growth). The business case should have contingency for a 14-month timeline. The steering committee reviews progress at Gate G2 (end of Phase 1) and adjusts the timeline if needed."
- *Option C*: "The 12-month estimate includes the ramp-up period — the velocity assumption of 40 points/sprint is the steady-state velocity after ramp-up, with the first 3 sprints planned at 25, 30, and 35 points respectively. This means the effective average velocity over 12 months is ~37 points/sprint, yielding ~222 points in 6 months or ~444 points in 12 months (accounting for non-development sprints). The plan should model the velocity ramp-up explicitly and show the cumulative delivery forecast against the scope baseline."
- *Custom*: [your own answer]

---

### Example Question (Gap — No Budget Information)

---

**[Critical] Section 8.1 — Budget Overview**

No budget information was found in any existing documentation. The project plan's budget section is the primary financial control mechanism for the project — without it, the plan cannot define resource constraints, contingency reserves, or financial tracking. The budget also links to the business case's investment case — if the plan's budget exceeds the business case's approved amount, the plan is not executable.

What is the total approved budget for this project, and how is it allocated between capital expenditure (CapEx), operational expenditure (OpEx), and contingency?

Suggested answers:
- *Option A*: "The business case approved a total investment of €500K: €350K CapEx (team, infrastructure, tooling) and €150K OpEx (cloud services, licenses, support). Contingency reserve of 10% (€50K) is included within the total. The plan should break this down by phase and track it monthly. Budget ownership: the project sponsor approves draw-down; the PM tracks and reports."
- *Option B*: "There is no formally approved budget yet — the project has an indicative envelope of €300K–€500K based on early estimates. The plan should present a budget breakdown at the expected level (€400K) with a range: lower bound €300K (minimal scope, mostly internal staff), upper bound €500K (full scope with contractor augmentation). The plan should recommend formal budget approval as a prerequisite for project mobilization, with the detailed budget breakdown supporting the approval request."
- *Option C*: "Budget is managed at the program level — this project receives an allocation from the program's annual budget. The current allocation is €200K for the first 6 months, with a further allocation subject to Gate G2 review. The plan should present the Phase 1 budget in detail and note that Phase 2+ budget is indicative pending gate approval. Contingency is managed at the program level (15% of total program budget)."
- *Custom*: [your own answer]

---

### Example Question (Gap — No Team Information)

---

**[Critical] Section 6.1 & 12.1 — Team Composition**

No team composition information was found. The team is the primary execution resource — the plan's schedule, velocity, and budget all depend on who is on the team, their skills, and their availability. A plan without a defined team is not actionable: it cannot estimate velocity, calculate capacity, or budget staffing costs.

What is the planned team composition — roles, number of people, seniority, and internal vs. external split?

Suggested answers:
- *Option A*: "The team is partially formed: we have a Tech Lead (internal, full-time, already assigned) and a Product Owner (internal, 50% allocation, shared with another project). We need to hire: 3 developers (2 senior, 1 mid), 1 QA engineer (senior), 1 DevOps engineer (mid). We also need a Scrum Master (could be shared or part-time). The plan should assume a 6-person core team with hiring timeline for open positions — first 2 sprints may operate at reduced capacity while hiring completes. Budget should include contractor rates for the first 3 months if internal hiring takes longer."
- *Option B*: "The team will be fully external — a consultancy engagement with 4 developers, 1 QA, 1 DevOps, and a part-time Scrum Master, plus a part-time internal Product Owner and Technical Lead for governance. The consultancy provides the delivery team; the internal team provides direction, acceptance, and stakeholder management. The plan should reflect this split in the RACI (internal = Accountable for decisions, external = Responsible for delivery) and budget (external team costs are CapEx)."
- *Option C*: "The team composition is not yet defined. The plan should include a team composition recommendation based on the scope: for a project of this size and complexity, a typical team would be [X developers, Y QA, Z DevOps, 1 PO, 1 SM, 1 TL]. The plan should present this as a proposed composition with alternatives (smaller team / longer timeline vs. larger team / shorter timeline) and flag team mobilization as a critical-path prerequisite for Sprint 0."
- *Custom*: [your own answer]

---

### Example Question (Gap — No Governance Defined)

---

**[Important] Section 5.1 — Governance Structure**

No governance structure was found in existing documentation. The governance structure determines how decisions are made, who makes them, and how issues are escalated — without it, the project lacks a decision-making framework and will default to ad-hoc decisions or decision paralysis. The plan must define this before execution begins.

What is the project's governance structure — who sits on the steering committee, how often do they meet, and what decisions do they make?

Suggested answers:
- *Option A*: "Steering committee meets monthly, composed of: Project Sponsor (VP Engineering — budget and strategic decisions), Product Owner (Business Lead — scope and priority decisions), Project Manager (execution and risk decisions), and Tech Lead (architecture and technical decisions). The committee approves: scope changes exceeding 5% budget impact, timeline extensions exceeding 2 weeks, risk mitigation actions requiring contingency draw-down, and stage-gate progression. Escalation path: team → PM → Steering Committee → Sponsor (for emergency decisions within 24 hours)."
- *Option B*: "Lightweight governance — no formal steering committee. The Product Owner makes scope and priority decisions. The Project Manager makes execution and risk decisions. The Sponsor is engaged only for budget approvals and escalation of critical issues. Monthly status report to the Sponsor. This is appropriate for a small project with low complexity and a trusted team. The plan should document this and define the escalation path for when decisions exceed the PM/PO authority."
- *Option C*: "The project is part of a program with existing program-level governance. The program's steering committee meets quarterly and makes strategic decisions (budget, scope, timeline). For project-level decisions, the project has a biweekly sync with the Program Manager and the Product Owner. The plan should define the project-level decision framework within the program's governance boundaries and note which decisions require program-level approval."
- *Custom*: [your own answer]

---

### Example Question (Modernization — Migration Approach)

---

**[Critical] Section 17.1 — Transition Strategy**

For a Software Modernization project, no transition strategy was found in existing documentation. The transition approach is the defining execution decision for a modernization project — it determines the schedule, budget, risk profile, and team structure. Without it, the plan cannot define the migration phases, dual-running costs, rollback strategy, or decommission timeline.

What is the migration approach for transitioning from the legacy system to the new system?

Suggested answers:
- *Option A*: "Phased migration using the strangler fig pattern — features are migrated incrementally, with a feature flag routing traffic to the new system for each migrated feature. Dual-running period: 4 months (estimated). Legacy system remains operational until all features are migrated and validated. Decommission: 2 months after final feature cutover. Rollback: feature flags can route traffic back to the legacy system within 30 minutes for any individual feature. Cutover decision authority: Tech Lead recommends, PM approves, Sponsor decides for high-risk cutovers. This approach reduces risk but extends the timeline and increases dual-running cost."
- *Option B*: "Big bang cutover — all users switch to the new system on a planned cutover date. The legacy system is put into read-only mode on D-7, data migration runs on D-2 to D-1, validation on D-1, and the switch occurs on D-Day. Rollback: revert to the legacy system's read-only snapshot within 4 hours if critical issues are found. Cutover decision: PM decides go/no-go at T-24h based on predefined criteria. This approach is faster and avoids dual-running costs, but has higher risk and requires a detailed cutover runbook with rollback triggers."
- *Option C*: "Parallel run for 3 months — both systems operate simultaneously, with data synchronization and comparison testing. Users gradually migrate to the new system in cohorts. After all users are migrated and comparison testing confirms feature parity, the legacy system is decommissioned. This approach provides the highest confidence but has the highest dual-running cost (estimated €X/month) and longest timeline. Rollback: users simply continue on the legacy system until the new system is verified."
- *Custom*: [your own answer]

---

### Example Question (Brown Field — Regression Risk)

---

**[Important] Section 9.2 & 10.2 — Regression Risk for Brown Field Enhancement**

For a Brown Field project extending an existing system, the existing documentation does not address regression risk — the risk that enhancements break existing functionality. This is a primary execution risk for Brown Field projects: every change to the existing codebase carries the potential for unintended side effects. Without a regression risk mitigation strategy, the plan cannot assure stakeholders that existing capabilities will be preserved.

What is the regression risk mitigation strategy — how will the project ensure that existing functionality is not broken by the enhancements?

Suggested answers:
- *Option A*: "The existing system has 65% automated test coverage. The plan's quality strategy (Section 9.2) includes: (1) all new code must have unit and integration tests before merge (enforced by CI pipeline), (2) an automated regression suite covering critical user journeys runs on every deployment to staging, (3) the team adds regression tests for any existing behavior that is modified or adjacent to modified code, (4) a manual smoke test of the top 20 user workflows runs before each release. Regression defects found in production are tracked as a KPI (target: <2% defect escape rate)."
- *Option B*: "The existing system has low test coverage (~20%). The plan's quality strategy includes a dedicated Sprint 1 activity to establish a regression testing baseline: (1) create automated smoke tests for the top 15 critical user journeys, (2) add integration tests for the modules being modified, (3) enforce a 'no deployment without regression pass' policy in the CI/CD pipeline. The plan should budget 15% of sprint capacity for regression test creation and maintenance in the first 4 sprints, reducing to 10% ongoing."
- *Option C*: "The existing system has no automated tests — it is a legacy system with significant technical debt. The plan should include a risk item (R-X): 'Low test coverage creates high regression risk — estimated 30% probability of a regression defect in production per release.' Mitigation: (1) invest in regression test automation as a Sprint 0 activity, (2) plan for extended UAT cycles with business users, (3) deploy to a staging environment that mirrors production for manual regression testing, (4) use feature flags to limit the blast radius of changes, (5) maintain a rollback capability for every release. The risk budget should include contingency for regression-related rework."
- *Custom*: [your own answer]

---

### Example Question (Green Field — Sprint 0 / Inception)

---

**[Important] Section 7.1 — Sprint 0 / Inception Phase**

For a Green Field project, Sprint 0 / Inception is critical — it establishes the team, tooling, environments, and architecture baseline before feature delivery can begin. No Sprint 0 plan was found in existing documentation. Without it, the team will start delivering features without the infrastructure to support them, leading to technical debt, integration problems, and delayed velocity ramp-up.

What is the Sprint 0 / Inception plan — what will be established before feature delivery begins?

Suggested answers:
- *Option A*: "Sprint 0 (2 weeks) delivers: (1) development environment setup (IDE, version control, branching strategy), (2) CI/CD pipeline with automated build, test, and deployment to dev/integration environments, (3) architecture baseline — initial project structure, core frameworks, and key ADRs documented, (4) team onboarding — access provisioned, coding standards agreed, Definition of Done defined, (5) backlog refinement — top 20 stories refined and estimated, Sprint 1 planned. This is a Must Have prerequisite — no feature work starts until Sprint 0 is complete."
- *Option B*: "Sprint 0 (1 week) delivers the minimum viable infrastructure: (1) version control and branching strategy, (2) basic CI pipeline (build + unit tests), (3) development environment with core frameworks. CI/CD to staging and production is delivered as part of Sprint 1 (DevOps story). Architecture baseline emerges during Sprint 1 and 2 as the team builds the first feature. This minimizes upfront setup time but risks rework if early architectural decisions need revisiting."
- *Option C*: "No formal Sprint 0 — the team uses the first 2 sprints as an 'inception period' where they deliver the first small feature AND set up infrastructure simultaneously. This keeps the team delivering user value from Sprint 1 while building the foundation. The risk is that infrastructure setup competes with feature delivery for capacity, effectively reducing velocity in Sprints 1–2. The plan should account for this reduced capacity (50% of steady-state velocity in Sprint 1, 75% in Sprint 2)."
- *Custom*: [your own answer]

---

## Anti-Patterns to Avoid

- **Don't generate the document without asking questions** — the project plan's value is in the execution-level analysis and internal consistency, not in template filling. An internally inconsistent plan is worse than no plan.
- **Don't ask questions that existing documentation already answers** — read carefully and use available information directly.
- **Don't ask too many questions at once** — batch by priority, lead with critical questions, offer to proceed with assumptions for lower-priority items.
- **Don't produce an internally inconsistent plan** — if the schedule, budget, team, and scope don't add up, the plan is not executable. Resolve contradictions before generating.
- **Don't be vague about governance** — "The steering committee meets regularly" is not actionable. "The steering committee (Sponsor, PO, PM, Tech Lead) meets on the first Thursday of each month from 10:00–11:30, decides on scope changes >5% budget impact, and requires a written decision log" is actionable.
- **Don't skip the RACI matrix** — it is the primary accountability mechanism. Every activity must have exactly one Accountable person.
- **Don't create a risk register with only obvious risks** — "The project may be delayed" is not a useful risk. "Key person dependency: the Tech Lead is the only person who understands the legacy data model; if they leave, data migration design is blocked for 4–6 weeks while a replacement ramps up" is a useful risk.
- **Don't treat the budget as a single number** — it must be broken down by phase, by category (CapEx/OpEx), and include contingency with access criteria. A budget that cannot be tracked cannot be controlled.
- **Don't ignore the velocity ramp-up** — new teams don't reach steady-state velocity immediately. The plan must model the ramp-up period explicitly or the schedule will be wrong.
- **Don't skip the transition plan for 🟤🔵 projects** — migration is the highest-risk phase of a modernization project. The plan without a detailed transition strategy is not a plan.
- **Don't duplicate content from preceding documents** — the project plan translates their recommendations into execution; it does not re-perform their analysis. Reference and summarize.
- **Don't mark sections [NOT APPLICABLE] just because they're hard to populate** — only mark them if they genuinely don't apply to the project type.
- **Don't produce a plan that can't be followed on Day 1** — the plan must be actionable from the moment it is baselined. If a section says "to be determined," it's a gap, not a plan.
- **Don't forget to include Sprint 0 / Inception for 🟢 projects** — the team cannot deliver features without infrastructure, tooling, and baseline architecture.
- **Don't conflate the project plan with the project scope** — the scope defines WHAT will be delivered; the project plan defines HOW, WHEN, BY WHOM, and WITH WHAT RESOURCES it will be delivered.
- **Don't produce a plan that contradicts the business case** — if the plan's budget, timeline, or scope differs from the business case, the plan must explain the variance and get approval for the change through the change control process.
- **Don't forget the change control process (Section 14)** — the project plan is a living document. It will change. The plan must define HOW it changes, WHO approves changes, and WHAT happens when changes exceed authority levels.
- **Don't skip the closeout plan (Section 19)** — projects must end cleanly. Knowledge transfer, post-implementation review, and handover to operations must be planned, not improvised.

## Document Hierarchy Context

The Project Plan is the **fourth or fifth** formal document in the project lifecycle, depending on which preceding documents were produced. It builds upon and translates:

| Document | Relationship | Precedes Project Plan? |
|----------|-------------|------------------------|
| **Viability Study** | Determines whether the project is feasible — the plan must be consistent with the feasibility assessment and project type classification | Yes — the plan references the viability study's key findings and risks |
| **Business Case** | Defines the investment case — the plan's budget, timeline, and resource assumptions must align with the approved investment option | Yes — the plan translates the business case's investment into an executable framework |
| **Project Scope** | Defines delivery boundaries — the plan's scope summary, deliverables, and priorities must reference and align with the scope document | Yes — the plan executes within the scope boundaries; it does not redefine them |
| **SRS** | Defines what the system must do — the plan's quality strategy and testing approach derive from the SRS's requirement specifications | Yes — the plan's quality management (Section 9) is informed by the SRS |

And it precedes:

| Document | Relationship | Follows Project Plan? |
|----------|-------------|----------------------|
| **Sprint Backlogs** | Select stories for sprint delivery based on the plan's sprint cadence and capacity | Yes — the plan defines the cadence; backlogs populate it |
| **Architecture Design** | Implements the plan's technical approach through architectural decisions | Yes — the plan's Section 12.4 and Appendix E inform architecture |
| **Test Plans** | Verify requirements through test cases aligned with the plan's quality strategy | Yes — the plan's Section 9 defines the testing strategy |
| **Operational Runbooks** | Support the deployment and incident response strategy defined in the plan | Yes — the plan's Sections 17.5 and 18.4 inform runbooks |

When generating the project plan, keep in mind that its primary output is an **actionable, internally consistent execution framework** that tells the team and stakeholders HOW the project will be delivered, WHEN milestones will be reached, WHO is responsible and accountable for what, WITH WHAT budget and resources, under WHAT governance and decision-making structure, and HOW risks, issues, and changes will be managed. The project plan is the authoritative source for project execution — once baselined, conflicts with other documents are resolved in favor of this plan (except where superseded by the business case or scope document).