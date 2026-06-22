---
name: generate-viability-study
description: Generates a Software Project Viability Study. The skill conducts deep investigative analysis of all available project information, stakeholder inputs, market evidence, and technical landscape to populate every applicable section. The viability study is the **first formal analysis document** in the project lifecycle — its purpose is to determine whether a project *should* proceed, not just *how*.
---

# Skill: Generate Viability Study

## Description

Generates a complete, rigorous Software Project Viability Study based on the template `templates/analysis/viability-study.md`. The skill conducts deep investigative analysis of all available project information, stakeholder inputs, market evidence, and technical landscape to populate every applicable section. When gaps, unclear statements, or contradictions are detected, the skill asks targeted open questions with suggested valid answers before proceeding. The viability study is the **first formal analysis document** in the project lifecycle — its purpose is to determine whether a project *should* proceed, not just *how*.

## Activation

When the user requests to create, generate, or draft a viability study, feasibility study, or viability assessment for a software project.

## Instructions

### Phase 1: Information Gathering & Deep Analysis

1. **Read the template** at `templates/analysis/viability-study.md` to understand the full structure, all 15 sections, their expected content, and project-type applicability (🟢 🟤 🔵 ⚪).

2. **Discover and read all existing project information:**
   - Search the workspace for any pre-existing analysis documents (check `documentation`, project folders, or any `.md` files with "viability", "feasibility", "business-case", or "analysis" in the name).
   - Search for any requirements documents, architecture decision records (ADRs), README files, or project documentation.
   - Search for any configuration files (`package.json`, `pom.xml`, `build.gradle`, `docker-compose.yml`, etc.) that reveal the technology stack and system boundaries.
   - If a codebase exists, explore the directory structure to understand current modules, services, and integrations.
   - Search for any stakeholder communication, meeting notes, decision logs, or email summaries.
   - Search for any existing financial data, cost reports, or budget documents.
   - Search for any compliance or security documentation (policies, audit reports, certifications).

3. **Classify the project type** based on available evidence:
   - **Green Field (🟢)**: No existing codebase; new product being built from scratch.
   - **Brown Field (🟤)**: Existing system being extended, refactored, or enhanced.
   - **Software Modernization (🔵)**: Legacy system being migrated, re-platformed, or re-architected.
   - If classification is ambiguous (e.g., extending an existing system while simultaneously re-architecting it), note this as a question for Phase 2 — the classification determines which sections apply and how the analysis is framed.

4. **Map existing information to template sections.** For each section of the viability study template, determine:
   - **Covered**: Sufficient information exists to populate the section with evidence-based content.
   - **Partially Covered**: Some information exists but is incomplete, ambiguous, or lacks supporting evidence.
   - **Gap**: No information exists for this section.
   - **Contradiction**: Information from different sources conflicts or is internally inconsistent.

5. **Perform deep gap-contradiction analysis.** The viability study is an investigative document — go beyond surface-level mapping:

   **Cross-domain consistency checks:**
   - If a project claims to address a market opportunity (Section 4), is there actual demand evidence or just stakeholder assertions?
   - If a technology is proposed (Section 5), is there evidence of organizational readiness to adopt it (Section 8)?
   - If benefits are claimed (Section 7), do the cost estimates (Section 7.1) and timeline (Section 5.7) make those benefits achievable within the projected timeframe?
   - If the project is classified as modernization (🔵), is there sufficient understanding of the current system (Section 3) to assess migration feasibility (Section 5.4)?
   - If the project claims competitive advantage (Section 4.3), is that advantage durable or easily replicated?

   **Evidence sufficiency checks:**
   - Are key claims backed by data, or are they assumptions presented as facts?
   - Are financial projections based on comparable projects, market research, or just optimistic estimates?
   - Is the risk assessment (Section 11) realistic — does it include only obvious risks, or has it considered second-order effects and systemic risks?
   - Has the "do nothing" alternative (Section 13) been genuinely evaluated with its own cost trajectory?

   **Internal logic checks:**
   - Does the SWOT analysis (Section 12) align with the risk register (Section 11)? Strengths should mitigate risks; weaknesses should amplify threats.
   - Do the alternatives analyzed (Section 13) include all options identified in the competitive landscape (Section 4.3)?
   - Does the recommended alternative (Section 13.3) align with the overall assessment (Section 14.1)?
   - Are the go/no-go criteria (Section 14.3) actually measurable and decision-useful, or are they vague?

   **Project-type-specific checks:**
   - 🟢 Green Field: Is the market size (Section 4.2) and demand validation (Section 4.4) sufficient to justify building from scratch vs. buying?
   - 🟤 Brown Field: Is the technical debt assessment (Section 3.3) detailed enough to determine whether extending is viable vs. rebuilding?
   - 🔵 Modernization: Is the data migration strategy (Section 5.4) feasible given the current system assessment (Section 3)? Are legacy vendor exit costs (Section 6.4) accounted for?

