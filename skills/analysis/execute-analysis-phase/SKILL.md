---
name: execute-analysis-phase
description: Orchestrates the complete analysis phase of a software project by chaining documentation review, gap analysis, idea refinement, viability study, business case, user stories, requirements specification, and project plan generation. Use when starting a new software project, when a user says "analyze my project", "run the analysis phase", "start project analysis", or when the full analysis pipeline needs to be executed from documentation through to project plan.
---

# Skill: Execute Analysis Phase

## Overview

Orchestrates the **complete analysis phase** of a software project — from raw documentation and ideas through to a structured project plan. This is the master workflow that chains every analysis sub-skill together, ensuring each step's output feeds the next step's input, gaps are caught early, and contradictions are resolved before they cascade into downstream documents.

The analysis phase transforms ambiguity into clarity through a structured pipeline:

```
Documentation → Understanding → Gap Resolution → Idea Refinement
     → Viability Study → Business Case → User Stories
          → Requirements Specification → Project Plan
```

## When to Use

**Use this skill when:**
- Starting analysis of a new software project or product
- A user requests "analyze my project", "run the full analysis", or "start the analysis phase"
- You need to take a project from raw concept to a complete set of analysis deliverables
- The project has external documentation that needs to be deeply analyzed before proceeding

**Do NOT use this skill when:**
- Only a single analysis artifact is needed (use the specific sub-skill instead)
- The project is already in development — use individual skills for targeted artifacts
- The user only wants to review or update an existing analysis document

## Core Process

The analysis phase is executed in **9 stages**. Each stage has a quality gate that must be passed before proceeding to the next. Stages may reveal information that requires revisiting earlier stages — this is expected and encouraged.

### Stage 1: Documentation Check & Intake

**Goal:** Ensure the agent has access to the right source material before analysis begins.

1. **Check if the user has referenced external documentation.** Look for:
   - Explicit mentions of documents, URLs, files, or resources
   - Attached files or pasted content
   - References to existing repositories, wikis, or knowledge bases
   - Pointers to RFCs, specs, meeting notes, or stakeholder communications

2. **If no documentation is referenced explicitly, ask the user:**

   > I need source material to perform a thorough analysis. Please provide or point to any of the following:
   >
   > - **Project brief or README** — What is this project about?
   > - **External documentation** — Any referenced standards, regulations, or domain docs
   > - **Architecture diagrams or RFCs** — Technical specifications or design proposals
   > - **Stakeholder communications** — Meeting notes, decision logs, email threads
   > - **Existing codebase or repositories** — If any code already exists
   > - **Competitor or market analysis** — If available
   >
   > Even a rough 1-page description is enough to start. The more you provide, the deeper the analysis.

3. **Catalog all received documentation** in a Documentation Inventory:
   - Document name / source
   - Type (brief, spec, RFC, code, market analysis, etc.)
   - Relevance (high / medium / low)
   - Trust level (authoritative / draft / unofficial / external-unverified)

**Quality Gate 1:** At least one document or source of project information exists before proceeding. If the user provides nothing, do NOT invent requirements — ask again or suggest a structured interview instead.

---

### Stage 2: Deep Documentation Analysis

**Goal:** Build a thorough understanding of the project concept and scope from all available material.

1. **Read every document in the Documentation Inventory thoroughly.** Do not skim — extract:
   - Core concept: What is being built and why?
   - Target users and stakeholders
   - Key features and capabilities mentioned
   - Constraints (budget, timeline, technology, compliance, regulations)
   - Success criteria or expected outcomes
   - Explicitly stated out-of-scope items
   - Technical assumptions or decisions already made

2. **Synthesize a Project Understanding Statement:**
   - One-paragraph summary of what the project aims to deliver
   - List of key stakeholders and their implied interests
   - Project type classification: Green Field / Brown Field / Software Modernization
   - Initial scope boundaries (what seems in vs. out of scope)

3. **Map the documentation landscape:**
   - Which aspects are well-documented?
   - Which aspects are only partially covered?
   - Which aspects have no documentation at all?

**Quality Gate 2:** The agent can articulate the project's core concept in the user's words and the user confirms this understanding is correct. Present the Project Understanding Statement to the user and get explicit confirmation before proceeding.

---

### Stage 3: Gap & Contradiction Analysis

**Goal:** Identify every information gap and contradiction before they poison downstream deliverables.

