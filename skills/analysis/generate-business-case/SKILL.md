---
name: generate-business-case
description: Generates a Business Case for a software project. The skill conducts financial and strategic analysis, evaluates multiple options against measurable criteria, and presents a defensible investment recommendation. The business case  builds on the viability study (if one exists) to answer *"Should we invest, how much, and in which option?"*
---

# Generate Business Case

## Description

Generates a complete, investment-grade Software Project Business Case based on the template `templates/analysis/business-case.md`. The skill conducts rigorous financial and strategic analysis, evaluates multiple options against measurable criteria, and presents a defensible investment recommendation. When gaps, unclear statements, or contradictions are detected, the skill asks targeted open questions with suggested valid answers before proceeding. The business case is the **second** formal analysis document in the project lifecycle — it builds on the viability study (if one exists) to answer *"Should we invest, how much, and in which option?"*

## Activation

When the user requests to create, generate, or draft a business case, investment case, or business justification for a software project.

## Instructions

### Phase 1: Information Gathering & Deep Analysis

1. **Read the template** at `templates/analysis/business-case.md` to understand the full structure, all 17 sections, their expected content, and project-type applicability (🟢 🟤 🔵 ⚪).

2. **Discover and read all existing project information:**
   - Search the workspace for any viability study documents (check `documentation`, `docs`, project folders, or any `.md` files with "viability" in the name). If found, read it thoroughly — the business case builds upon its findings.
   - Search for any pre-existing business case or investment analysis documents.
   - Search for any requirements documents, architecture decision records (ADRs), README files, or project documentation.
   - Search for any configuration files (`package.json`, `pom.xml`, `build.gradle`, `docker-compose.yml`, etc.) that reveal the technology stack and system boundaries.
   - If a codebase exists, explore the directory structure to understand current modules, services, and integrations.
   - Search for any financial data — budget documents, cost reports, vendor pricing, cloud cost estimates, staffing rate cards.
   - Search for any stakeholder communication, meeting notes, decision logs, or executive summaries.
   - Search for any compliance, security, or regulatory documentation.
   - Search for any market research, competitive analysis, or customer data.

3. **Classify the project type** based on available evidence:
   - **Green Field (🟢)**: New product from scratch — business case focus: market opportunity, revenue potential, ground-up costs, time-to-market.
   - **Brown Field (🟤)**: Existing system enhancement — business case focus: incremental value, enhancement vs. replacement costs, feature gap ROI.
   - **Software Modernization (🔵)**: Legacy system migration — business case focus: status quo cost vs. modernization cost, risk reduction, operational efficiency, transition costs.
   - If a viability study exists, verify that its classification is consistent with the evidence. If classification is ambiguous, note this as a question for Phase 2.

4. **Map existing information to template sections.** For each section, determine:
   - **Covered**: Sufficient information exists to populate the section with evidence-based content.
   - **Partially Covered**: Some information exists but is incomplete, lacks financial detail, or needs validation.
   - **Gap**: No information exists for this section.
   - **Contradiction**: Information from different sources conflicts.