6. **Build a viability evidence map** — for each section, tag the quality of available evidence:
   - 🟢 **Strong Evidence**: Data-backed, verified from multiple sources, or directly observable.
   - 🟡 **Moderate Evidence**: Single-source data, stakeholder reports, or extrapolated from analogous situations.
   - 🔴 **Weak/No Evidence**: Assertions, assumptions, or no information available.

   Sections with 🔴 evidence quality are priority candidates for Phase 2 questions.

### Phase 2: Clarification Questions

Before generating the document, ask the user targeted questions for every **Partially Covered**, **Gap**, **Contradiction**, or **Weak/No Evidence** area identified in Phase 1.

#### Question Design Principles

- **Ask open questions** that invite thoughtful responses and deeper thinking — not yes/no questions.
- **Always suggest 2–3 possible valid answers** for each question to help the user think through the options and to demonstrate understanding of the domain.
- **Contextualize each question** — briefly explain why the information matters for the viability decision and what happens if it remains unanswered (e.g., "Without this, the study cannot determine whether the project is financially viable or technically feasible").
- **Group questions by template section** so the user can address them systematically.
- **Prioritize questions** — mark questions as:
  - **[Critical]**: Blocks the viability determination — the study cannot reach a conclusion without this.
  - **[Important]**: Affects the quality and confidence of the viability assessment.
  - **[Optional]**: Refines the analysis but does not block the viability determination.
- **Reference the source** of the contradiction or gap (e.g., "The stakeholder interview suggests X, but the existing system documentation implies Y").
- **Surface assumptions** — when no evidence exists but a reasonable assumption can be made, propose the assumption and ask the user to confirm, challenge, or refine it.
- **Do not ask questions that can be answered by reading existing documentation** — if the answer exists in a file the skill has already read, use that information directly.
- **Challenge over-optimism** — if stakeholder inputs or existing documents present unrealistically favorable projections without evidence, flag this explicitly and ask for substantiation.

#### Question Template

For each question, use this format:

---

**[Priority] Section X.Y — [Topic]**

[Context: Why this matters for the viability determination and what happens if unanswered]

[The open question]

Suggested answers:
- *Option A*: [description and implications for viability]
- *Option B*: [description and implications for viability]
- *Option C*: [description and implications for viability]
- *Custom*: [your own answer]

---

#### Minimum Required Questions by Project Type

**All project types** must resolve these before the viability determination can be made:

- What is the core problem or opportunity this project addresses? (What happens if we do nothing?)
- What does "success" look like for this project in measurable terms?
- Who are the primary stakeholders and what is their attitude toward this project?
- What is the approximate budget envelope and timeline expectation?
- What is the initial project type classification and what evidence supports it?
- What are the top 3 risks that could make this project non-viable?
- What are the most important alternatives to this project (including "do nothing")?

**Green Field (🟢) additional questions:**
- What evidence exists that there is genuine demand for this product (beyond stakeholder conviction)?
- What is the target market size (TAM/SAM/SOM), and what data supports these figures?
- What constitutes the Minimum Viable Product, and how will market validation occur before full investment?
- Which technology and architecture decisions are already mandated vs. still open for evaluation?
- What is the competitive landscape, and what prevents competitors from replicating this?

**Brown Field (🟤) additional questions:**
- What is the current state of the existing system — its health, test coverage, and technical debt severity?
- What specific capability gaps in the current system create the business problem?
- Is the existing system architecturally capable of supporting the proposed enhancements, or does the debt burden make extension non-viable?
- What backward compatibility constraints apply, and how do they limit the enhancement options?

**Software Modernization (🔵) additional questions:**
- What is the current system's technical debt profile, and what is the cost of maintaining the status quo?
- What is the feature parity target at migration cutover — 100% parity, or is partial parity acceptable?
- What is the migration approach (big bang, phased, parallel run, strangler fig), and what evidence supports its feasibility?
- What is the rollback strategy if the migration fails, and what is the maximum acceptable downtime?
- What are the legacy vendor contract exit costs and timeline constraints?