1. **Systematically check for gaps across these dimensions:**

   | Dimension | What to Check |
   |-----------|---------------|
   | **Problem & Goals** | Is the problem clearly stated? Are success criteria measurable? |
   | **Users & Stakeholders** | Are all user types identified? Are stakeholder priorities known? |
   | **Scope & Boundaries** | Are in-scope and out-of-scope items explicit? |
   | **Constraints** | Are budget, timeline, technology, compliance constraints stated? |
   | **Dependencies** | Are external systems, APIs, data sources identified? |
   | **Risks & Assumptions** | Are key risks called out? Are assumptions explicit? |
   | **Non-Functional Requirements** | Performance, security, scalability, accessibility needs? |
   | **Existing System** (if Brown Field/Modernization) | Current state documented? Migration constraints known? |

2. **Check for contradictions between sources:**
   - Do different documents disagree on scope, priorities, or constraints?
   - Are there implicit contradictions (e.g., "agile" process but fixed-scope contract)?
   - Do stated timelines match the implied complexity?
   - Do budget constraints match the ambition level?

3. **Produce a Gap & Contradiction Register:**
   - Each gap: ID, dimension, description, severity (Critical / Important / Optional)
   - Each contradiction: ID, sources, description, resolution options

**Quality Gate 3:** The gap/contradiction register is complete and presented to the user. At least all Critical gaps have a path to resolution (via interview or deferred assumption).

---

### Stage 4: Gap Resolution via Interview

**Goal:** Fill critical gaps and resolve contradictions through structured interviewing.

1. **Invoke the `/interview-me` skill** to address all gaps and contradictions from Stage 3.
   - Prioritize Critical gaps first, then Important, then Optional.
   - Frame interview questions around the gaps — do not re-ask what documentation already answers.
   - Use the interview-me process: one question at a time, with confidence tracking, until ~95% confidence on each gap.

2. **Specific interview targets based on gap type:**

   | Gap Type | Interview Focus |
   |----------|----------------|
   | Unclear problem/goals | "What does success look like? How would you measure it?" |
   | Unknown users | "Who are the primary users? Who else is affected?" |
   | Vague scope | "What's the smallest version that would be valuable? What's definitely NOT in scope?" |
   | Missing constraints | "What budget, timeline, or technology constraints exist?" |
   | Unstated assumptions | "What assumptions are you making that, if wrong, would change the plan?" |
   | Contradictions | "Source A says X, Source B implies Y. Which reflects your intent?" |

3. **Update the Gap & Contradiction Register** with interview outcomes:
   - Resolved gaps → document the answer
   - Partially resolved → note what's still needed
   - Unresolved → flag for assumption with rationale
   - Contradictions resolved → document which source takes precedence

**Quality Gate 4:** All Critical gaps are resolved. Important gaps are either resolved or have a documented assumption with user acknowledgment. The Project Understanding Statement is updated to reflect new information.

---

### Stage 5: Idea Refinement

**Goal:** Sharpen the concept into a precise, actionable idea with validated assumptions.

1. **Invoke the `/idea-refine` skill** on the confirmed Project Understanding Statement.
   - Feed the skill the full understanding statement, resolved gaps, and any constraints identified.
   - The idea-refine skill will apply divergent and convergent thinking to stress-test and refine the concept.

2. **Ensure idea refinement covers:**
   - **Core value proposition** — What unique value does this project deliver?
   - **Key assumptions** — What must be true for this to succeed? Which are riskiest?
   - **Edge cases & second-order effects** — What could go wrong beyond obvious risks?
   - **Alternative approaches** — Is this the best way to solve the problem? What else was considered?
   - **Refinement criteria** — Is the idea specific enough to start viability assessment?

3. **Capture the Refined Project Concept:**
   - Updated Project Understanding Statement incorporating refinement
   - Validated key assumptions (with confidence levels)
   - Explicitly rejected alternatives (with reasons)
   - Refined scope boundaries

**Quality Gate 5:** The refined concept is specific enough that viability can be assessed. The user confirms: "Yes, this accurately represents what I want to explore." If the refinement reveals the idea is not viable or needs fundamental rethinking, loop back to Stage 4 before proceeding.

---

### Stage 6: Viability Study

**Goal:** Determine whether the project should proceed at all.

1. **Invoke the `/generate-viability-study` skill.**
   - Input: Refined Project Concept, Documentation Inventory, Gap & Contradiction Register
   - The skill will use the template at `templates/analysis/viability-study.md`

2. **The viability study assesses:**
   - Technical feasibility — Can it be built with available technology and expertise?
   - Economic viability — Do expected benefits justify expected costs?
   - Organizational readiness — Can the organization support this project?
   - Market / regulatory alignment — Does the external environment support it?
   - Risk profile — Are the risks acceptable and manageable?