5. **Perform deep investment-readiness analysis.** The business case is an investment document — it must be financially rigorous and defensible:

   **Viability study alignment checks** (if a viability study exists):
   - Does the viability study's recommendation align with the options being considered in the business case?
   - Are the viability study's key risks and assumptions reflected in the business case's risk register and sensitivity analysis?
   - Does the business case's recommended option match the viability study's conclusion, and if not, what changed?
   - Are the viability study's evidence gaps now resolved, or are they still open assumptions?

   **Financial rigor checks:**
   - Are cost estimates based on a stated methodology (expert judgment, analogous, parametric, bottom-up) or are they unexplained figures?
   - Do benefits have stated confidence levels and supporting evidence, or are they aspirational targets?
   - Is the "do nothing" option (Option 0) genuinely evaluated with its own cost trajectory, or is it a token baseline?
   - Are sensitivity analysis scenarios realistic and do they cover the variables that most affect NPV?
   - Is the discount rate stated with rationale, or is it an unexplained assumption?
   - Are dual-running costs 🟤🔵 accounted for in the transition period?
   - Are legacy cost retirements 🟤🔵 properly reflected as savings in OpEx projections?
   - Is the contingency percentage justified by the estimation confidence level?

   **Options analysis integrity checks:**
   - Are the options genuinely distinct and viable, or are they variations of the same approach?
   - Is the comparison criteria weighting justified and not biased toward a predetermined outcome?
   - Does each option have a complete cost and benefit profile, or are some options under-specified?
   - Are the financial comparisons (Section 5.3) and risk comparisons (Section 5.4) consistent with the options descriptions (Section 5.1)?
   - Is the recommended option actually the best on weighted criteria, or is there a disconnect?

   **Strategic alignment checks:**
   - Do the stated business objectives (Section 4.1) actually address the problem statement (Section 3.1)?
   - Are success criteria (Section 4.2) measurable and time-bound, or are they vague aspirations?
   - Do KPIs (Section 4.3) have thresholds that enable go/no-go decisions, or are they just tracking metrics?
   - Does the strategic alignment (Section 3.3) connect to real organizational priorities, or is it generic?

   **Accountability checks:**
   - Is there a post-implementation review plan (Section 16) that holds the project accountable for delivering promised benefits?
   - Are benefit realization timelines (Section 7.3) realistic and triggered by identifiable milestones?
   - Is the governance structure (Section 15) specific enough to make decisions, or is it vague about authority?

6. **Build an investment readiness map** — for each section, tag readiness:
   - 🟢 **Investment-Ready**: Data-backed, financially quantified, methodology stated, defensible.
   - 🟡 **Partially Ready**: Some data exists but needs validation, financial quantification, or methodology clarification.
   - 🔴 **Not Ready**: Missing, unquantified, or based on unsupported assertions.

   Sections with 🔴 readiness are priority candidates for Phase 2 questions.

### Phase 2: Clarification Questions

Before generating the document, ask the user targeted questions for every **Partially Covered**, **Gap**, **Contradiction**, or **Not Ready** area identified in Phase 1.

#### Question Design Principles

- **Ask open questions** that invite thoughtful responses — not yes/no questions.
- **Always suggest 2–3 possible valid answers** for each question to help the user think through the options and demonstrate understanding of the domain.
- **Contextualize each question** — briefly explain why the information matters for the investment decision and what happens if it remains unanswered (e.g., "Without this, the business case cannot present a defensible NPV to the investment committee").
- **Group questions by template section** so the user can address them systematically.
- **Prioritize questions** — mark questions as:
  - **[Critical]**: Blocks the investment recommendation — the business case cannot reach a conclusion without this.
  - **[Important]**: Affects the credibility and confidence of the investment case.
  - **[Optional]**: Refines the analysis but does not block the recommendation.
- **Reference the source** of the contradiction or gap (e.g., "The viability study estimates 18 months, but the proposed budget implies a 12-month timeline").
- **Challenge financial optimism** — if benefit estimates seem inflated, cost estimates seem understated, or sensitivity scenarios are too narrow, flag this explicitly and ask for substantiation.
- **Do not ask questions that can be answered by reading existing documentation** — use available information directly.
- **Distinguish between information that must be resolved now vs. information that can be documented as assumptions with validation plans.**

#### Question Template

For each question, use this format:

---

**[Priority] Section X.Y — [Topic]**

[Context: Why this matters for the investment decision and what happens if unanswered]

[The open question]

Suggested answers:
- *Option A*: [description and implications for the business case]
- *Option B*: [description and implications for the business case]
- *Option C*: [description and implications for the business case]
- *Custom*: [your own answer]

---

#### Minimum Required Questions by Project Type

**All project types** must resolve these before the investment recommendation can be made:

- What is the total investment envelope being considered, and who has approval authority?
- What is the discount rate / hurdle rate the organization uses for investment decisions?
- What are the 2–3 distinct options being considered (including "do nothing")?
- What is the analysis period for financial modeling (typically 3 or 5 years)?
- What are the top 3 financial assumptions that most affect the NPV?
- What is the approximate expected timeline and how does it map to budget cycles?
- What happens if this investment is not made — what is the cost trajectory of inaction?