### Phase 3: Document Generation

Once all critical and important questions are resolved, generate the viability study document.

#### Generation Rules

1. **Use the template structure exactly** — follow `templates/analysis/viability-study.md` section by section.
2. **Replace all `<!-- -->` placeholders** with project-specific content derived from the analysis and user answers.
3. **Mark sections as [APPLICABLE] or [NOT APPLICABLE]** based on the project type classification. For [NOT APPLICABLE] sections, include a one-line rationale (e.g., "[NOT APPLICABLE] — Green Field project with no existing system to assess").
4. **For 🟤🔵 sections**, populate them if the project type matches; otherwise mark [NOT APPLICABLE].
5. **Fill every table** with concrete, specific content — no placeholder values remaining in the final document.
6. **Write the Executive Summary (Section 1) last** — after all other sections are complete, synthesize the key findings and overall viability determination.
7. **Be evidence-based** — every claim in the study should be traceable to a source: existing documentation, stakeholder input, market data, technical analysis, or a clearly labeled assumption.
8. **Be specific, not vague** — write "The current system has 23% test coverage and 47 known unresolved CVEs in dependencies" not "The current system has low test coverage and security issues."
9. **Distinguish facts from assumptions** — when evidence is insufficient, explicitly label content as assumptions and note the risk if the assumption is wrong.
10. **Present balanced analysis** — the viability study must present evidence both for and against proceeding. It is not a business case; it is an honest assessment.
11. **Quantify wherever possible** — use numbers, percentages, timeframes, and monetary values instead of qualitative descriptors alone.
12. **Cross-reference between sections** — when content in one section depends on another, reference it (e.g., "As assessed in Section 3.3, the technical debt severity is 🔴 Critical, which directly impacts the migration feasibility discussed in Section 5.4").
13. **Ensure the SWOT analysis (Section 12) and risk register (Section 11) are aligned** — strengths should mitigate risks; weaknesses should amplify threats; opportunities may counterbalance threats.
14. **Ensure the alternatives analysis (Section 13) includes the "do nothing" baseline** with its own cost trajectory and risk profile.
15. **Make the go/no-go criteria (Section 14.3) measurable** — each criterion must have a threshold, a current value (or "unknown"), and a yes/no assessment.
16. **Save the generated document** to an appropriate location, suggested: `docs/viability-study.md` or `documentation/viability-study.md`.

#### Quality Checks Before Delivery

After generating the document, perform these self-checks:

- [ ] Every section is either populated with project-specific content or marked [NOT APPLICABLE] with rationale.
- [ ] No `<!-- -->` placeholders remain (except the document status and date fields that require human input).
- [ ] The Executive Summary accurately reflects the full document content, including the overall viability determination.
- [ ] The project type classification in Section 2.2 is consistent with how 🟢🟤🔵 sections are handled throughout.
- [ ] The Current System Assessment (Section 3) has sufficient detail for 🟤🔵 projects, or is properly marked [NOT APPLICABLE] for 🟢.
- [ ] The Market & Demand Analysis (Section 4) is based on evidence, not just assertions — demand validation (Section 4.4) includes actual data or clearly labeled assumptions.
- [ ] Technical Feasibility (Section 5) covers both architecture and effort estimation with stated confidence levels.
- [ ] Security & Compliance (Section 6) addresses applicable regulations with their impact on the project.
- [ ] Financial analysis (Section 7) includes both costs and benefits with confidence levels and key assumptions.
- [ ] The Risk Register (Section 11) is internally consistent with the SWOT analysis (Section 12) — no major risk is missing from either.
- [ ] The Alternatives Analysis (Section 13) includes "do nothing" with a realistic cost/risk trajectory.
- [ ] The Go/No-Go Criteria (Section 14.3) are measurable and decision-useful.
- [ ] The overall recommendation (Section 14.1) is supported by the evidence presented in the preceding sections — it does not contradict the findings.
- [ ] Every claim is traceable to a source (document, stakeholder, analysis, or labeled assumption).
- [ ] The document presents balanced evidence — both supporting and challenging the project's viability.
- [ ] No contradictions exist between sections (if they do, flag them explicitly in the document).

### Phase 4: Post-Generation Review

After the document is generated:

1. **Present the document** to the user.
2. **Highlight key judgments made** during generation — where the skill made interpretive calls based on available information, point them out so the user can verify.
3. **Flag remaining uncertainties** — any areas where information was insufficient and reasonable assumptions were made. Indicate the risk each assumption poses to the viability determination.
4. **Present the viability determination** clearly — whether the analysis supports proceeding, proceeding with conditions, or not proceeding, and the key factors driving that conclusion.
5. **Offer to refine** any section the user wants to adjust.
6. **Suggest next steps** — e.g., stakeholder review, business case creation (using `templates/analysis/business-case.md`), proof-of-concept for technical validation, market research for demand validation.

## Examples

### Example Question (Gap — No Demand Validation)

**[Critical] Section 4.4 — Demand Validation**

No demand validation evidence was found — no user interviews, surveys, waitlist data, support tickets, or market research reports. The viability study cannot determine whether there is genuine demand for this solution without some form of validation. A viability study that proceeds without demand evidence risks recommending investment in a solution nobody needs.

What evidence exists that target users or customers actually want this solution, and how can demand be validated?

Suggested answers:
- *Option A*: "We have interview data from 15 prospective users, 12 of whom confirmed the pain point and expressed willingness to adopt. I can provide the interview summaries. This validates demand but the sample is small and may not be representative."
- *Option B*: "We don't have direct user validation yet, but we have 200+ support tickets requesting similar capabilities and internal usage data from a manual workaround that 50 people use daily. This is indirect but substantial evidence of demand."
- *Option C*: "We have no demand validation yet. The viability study should explicitly flag this as a critical gap and recommend that a demand validation exercise (e.g., user interviews, landing page test, prototype demo) be completed before any investment decision is made."
- *Custom*: [your own answer]

### Example Question (Contradiction — Project Type Ambiguity)

**[Critical] Section 2.2 — Project Type Classification**

The project description mentions "building a new platform to replace the legacy system," which could be classified as either Software Modernization (🔵 — replacing a legacy system) or Green Field (🟢 — building from scratch). The classification determines whether the Current System Assessment (Section 3), Data Migration Strategy (Section 5.4), and Legacy Decommission sections apply. Without resolving this, the study structure is ambiguous.

How should this project be classified, given that a new system is being built to replace an existing one?

Suggested answers:
- *Option A*: "Software Modernization (🔵) — the primary purpose is to replace the legacy system. The new system is built from scratch, but the project's viability depends on successful migration, feature parity, and legacy decommission. Sections 3, 5.4, and related 🟤🔵 sections are critical."
- *Option B*: "Green Field (🟢) — while a legacy system exists, the new system shares no code, architecture, or data model with it. The legacy system is simply being retired and replaced; there is no migration path — it's a clean break. The Current System Assessment applies only to understand what capabilities the new system must replicate."
- *Option C*: "Hybrid classification — the project is Green Field in terms of the new system build, but Software Modernization in terms of the transition and decommission. Mark 🟢 sections for the build analysis and 🔵 sections for the transition analysis, and explain the dual classification in Section 2.2."
- *Custom*: [your own answer]

### Example Question (Weak Evidence — Financial Projections)

**[Important] Section 7.2 — Revenue / Benefit Model**

The financial projections provided appear to be based on best-case assumptions without documented methodology. The viability study's financial analysis (Section 7) requires defensible projections with stated confidence levels — optimistic projections without evidence undermine the credibility of the viability determination.

What is the basis for the financial projections, and what confidence level should be assigned?

Suggested answers:
- *Option A*: "The projections are based on comparable projects in our industry — we have data from 3 similar modernization projects with known outcomes. I can provide the benchmark data. Confidence level: Medium — the comparables are close but not identical."
- *Option B*: "The projections are estimates from the product team based on their market experience. No external benchmarking has been done. Confidence level: Low — these should be treated as hypotheses to be validated, not forecasts. The viability study should present a best/expected/worst case range."
- *Option C*: "We have partial data: customer survey data on willingness to pay, and historical conversion rates from a similar product launch. These can be combined for a bottom-up estimate. Confidence level: Medium-Low — the data exists but requires assumptions about conversion and retention."
- *Custom*: [your own answer]

### Example Question (Technical Debt Impact — Brown Field)

**[Important] Section 3.3 — Technical Debt Assessment**