3. **Review the viability study output:**
   - Does the recommendation align with the user's expectations?
   - Are there showstoppers that should halt the analysis phase?
   - Are there conditions that must be met for the project to remain viable?

4. **Decision point — present to the user:**
   - If **viable** → proceed to Stage 7 (Business Case)
   - If **conditionally viable** → discuss conditions with user, then proceed or pause
   - If **not viable** → stop and discuss alternatives; do NOT proceed to business case

**Quality Gate 6:** Viability study is complete and the user has explicitly decided to proceed (or has provided conditions to proceed under). If the user decides not to proceed, the analysis phase ends here with the viability study as the final deliverable.

---

### Stage 7: Business Case

**Goal:** Build the investment case — should the organization commit resources, how much, and to which option?

1. **Invoke the `/generate-business-case` skill.**
   - Input: Viability study, Refined Project Concept, Documentation Inventory
   - The skill will use the template at `templates/analysis/business-case.md`

2. **The business case develops:**
   - Strategic alignment — How does this project support organizational goals?
   - Options analysis — What are the viable approaches? (build, buy, partner, etc.)
   - Cost-benefit analysis — Quantified where possible
   - Risk assessment — With mitigation strategies
   - Recommended option — With rationale

3. **Cross-reference with viability study:**
   - Verify that the business case's assumptions are consistent with the viability study's findings
   - If the viability study flagged conditions, ensure the business case addresses them
   - If the business case introduces new assumptions, add them to the Gap & Contradiction Register

4. **Present the business case to the user** for review and decision:
   - Which option is recommended and why
   - What the investment profile looks like
   - What key risks remain

**Quality Gate 7:** Business case is complete, the user has reviewed it, and has confirmed the recommended direction. If the user chooses an option different from the recommendation, document their rationale before proceeding.

---

### Stage 8: User Stories & Requirements Specification

**Goal:** Define what the system must do and how users will interact with it.

These two artifacts are generated in sequence because user stories inform requirements, and requirements formalize user stories.

#### Stage 8a: User Stories

1. **Invoke the `/generate-user-stories` skill.**
   - Input: Business case, Refined Project Concept, Viability study
   - The skill will use the template at `templates/analysis/user-stories.md`