**Green Field (🟢) additional questions:**
- What is the revenue model and what are the projected revenue figures for the first 3–5 years?
- What is the target market size (TAM/SAM/SOM) and what data supports these figures?
- How will demand be validated before full investment commitment — is there a phased funding approach?
- What are the competitive threats and how do they affect the financial projections?
- What constitutes the Minimum Viable Product, and how does it reduce initial investment risk?

**Brown Field (🟤) additional questions:**
- What is the current system's operating cost (the baseline that enhancements must improve upon)?
- What specific capability gaps are creating quantifiable business loss or cost?
- What would it cost to simply maintain the current system for the next 3–5 years (Option 0 trajectory)?
- Are there backward compatibility requirements that constrain the enhancement options or increase cost?

**Software Modernization (🔵) additional questions:**
- What is the current annual cost of maintaining the legacy system (including incident costs, workarounds, and opportunity cost)?
- What are the legacy vendor contract exit costs and timeline constraints?
- What is the dual-running cost during the transition period?
- What are the legacy system savings (negative OpEx) once decommission is complete?
- What is the maximum acceptable migration downtime, and how does it constrain the transition approach?

### Phase 3: Document Generation

Once all critical and important questions are resolved, generate the business case document.

#### Generation Rules

1. **Use the template structure exactly** — follow `templates/analysis/business-case.md` section by section.
2. **Replace all `<!-- -->` placeholders** with project-specific content derived from the analysis and user answers.
3. **Mark sections as [APPLICABLE] or [NOT APPLICABLE]** based on the project type classification. For [NOT APPLICABLE] sections, include a one-line rationale.
4. **For 🟤🔵 sections**, populate them if the project type matches; otherwise mark [NOT APPLICABLE].
5. **Fill every table** with concrete, specific content — no placeholder values remaining in the final document.
6. **Write the Executive Summary (Section 1) last** — after all other sections are complete, synthesize the investment recommendation.
7. **Be financially rigorous** — every cost and benefit figure must have a stated confidence level, methodology, and key assumptions. Unsupported figures undermine the business case's credibility.
8. **Be specific, not vague** — write "NPV of €340K at 8% discount rate over 5 years, with payback in 2.4 years" not "The project has a positive NPV and reasonable payback."
9. **Build on the viability study** — if one exists, reference its findings, adopt its classification, and elaborate its recommendations into specific investment options. Do not repeat its analysis — the business case adds financial rigor and option selection.
10. **Include "do nothing" as a real option** — Option 0 must have its own cost trajectory, risk profile, and financial impact. It is the baseline against which all other options are measured.
11. **Present balanced options** — each option must have genuine strengths and weaknesses. The comparison must not be engineered to favor a predetermined outcome.
12. **Quantify benefits with confidence levels** — every tangible benefit must have an estimated annual value, a confidence level (High/Medium/Low), the assumption it rests on, and the evidence supporting it.
13. **Include dis-benefits** (Section 7.4) honestly — every investment has negative consequences; acknowledging them builds credibility.
14. **Make sensitivity analysis comprehensive** (Section 9.6) — test the variables that most affect NPV: cost overrun, benefit delay, lower adoption, higher discount rate, extended timeline. Include break-even analysis.
15. **Make the risk register financially-aware** (Section 10.1) — each risk should have a financial impact estimate if it materializes, not just a qualitative score.
16. **Define measurable go/no-go criteria** at each stage gate (Section 15.2) — each gate must have specific, measurable pass/fail criteria.
17. **Include a post-implementation review plan** (Section 16) — this holds the project accountable for delivering promised benefits and is essential for investment credibility.
18. **Cross-reference between sections** — benefits in Section 7 must align with cash flows in Section 9.1, options in Section 5 must match the financial comparison in Section 5.3, and risks in Section 10 must be reflected in sensitivity scenarios in Section 9.6.
19. **Save the generated document** to an appropriate location, suggested: `docs/business-case.md` or `documentation/business-case.md`.

#### Quality Checks Before Delivery

After generating the document, perform these self-checks:

- [ ] Every section is either populated with project-specific content or marked [NOT APPLICABLE] with rationale.
- [ ] No `<!-- -->` placeholders remain (except the document status and date fields that require human input).
- [ ] The Executive Summary accurately reflects the full document, including the investment recommendation, total investment, expected return, and top risks.
- [ ] The project type classification in Section 2.2 is consistent with how 🟢🟤🔵 sections are handled throughout.
- [ ] Option 0 ("Do Nothing") is genuinely evaluated with its own cost trajectory and risk profile — not a token baseline.
- [ ] At least 2 investable options are compared in addition to "do nothing."
- [ ] The options comparison (Section 5.2) uses weighted criteria with justified weights.
- [ ] The financial comparison (Section 5.3) includes NPV, IRR, payback, and BCR for each investable option.
- [ ] The recommended option (Section 6) is the one that scores best on the weighted criteria AND the financial comparison — if not, the discrepancy is explained.
- [ ] Every tangible benefit (Section 7.1) has an annual value, confidence level, assumption, and evidence source.
- [ ] Dis-benefits (Section 7.4) are acknowledged with mitigation.
- [ ] Cost estimates (Section 8) state the estimation methodology and confidence level.
- [ ] The financial analysis (Section 9) includes: cash flow projection, NPV, IRR, payback period, BCR, and sensitivity analysis with at least 4 scenarios.
- [ ] The sensitivity analysis identifies the break-even point and the variables that most affect NPV.
- [ ] The risk register (Section 10) includes financial impact estimates for each risk.
- [ ] The risk appetite and tolerances (Section 10.3) define specific thresholds.
- [ ] The implementation plan (Section 11) includes delivery phases, milestones, and go/no-go gates.
- [ ] The transition strategy (Section 11.4) is populated for 🟤🔵 projects.
- [ ] The governance structure (Section 15) defines specific decision-makers with authority levels.
- [ ] The post-implementation review plan (Section 16) includes benefit realization tracking and a review schedule.
- [ ] Benefits in Section 7 align with cash flows in Section 9.1 — no orphaned or contradictory figures.
- [ ] If a viability study exists, its key findings are referenced and built upon, not duplicated.
- [ ] The document is internally consistent — no contradictions between sections.

### Phase 4: Post-Generation Review

After the document is generated:

1. **Present the document** to the user.
2. **Highlight key judgments made** during generation — where the skill made interpretive calls (e.g., choosing a discount rate, weighting criteria), point them out so the user can verify.
3. **Present the financial summary** clearly — NPV, IRR, payback, BCR, and the overall financial verdict.
4. **Flag remaining financial uncertainties** — areas where assumptions were necessary and which variables most affect the investment case. Identify these as priorities for validation.
5. **Highlight the recommended option** and its key trade-offs — make sure the user understands what was accepted and what was given up.
6. **Offer to refine** any section the user wants to adjust.
7. **Suggest next steps** — e.g., stakeholder review, investment committee presentation, project scope creation (using `templates/analysis/project-scope.md`), financial model validation, procurement for quoted pricing.

## Examples

### Example Question (Gap — No "Do Nothing" Cost Trajectory)

**[Critical] Section 5.1 — Option 0: Do Nothing Baseline**

No cost trajectory for the "do nothing" option was found. Option 0 is the baseline against which all other options are measured — without it, the business case cannot demonstrate that any investment creates more value than inaction. For 🟤🔵 projects, the "do nothing" trajectory typically shows increasing maintenance costs, rising risk, and degrading performance.

What is the cost and risk trajectory if no investment is made over the next 3–5 years?

Suggested answers:
- *Option A*: "The current system's annual maintenance cost is €120K and rising 12% YoY due to increasing vendor fees and incident remediation. By Year 5, annual cost reaches €190K with no new capabilities. Cumulative 5-year cost of inaction: ~€760K. Additionally, the platform reaches end-of-support in Year 3, creating a compliance risk."
- *Option B*: "The current system is stable but stagnant — maintenance cost is flat at ~€80K/year. The cost of inaction is primarily opportunity cost: we estimate €200K/year in unrealized revenue from capabilities the current system cannot deliver. Cumulative 5-year opportunity cost: ~€1M."
- *Option C*: "We don't have a detailed cost trajectory but we know: (1) the current system costs €X/year to operate, (2) two critical dependencies reach end-of-life within 3 years, and (3) each major incident costs ~€Y to resolve with increasing frequency. The business case should model this with stated assumptions."
- *Custom*: [your own answer]