For a Brown Field project, the viability of extending the existing system hinges on the severity and impact of technical debt. No technical debt assessment was found in existing documentation. Without this, the study cannot determine whether extension is viable or whether the debt burden makes a rewrite more cost-effective.

What is the current state of technical debt in the existing system, and how does it impact the feasibility of the proposed enhancements?

Suggested answers:
- *Option A*: "Technical debt is manageable — we have a debt inventory, test coverage above 60%, and the areas needing enhancement have low coupling to the most indebted modules. Extension is viable with targeted refactoring in the enhancement areas."
- *Option B*: "Technical debt is significant — test coverage is below 30%, key modules have cyclomatic complexity above 50, and the areas we need to enhance are tightly coupled to the most fragile parts of the codebase. Extension may cost 2–3x more than estimated due to rework. A rewrite of the affected modules should be evaluated as an alternative."
- *Option C*: "We don't have a formal technical debt assessment. The viability study should recommend that a codebase audit be completed as a prerequisite before the viability determination can be finalized. In the interim, we can use the team's qualitative assessment as a placeholder."
- *Custom*: [your own answer]

### Example Question (Risk Register vs. SWOT Alignment)

**[Optional] Section 11 & 12 — Risk and SWOT Consistency**

The SWOT analysis identifies "dependency on a single cloud vendor" as a threat, but the risk register does not include a corresponding risk item for vendor lock-in or vendor service disruption. These two sections should be cross-referenced to ensure completeness.

Should vendor dependency be added to the risk register, or is the SWOT threat assessment sufficient for this viability study?

Suggested answers:
- *Option A*: "Add it to the risk register as a separate item — the risk register requires likelihood, impact, and mitigation which the SWOT format doesn't provide. This ensures the risk is actionable and tracked."
- *Option B*: "Vendor dependency is acknowledged in the SWOT but is an accepted risk with low likelihood given the vendor's market position. Note it as an accepted risk in the risk register with a low score, and reference the SWOT entry for context."
- *Option C*: "Merge the vendor dependency into an existing risk item about 'infrastructure single points of failure' which already covers vendor, platform, and data center dependencies. Avoid duplicating risks across the two sections."
- *Custom*: [your own answer]

## Anti-Patterns to Avoid

- **Don't generate the document without asking questions** — the viability study's value is in the rigorous investigation and honest assessment, not in filling a template.
- **Don't ask questions that existing documentation already answers** — read carefully first and use available information directly.
- **Don't ask too many questions at once** — batch by priority, lead with critical questions, offer to proceed with assumptions for lower-priority items.
- **Don't produce an advocacy document** — the viability study is not a pitch; it is an honest assessment. If the evidence suggests the project is not viable, say so clearly.
- **Don't present assumptions as facts** — explicitly label assumptions and note their risk to the viability determination.
- **Don't skip the "do nothing" alternative** — the cost and risk trajectory of inaction is the baseline against which all other options must be compared.
- **Don't produce vague risk assessments** — "Technical risk: Medium" is useless. "Data migration of 2.3M records from a legacy system with no documentation and 12 known schema inconsistencies: Likelihood High, Impact Major" is useful.
- **Don't make the go/no-go criteria unmeasurable** — "Team must be ready" is not a criterion. "At least 2 engineers with Kubernetes experience must be hired and onboarded by Q2" is.
- **Don't let the SWOT analysis and risk register contradict each other** — they must be internally consistent.
- **Don't mark sections [NOT APPLICABLE] just because they're hard to populate** — only mark them if they genuinely don't apply to the project type.
- **Don't skip the evidence quality assessment** — the viability study must be transparent about the strength of evidence behind each conclusion.
- **Don't conflate the viability study with a business case** — the viability study determines *whether* to invest; the business case (which follows) determines *how much* and *in what*.

## Document Hierarchy Context

The viability study is the **first** formal analysis document in the project lifecycle. It precedes and informs:

| Document | Relationship | Follows Viability Study? |
|----------|-------------|--------------------------|
| **Business Case** | Uses viability study findings to build the investment case | Yes — the business case elaborates the financial analysis and recommended option |
| **Project Scope** | Translates viability study recommendations into delivery boundaries | Yes — scope is defined after the project is deemed viable |

When generating the viability study, keep in mind that its primary output is a **viability determination** (proceed / proceed with conditions / do not proceed) that enables the decision to invest in the business case phase. The viability study does not need to define scope in detail or produce implementation plans — it needs to determine whether the project is worth investing in further analysis.