2. **Ensure user stories cover:**
   - All user roles identified in the analysis
   - All key features from the business case's recommended option
   - Non-functional requirements expressed as user-facing stories where possible
   - Priority ordering (Must Have / Should Have / Could Have / Won't Have)
   - Acceptance criteria for each story

#### Stage 8b: Software Requirements Specification

1. **Invoke the `/generate-software-requirements-specification` skill.**
   - Input: User stories, Business case, Viability study, Refined Project Concept
   - The skill will use the template at `templates/analysis/software-requirements-specification.md`

2. **Ensure the SRS covers:**
   - Functional requirements (derived from user stories)
   - Non-functional requirements (performance, security, usability, etc.)
   - System interfaces and integrations
   - Data requirements
   - Constraints and assumptions
   - Traceability from each requirement to user stories and business objectives

3. **Cross-reference user stories with SRS:**
   - Every user story must have at least one corresponding requirement
   - Every functional requirement must trace back to at least one user story
   - Gaps in either direction must be resolved before proceeding

**Quality Gate 8:** User stories and SRS are complete, internally consistent, and cross-referenced. The user has reviewed both and confirmed they accurately represent the desired system behavior.

---

### Stage 9: Project Plan

**Goal:** Translate everything into an actionable plan — how, when, by whom, with what resources.

1. **Invoke the `/generate-project-plan` skill.**
   - Input: SRS, User stories, Business case, Viability study
   - The skill will use the template at `templates/analysis/project-plan.md`

2. **Ensure the project plan covers:**
   - Work breakdown structure (derived from requirements and user stories)
   - Phase/milestone definitions
   - Resource allocation and team structure
   - Timeline with dependencies
   - Risk management plan (updated from business case)
   - Budget allocation (aligned with business case)
   - Governance and decision-making framework

3. **Cross-reference with preceding deliverables:**
   - Every work package traces to at least one requirement
   - Timeline is consistent with business case assumptions
   - Budget is aligned with business case cost estimates
   - Risks from the viability study and business case are addressed in the risk management plan
   - User story priorities are reflected in phasing and scheduling

**Quality Gate 9:** The project plan is complete, traceable to all preceding deliverables, and the user has reviewed and approved it. The analysis phase is complete.

---

## Deliverables Summary

Upon completion of the analysis phase, the following artifacts should exist:

| # | Deliverable | Template | Depends On |
|---|-------------|----------|------------|
| 1 | Documentation Inventory | — | Stage 1 output |
| 2 | Project Understanding Statement | — | Stage 2 output |
| 3 | Gap & Contradiction Register | — | Stage 3 output |
| 4 | Refined Project Concept | — | Stages 4–5 output |
| 5 | Viability Study | `templates/analysis/viability-study.md` | Stage 6 output |
| 6 | Business Case | `templates/analysis/business-case.md` | Stage 7 output |
| 7 | User Stories | `templates/analysis/user-stories.md` | Stage 8a output |
| 8 | Software Requirements Specification | `templates/analysis/software-requirements-specification.md` | Stage 8b output |
| 9 | Project Plan | `templates/analysis/project-plan.md` | Stage 9 output |

All deliverables should be saved in the project's `documentation/` directory or as directed by the user.

## Traceability Chain

Every element in the final project plan must be traceable backwards through the pipeline:

```
Project Plan work package
  → SRS requirement
    → User story
      → Business case objective
        → Viability study finding
          → Refined concept assumption
            → Original documentation / interview answer
```

If any link in this chain is broken, the analysis is incomplete. Flag broken traceability links explicitly and resolve them before closing the analysis phase.

## Handling Iterations & Backtracking

The analysis phase is not strictly linear. New information discovered at any stage may require revisiting earlier stages:

| Discovery at Stage... | May Require Revisiting... | Action |
|-----------------------|--------------------------|--------|
| Stage 5 (Idea Refine) | Stage 2 (Understanding) | Update Project Understanding Statement |
| Stage 6 (Viability) | Stage 4 (Interview) | Ask new questions raised by viability assessment |
| Stage 7 (Business Case) | Stage 5 (Idea Refine) | Re-refine concept if business case reveals new constraints |
| Stage 8 (User Stories / SRS) | Stage 7 (Business Case) | Update business case if requirements reveal cost implications |
| Stage 9 (Project Plan) | Stage 8 (User Stories / SRS) | Adjust requirements if planning reveals feasibility issues |

**Rules for backtracking:**
1. Always inform the user when backtracking is needed and why
2. Re-run the affected sub-skill(s), not just patch the output
3. Propagate changes forward through all dependent deliverables
4. Update the Gap & Contradiction Register with any new findings

## Common Rationalizations

| Rationalization | Reality |
|---|---|
| "We can skip the viability study — we already know it's viable" | Skipping viability means you carry unvalidated assumptions into the business case, which compounds risk in every downstream document. |
| "The documentation is thin — let's just start generating and fill gaps as we go" | Garbage in, garbage out. Thin documentation is exactly when you need the interview-me skill most. |
| "We don't need user stories for an internal tool" | Internal tools have users too. Skipping user stories means skipping empathy and use-case coverage, which leads to requirements gaps. |
| "The idea-refine step feels redundant after the interview" | Interviewing extracts intent; idea refinement stress-tests it. They serve different purposes — one asks "what do you want?", the other asks "is this the right thing to want?" |
| "Let's just generate all documents at once" | Each document builds on the previous one's output. Generating them all at once means no quality gates, no traceability, and no opportunity for the user to course-correct. |
| "We can fix contradictions later" | Contradictions compound. A contradiction in the viability study becomes a contradiction in every downstream document. Resolve them early. |

## Red Flags

- Agent proceeds to viability study without confirmed Project Understanding Statement
- Gaps marked as Critical are deferred without user acknowledgment
- Business case recommendation contradicts viability study findings without explanation
- User stories don't trace back to business case objectives
- SRS requirements have no corresponding user stories
- Project plan work packages have no traceability to requirements
- Agent invents requirements not supported by any documentation or interview
- Quality gates are skipped because "the user seems eager to proceed"
- Backtracking is avoided because "we already spent time on that stage"
- The user was never asked for clarification on critical gaps

## Verification

Before declaring the analysis phase complete, verify:

- [ ] Documentation Inventory exists and all sources are accounted for
- [ ] Project Understanding Statement is confirmed by the user
- [ ] Gap & Contradiction Register has no unresolved Critical items
- [ ] Refined Project Concept has been validated through idea-refine
- [ ] Viability study has been reviewed and the user decided to proceed
- [ ] Business case has been reviewed and the user confirmed the direction
- [ ] User stories are complete with priorities and acceptance criteria
- [ ] SRS is complete with traceability to user stories and business objectives
- [ ] Project plan is complete with traceability to requirements and business case
- [ ] Full traceability chain from project plan back to original documentation is intact
- [ ] All deliverables are saved in the project documentation directory
- [ ] The user has reviewed and approved the complete analysis package