### Example Question (Weak Financial Rigor — Unsupported Benefits)

**[Critical] Section 7.1 — Tangible Benefits**

The benefit estimates provided appear to be aspirational targets without stated confidence levels, supporting evidence, or the assumptions they rest on. The investment committee requires each benefit to be traceable to a source and accompanied by a confidence level. Unsupported benefit estimates are a common reason for business case rejection.

What is the evidence and confidence level for the major benefit claims?

Suggested answers:
- *Option A*: "The €500K/year cost reduction is based on eliminating 4 FTEs who currently perform manual data reconciliation — confirmed by department head and supported by timesheet data. Confidence: High. The €200K/year revenue increase assumes 10% conversion from a waitlist of 500 contacts — this is unvalidated. Confidence: Low. The business case should present these with different confidence levels."
- *Option B*: "Benefits are estimated from a comparable modernization project completed 18 months ago in a sister department — that project achieved €380K/year in savings against a projection of €450K (84% realization). We can use that realization rate to adjust our projections. Confidence: Medium — comparables exist but contexts differ."
- *Option C*: "We have no direct evidence for the benefit figures — they are best-case estimates. The business case should clearly label them as such, include a sensitivity analysis that tests 50%, 70%, and 100% realization rates, and make the investment recommendation conditional on achieving at least the 70% scenario."
- *Custom*: [your own answer]

### Example Question (Contradiction — Options vs. Recommendation)

**[Important] Section 5 & 6 — Options Analysis vs. Recommendation**

The viability study recommended a "phased re-architecture" approach, but the options currently under consideration seem to only include "full rebuild" and "buy SaaS." If the viability study's recommended approach is not one of the options, the business case should explain why it was excluded or add it as an option.

Which options should the business case evaluate, and how do they relate to the viability study's recommendation?

Suggested answers:
- *Option A*: "Add the viability study's recommended option (phased re-architecture) as Option 1. Include the full rebuild as Option 2 and the SaaS replacement as Option 3. The 'do nothing' baseline is Option 0. This ensures the business case evaluates all viable paths including the one the viability study endorsed."
- *Option B*: "The phased re-architecture was recommended in the viability study, but subsequent financial analysis showed its TCO exceeds the full rebuild by 15% due to extended dual-running costs. The business case should include it as an option but document why it was not recommended — this shows thoroughness and addresses the viability study's conclusion."
- *Option C*: "The viability study's recommendation has been superseded by new information: a vendor now offers a SaaS solution that covers 85% of requirements at 40% lower TCO. The business case should include the SaaS option and explain how the landscape changed since the viability study."
- *Custom*: [your own answer]

### Example Question (Missing Sensitivity — Discount Rate)

**[Important] Section 9.6 — Sensitivity Analysis**

The discount rate used for NPV calculations has not been specified. The discount rate materially affects whether the project appears financially attractive — a rate too low inflates NPV; a rate too high deflates it. Investment committees typically require a stated rate with rationale and a sensitivity test at +/- 2–3%.

What discount rate should be used, and what is the organization's standard hurdle rate?

Suggested answers:
- *Option A*: "The organization's standard hurdle rate is 8% (weighted average cost of capital). Use 8% as the expected case, and test sensitivity at 6% and 11% in the sensitivity analysis. The rationale for 8% is: it reflects our corporate cost of capital plus a 2% risk premium for technology projects."
- *Option B*: "The organization uses different rates by project risk: 6% for low-risk incremental improvements, 10% for standard technology projects, and 15% for innovative/green-field ventures. This project should use [X]% because [rationale]. The sensitivity analysis should test at +/- 3%."
- *Option C*: "We don't have a formal hurdle rate. The business case should use the current cost of capital (~5%) as a minimum and include scenarios at 5%, 8%, and 12% to show how the investment case holds across different rate assumptions. Recommend that the finance team define an official rate."
- *Custom*: [your own answer]

### Example Question (Brown Field — Enhancement vs. Replace Decision)

**[Important] Section 5.1 — Options for Brown Field Project**

For a Brown Field project, the fundamental question is whether to enhance the existing system or replace it. No analysis was found comparing the cost of incremental enhancement against the cost of replacement. The business case must present both as credible options with their own cost-benefit profiles.

Should the business case evaluate "enhance existing" and "replace with new" as separate options, and what data supports each?

Suggested answers:
- *Option A*: "Yes — present two options: (1) Enhance the existing system with targeted refactoring and new modules, estimated at €X with 18-month delivery; (2) Replace with a new build on modern architecture, estimated at €Y with 24-month delivery. The viability study's tech debt assessment (Section 3.3) shows moderate debt, making both options viable. The comparison should weigh time-to-value (advantage: enhance) against long-term flexibility (advantage: replace)."
- *Option B*: "The existing system's tech debt makes enhancement non-viable — the viability study rated debt as 🔴 Critical with test coverage at 18% and key modules at cyclomatic complexity >60. Enhancement would cost 2–3x the nominal estimate due to rework. The business case should include enhancement as an option but document why it scores poorly, demonstrating that replacement was evaluated fairly."
- *Option C*: "We need a technical assessment to determine whether enhancement is viable. The business case should include both options with the enhancement estimate flagged as 'Low Confidence — pending codebase audit.' This makes the audit a prerequisite for finalizing the investment decision."
- *Custom*: [your own answer]

## Anti-Patterns to Avoid

- **Don't generate the document without asking questions** — the business case's value is in financial rigor and honest option comparison, not template filling.
- **Don't ask questions that existing documentation already answers** — read carefully and use available information directly.
- **Don't ask too many questions at once** — batch by priority, lead with critical questions, offer to proceed with assumptions for lower-priority items.
- **Don't produce an advocacy document** — the business case is an investment analysis, not a sales pitch. If Option 2 is better than Option 1, say so. If the numbers don't support investment, recommend rejection.
- **Don't present benefits without confidence levels** — every benefit figure needs a confidence level and the assumption it rests on.
- **Don't treat "do nothing" as a token option** — it must have a genuine cost trajectory, risk profile, and financial impact. It is the baseline for all comparisons.
- **Don't engineer the options comparison to favor a predetermined outcome** — if the weights or scores look suspicious, recalibrate.
- **Don't skip sensitivity analysis** — a business case without sensitivity analysis is indefensible. The investment committee will ask "what if costs overrun by 20%?"
- **Don't conflate the business case with the viability study** — the viability study determines *whether* to invest; the business case determines *how much* and *in which option*. Build on the viability study; don't duplicate it.
- **Don't produce vague success criteria** — "Improve customer satisfaction" is not a success criterion. "Increase NPS from 32 to 55 within 12 months of go-live" is.
- **Don't skip the post-implementation review plan** — it is the accountability mechanism that makes the investment case credible.
- **Don't omit dis-benefits** — every investment has negative consequences. Acknowledging them builds credibility; hiding them destroys it.
- **Don't make financial claims you can't trace** — every figure in the cash flow projection must trace to a cost estimate (Section 8) or a benefit estimate (Section 7).

## Document Hierarchy Context

The business case is the **second** formal analysis document in the project lifecycle. It follows and builds upon:

| Document | Relationship | Precedes Business Case? |
|----------|-------------|------------------------|
| **Viability Study** | Determines whether the project is feasible and worth pursuing; the business case elaborates the financial case for the viable options | Yes — the business case should reference and build on the viability study's findings |

And it precedes:

| Document | Relationship | Follows Business Case? |
|----------|-------------|------------------------|
| **Project Scope** | Translates the approved business case option into concrete delivery boundaries | Yes — scope is defined after the investment is approved |

When generating the business case, keep in mind that its primary output is an **investment recommendation** (approve / approve with conditions / reject) with a specific option selected, total investment quantified, and financial return projected. The business case enables the budget holder or investment committee to make an informed funding decision.