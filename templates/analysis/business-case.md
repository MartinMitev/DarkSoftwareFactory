# Software Project Business Case

> **Template Version:** 1.0  
> **Last Updated:** <!-- date -->  
> **Document Status:** <!-- Draft | Under Review | Approved -->

---

## Metadata

| Field                | Value |
|----------------------|-------|
| **Project Name**     | <!-- project name --> |
| **Project Type**     | <!-- Green Field | Brown Field | Software Modernization --> |
| **Sponsor**          | <!-- sponsoring stakeholder or department --> |
| **Product Owner**    | <!-- product owner name --> |
| **Technical Lead**   | <!-- technical lead name --> |
| **Author(s)**        | <!-- author name(s) --> |
| **Reviewer(s)**      | <!-- reviewer name(s) --> |
| **Date Created**     | <!-- creation date --> |
| **Date Revised**     | <!-- revision date --> |
| **Classification**   | <!-- Public | Internal | Confidential --> |
| **Budget Authority** | <!-- name or committee with approval power --> |
| **Investment Category** | <!-- Capital Expenditure | Operational Expenditure | Mixed --> |

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Introduction](#2-introduction)
3. [Business Problem & Opportunity](#3-business-problem--opportunity)
4. [Objectives & Success Criteria](#4-objectives--success-criteria)
5. [Options Analysis](#5-options-analysis)
6. [Recommended Option](#6-recommended-option)
7. [Benefits & Value Proposition](#7-benefits--value-proposition)
8. [Cost Estimate](#8-cost-estimate)
9. [Financial Analysis](#9-financial-analysis)
10. [Risk Assessment](#10-risk-assessment)
11. [Implementation Plan](#11-implementation-plan)
12. [Resource Requirements](#12-resource-requirements)
13. [Stakeholder Engagement](#13-stakeholder-engagement)
14. [Dependencies & Assumptions](#14-dependencies--assumptions)
15. [Governance & Approval](#15-governance--approval)
16. [Post-Implementation Review Plan](#16-post-implementation-review-plan)
17. [Appendices](#17-appendices)

---

## 1. Executive Summary

<!-- 
Provide a concise, high-level overview of the entire business case. Write this section last, after all analysis is complete.

Expected content:
- A clear statement of the business problem or opportunity being addressed (2–3 sentences).
- The recommended option and a brief justification for why it was selected over alternatives.
- The total investment required and the expected financial return (NPV, payback period).
- A summary of the top risks and how they will be mitigated.
- The overall investment recommendation (approve / approve with conditions / reject).
- Key dependencies or prerequisites for the investment to deliver its promised value.

Keep this section to 1 page maximum. It must stand alone as a readable summary for decision-makers who may not read the full document.
-->

| Field | Summary |
|-------|---------|
| **Business Problem / Opportunity** | <!-- 2–3 sentence description --> |
| **Recommended Option** | <!-- which option and why in 1–2 sentences --> |
| **Total Investment** | <!-- total cost over project lifecycle --> |
| **Expected Return** | <!-- NPV, payback period, IRR --> |
| **Top Risks** | <!-- 2–3 highest-impact risks --> |
| **Investment Recommendation** | <!-- Approve / Approve with Conditions / Reject --> |
| **Key Dependencies** | <!-- prerequisites for value realization --> |

---

## 2. Introduction

### 2.1 Purpose

<!--
State the purpose of this business case and the investment decision it supports.

Expected content:
- The specific business problem or opportunity the project addresses.
- Why a business case is being created (e.g., budget approval, steering committee decision, investment committee review).
- The intended audience for this document (e.g., executive board, CFO, investment committee, steering committee).
- What decision this document enables (e.g., approve funding, authorize procurement, proceed to delivery).
- The relationship to any preceding viability study or feasibility analysis.
-->

### 2.2 Project Type Classification

<!--
Classify the project and explain the implications for the business case.

**Green Field** — Building a new software product or system from scratch with no existing codebase or legacy constraints.
Business case focus: market opportunity validation, ground-up cost estimation, revenue potential, competitive positioning, time-to-market advantage.

**Brown Field** — Extending, refactoring, or significantly enhancing an existing software system while maintaining backward compatibility and operational continuity.
Business case focus: incremental value over current system, enhancement cost vs. replacement cost, user base retention, feature gap closure ROI.

**Software Modernization** — Re-architecting, re-platforming, or migrating a legacy system to modern technologies, architectures, or cloud platforms.
Business case focus: cost of maintaining status quo vs. modernization cost, risk reduction from legacy dependencies, operational efficiency gains, migration transition costs.

Mark sections in this template as [APPLICABLE] or [NOT APPLICABLE] based on the project type. Sections marked with icons indicate particular relevance:
- 🟢 = Primarily relevant for Green Field projects
- 🟤 = Primarily relevant for Brown Field projects
- 🔵 = Primarily relevant for Software Modernization projects
- ⚪ = Relevant for all project types
-->

| Attribute | Value |
|-----------|-------|
| **Project Type** | <!-- Green Field / Brown Field / Software Modernization --> |
| **Rationale for Classification** | <!-- why this classification applies --> |
| **Key Implications for Business Case** | <!-- what this means for the financial and strategic analysis --> |

### 2.3 Scope

<!--
Define the boundaries of the investment—what is included and explicitly excluded.

Expected content:
- The software product, service, or system being invested in.
- Which modules, components, services, or phases are in scope.
- Geographic, temporal, or organizational boundaries.
- Assumptions that limit the business case (e.g., "This business case assumes current pricing models remain stable for 3 years").
- What is explicitly out of scope (e.g., downstream system changes, organizational restructuring, future phases not yet approved).
- How scope relates to any preceding viability study.
-->

| In Scope | Out of Scope |
|----------|--------------|
| <!-- item --> | <!-- item --> |

### 2.4 Definitions & Abbreviations

<!--
List terms, acronyms, or abbreviations used throughout the document.

Expected content:
- A table of term/abbreviation and its definition.
- Include financial terms (e.g., NPV, IRR, BCR, CapEx, OpEx, TCO, ROI, SROI).
- Include software-specific terms (e.g., CI/CD, SaaS, SLA, SLO, MTTR, MTBF).
- Include project management terms (e.g., EAC, ETC, SPI, CPI, WBS).
-->

| Term / Abbreviation | Definition |
|---------------------|------------|
|                     |            |

### 2.5 References

<!--
List external documents, standards, prior analyses, or data sources referenced.

Expected content:
- Document title, version/date, and location/URL.
- Include the viability study if one was produced.
- Include architectural decision records, market research, financial policies, procurement guidelines.
- Include any regulatory references or compliance frameworks that shaped the case.
-->

| Reference | Description | Location |
|-----------|-------------|----------|
|           |             |          |

---

## 3. Business Problem & Opportunity

### 3.1 Problem Statement ⚪

<!--
Clearly articulate the business problem being solved or the opportunity being seized.

Expected content:
- A precise description of the current pain point, unmet need, or strategic opportunity.
- Quantification of the problem where possible (e.g., revenue lost, costs incurred, hours wasted, incidents per month).
- The business impact of not addressing the problem (cost of inaction, worsening trend).
- Who is affected (customers, employees, partners, operations).
- How the problem was identified (support data, customer feedback, competitive analysis, strategic planning).
- Timeline urgency: why now and what happens if we wait.
-->

| Dimension | Description |
|-----------|-------------|
| **Problem / Opportunity** | <!-- describe the problem or opportunity --> |
| **Quantified Impact** | <!-- numbers, metrics, financial impact --> |
| **Affected Parties** | <!-- who is impacted --> |
| **Source of Evidence** | <!-- how was this identified --> |
| **Urgency / "Why Now"** | <!-- what makes this time-sensitive --> |
| **Cost of Inaction** | <!-- what happens if we do nothing --> |

### 3.2 Current State Assessment 🟤🔵

<!--
Describe the current situation for Brown Field and Modernization projects.

Expected content:
- 🟤 Current system capabilities and the specific gaps that create the business problem.
- 🟤 Limitations that prevent the existing system from meeting current or future demand.
- 🔵 Legacy system risks: increasing maintenance cost, shrinking talent pool, vendor lock-in, compliance gaps, performance degradation.
- 🔵 Technical debt cost quantification: hours/month lost to workarounds, incident costs, delayed feature delivery.
- 🔵 End-of-life timelines for critical platform components or vendor contracts.
- Quantified baseline metrics that the project will improve upon.
-->

| Current State Metric | Value | Trend | Target After Project |
|-----------------------|-------|-------|----------------------|
| <!-- e.g., Monthly maintenance cost --> | <!-- e.g., €50K --> | <!-- e.g., ↑ 12% YoY --> | <!-- e.g., €15K --> |
| <!-- e.g., Mean time to recovery --> | <!-- e.g., 4 hours --> | <!-- e.g., ↑ 20% YoY --> | <!-- e.g., 30 min --> |

### 3.3 Strategic Alignment ⚪

<!--
Explain how the project aligns with organizational strategy and priorities.

Expected content:
- Alignment with the organization's strategic objectives, mission, or vision.
- Alignment with specific strategic initiatives or OKRs.
- How the project supports digital transformation, cloud-first, or technology modernization strategies.
- How the project enables future strategic capabilities (platform plays, ecosystem enablement).
- Links to existing business or technology roadmaps.
-->

| Strategic Objective | How This Project Contributes | Priority |
|---------------------|------------------------------|----------|
|                     |                              |          |

### 3.4 Market & Competitive Context 🟢

<!--
Describe the market conditions that make this project strategically important.

Expected content:
- Market size, growth rate, and trends relevant to the project.
- Competitive threats or first-mover advantages.
- Customer expectations or industry standards that demand action.
- Technology trends that create opportunity or risk of obsolescence.
- Regulatory or compliance drivers that create urgency.
-->

---

## 4. Objectives & Success Criteria

### 4.1 Business Objectives ⚪

<!--
Define what the project must achieve from a business perspective.

Expected content:
- Clear, measurable business objectives (use SMART criteria: Specific, Measurable, Achievable, Relevant, Time-bound).
- Objectives should directly address the problem statement from Section 3.1.
- Distinguish between primary objectives (must achieve) and secondary objectives (nice to have).
- Timeframe for each objective (short-term, medium-term, long-term).
- How each objective links to strategic priorities from Section 3.3.
-->

| # | Business Objective | SMART Measure | Timeframe | Priority | Linked Strategy |
|---|-------------------|---------------|-----------|----------|-----------------|
|   |                   |               |           |          |                 |

### 4.2 Success Criteria ⚪

<!--
Define the specific, measurable criteria that will determine project success.

Expected content:
- Quantitative success criteria tied to business objectives (e.g., reduce processing time by 60%, achieve 99.9% availability, reduce support tickets by 40%).
- Qualitative success criteria (e.g., improved user satisfaction, reduced cognitive load for operators).
- Financial success criteria (e.g., achieve positive NPV within 3 years, reduce OpEx by €X/year).
- Technical success criteria (e.g., achieve <200ms p99 latency, migrate 100% of data with zero loss).
- 🟤🔵: Success criteria for migration/transition (e.g., zero-downtime cutover, feature parity ≥95% at launch).
- Timeline for measuring success (e.g., 6 months post-launch, 12 months post-migration).
-->

| # | Success Criterion | Measure | Baseline | Target | Measurement Method | When Measured |
|---|-------------------|---------|----------|--------|-------------------|---------------|
|   |                   |         |          |        |                   |               |

### 4.3 Key Performance Indicators (KPIs) ⚪

<!--
Define the KPIs that will be tracked to monitor value delivery.

Expected content:
- Leading indicators (predict future performance, e.g., user adoption rate, feature velocity).
- Lagging indicators (confirm achieved outcomes, e.g., cost savings, revenue, incident reduction).
- How each KPI relates to a business objective or success criterion.
- Data source for each KPI and measurement frequency.
- Thresholds: green (on track) / amber (at risk) / red (off track).
-->

| KPI | Type | Related Objective | Target | Data Source | Frequency | Green / Amber / Red Thresholds |
|-----|------|-------------------|--------|-------------|-----------|-------------------------------|
|     |      |                   |        |             |           |                               |

---

## 5. Options Analysis

### 5.1 Identified Options ⚪

<!--
List and describe the distinct options considered for addressing the business problem.

Expected content:
- **Option 0: Do Nothing** — The baseline of maintaining the status quo. Always include this as the reference case. Describe the cost and risk trajectory of inaction.
- **Option 1** — The primary proposed option (e.g., build a new system, extend the current system, modernize the platform).
- **Option 2** — A credible alternative (e.g., buy a COTS/SaaS solution, adopt an open-source platform, take a different architectural approach).
- **Option 3** (optional) — An additional alternative if relevant (e.g., partial implementation, phased approach, hybrid approach).
- Each option should be a complete, viable path that fully or partially addresses the problem.
- 🟢 Green Field options: build vs. buy vs. open-source adopt/customize vs. partner.
- 🟤 Brown Field options: incremental refactoring vs. partial rewrite vs. wrap-and-extend vs. replace.
- 🔵 Modernization options: re-host (lift & shift) vs. re-platform vs. re-architect vs. rebuild vs. replace with COTS/SaaS.
-->

| # | Option Name | Description | Key Characteristics |
|---|-------------|-------------|---------------------|
| 0 | Do Nothing | <!-- describe status quo trajectory --> | <!-- no investment, declining/increasing costs --> |
| 1 | <!-- name --> | <!-- describe --> | <!-- key features --> |
| 2 | <!-- name --> | <!-- describe --> | <!-- key features --> |
| 3 | <!-- name --> | <!-- describe --> | <!-- key features --> |

### 5.2 Options Comparison ⚪

<!--
Compare all options against key evaluation criteria.

Expected content:
- Define evaluation criteria (e.g., total cost, time to value, risk level, strategic fit, scalability, team readiness, vendor lock-in, compliance fit).
- Assign weights to each criterion based on organizational priorities.
- Score each option (1–5 scale, where 5 = best).
- Calculate weighted scores for each option.
- Provide a brief narrative justification for each score.
- Include both quantitative and qualitative assessment.
-->

| Criterion | Weight | Option 0: Do Nothing | Option 1 | Option 2 | Option 3 |
|-----------|--------|----------------------|----------|----------|----------|
| Total Cost of Ownership | | | | | |
| Time to Value | | | | | |
| Risk Level | | | | | |
| Strategic Fit | | | | | |
| Scalability & Flexibility | | | | | |
| Team Readiness | | | | | |
| Compliance Fit | | | | | |
| Vendor Lock-in Risk | | | | | |
| **Weighted Total** | | | | | |

### 5.3 Financial Comparison ⚪

<!--
Compare the financial profiles of each option.

Expected content:
- Total cost of ownership over the analysis period (typically 3–5 years) for each option.
- NPV, IRR, and payback period for each investable option.
- Cost-benefit ratio for each option.
- Sensitivity of each option to key assumptions (e.g., what if costs overrun by 20%, what if benefits are delayed by 6 months).
- 🟤🔵: Include the cost of continuing with the current system as the Option 0 baseline.
-->

| Financial Metric | Option 0: Do Nothing | Option 1 | Option 2 | Option 3 |
|------------------|---------------------|----------|----------|----------|
| Total Cost (3–5 yr) | | | | |
| NPV | — | | | |
| IRR | — | | | |
| Payback Period | — | | | |
| Benefit-Cost Ratio | — | | | |
| Sensitivity (Cost +20%) | | | | | |
| Sensitivity (Benefits delayed 6mo) | | | | | |

### 5.4 Risk Comparison ⚪

<!--
Compare the risk profiles of each option.

Expected content:
- Key risks specific to each option.
- Overall risk rating for each option (Low / Medium / High).
- Risk mitigation cost for each option.
- Residual risk after mitigation for each option.
- 🟤🔵: Migration-specific risks (data loss, downtime, feature regression) per option.
-->

| Risk Dimension | Option 0: Do Nothing | Option 1 | Option 2 | Option 3 |
|---------------|---------------------|----------|----------|----------|
| Overall Risk Rating | | | | |
| Technical Risk | | | | |
| Financial Risk | | | | |
| Operational Risk | | | | |
| Compliance Risk | | | | |
| Migration Risk 🟤🔵 | — | | | |
| Risk Mitigation Cost | | | | |
| Residual Risk | | | | |

---

## 6. Recommended Option

### 6.1 Recommendation ⚪

<!--
State the recommended option and the rationale for selecting it.

Expected content:
- Clear identification of the recommended option (by number and name).
- The primary reasons for selection (which criteria drove the decision).
- Why the recommended option is superior to the alternatives on the most important criteria.
- Acknowledgment of the trade-offs accepted (what the recommended option gives up vs. alternatives).
- How the recommendation addresses the business problem from Section 3.1.
- How the recommendation satisfies the objectives from Section 4.1.
-->

### 6.2 Conditions & Prerequisites ⚪

<!--
State the conditions that must be met for the recommended option to deliver its expected value.

Expected content:
- Technical prerequisites (e.g., infrastructure provisioned, team hired, PoC validated, API contracts finalized).
- Organizational prerequisites (e.g., stakeholder alignment, governance established, training completed).
- Financial prerequisites (e.g., budget approval, funding phasing agreed).
- 🟤🔵: Migration prerequisites (e.g., data migration tooling ready, rollback tested, feature parity checklist signed off).
- Timeline for meeting each prerequisite.
- Which prerequisites are critical path (must be met before project start) vs. can be met during execution.
-->

| # | Prerequisite / Condition | Type | Critical Path? | Target Date | Owner |
|---|-------------------------|------|----------------|-------------|-------|
|   |                         |      |                |             |       |

### 6.3 Trade-offs & Accepted Risks ⚪

<!--
Explicitly state the trade-offs and risks accepted with the recommended option.

Expected content:
- What the recommended option does NOT deliver that alternatives would have.
- Known risks that are accepted without full mitigation (with rationale).
- Constraints that limit the option's effectiveness.
- Why the trade-offs are acceptable given the overall value proposition.
-->

| Trade-off / Accepted Risk | Impact | Rationale for Acceptance |
|---------------------------|--------|--------------------------|
|                           |        |                          |

---

## 7. Benefits & Value Proposition

### 7.1 Tangible Benefits ⚪

<!--
Quantify the direct, measurable financial benefits the project will deliver.

Expected content:
- Cost reductions (e.g., reduced infrastructure costs, lower licensing fees, fewer support incidents, reduced manual effort).
- Revenue increases (e.g., new revenue streams, improved conversion, expanded market reach).
- Productivity gains (e.g., faster delivery cycles, reduced time-to-market, developer productivity improvements).
- Risk reduction value (e.g., reduced probability of costly outages, compliance penalty avoidance, vendor lock-in elimination).
- Quantify each benefit with: estimated annual value, confidence level, and the assumption underlying the estimate.
- 🟤🔵: Savings from retiring legacy systems (infrastructure, licensing, support overhead).
- 🟤🔵: Avoided costs from preventing known risks (e.g., end-of-support platforms, known security vulnerabilities).
-->

| # | Benefit | Category | Annual Value | Confidence | Assumption | Evidence |
|---|---------|----------|--------------|------------|------------|----------|
|   |         |          |              |            |            |          |

### 7.2 Intangible Benefits ⚪

<!--
Describe the non-financial or hard-to-quantify benefits.

Expected content:
- Improved customer or employee experience and satisfaction.
- Strategic positioning and competitive advantage.
- Brand reputation or market perception improvements.
- Organizational capability building (skills, processes, platform maturity).
- Improved agility and time-to-market for future initiatives.
- Knowledge retention and reduced key-person dependency 🟤🔵.
- Enablement of future capabilities that are not yet fully defined (platform effect).
- Assign a qualitative value assessment (High / Medium / Low) and describe the rationale.
-->

| # | Intangible Benefit | Qualitative Value | Rationale |
|---|-------------------|-------------------|-----------|
|   |                   |                   |           |

### 7.3 Benefit Realization Timeline ⚪

<!--
Map when benefits will be realized over the project lifecycle and beyond.

Expected content:
- Phased benefit realization: when each benefit starts, reaches full value, and its duration.
- Distinguish between benefits realized during delivery (quick wins) and post-delivery.
- 🟤🔵: Benefits from legacy system retirement (when do savings start, when are they fully realized).
- 🟤🔵: Dual-running costs during transition and when they end.
- Cumulative benefit curve over the analysis period.
- Key milestones that trigger benefit realization (e.g., go-live, user migration, legacy decommission).
-->

| Benefit | Year 1 | Year 2 | Year 3 | Year 4 | Year 5 | Trigger Milestone |
|---------|--------|--------|--------|--------|--------|-------------------|
|         |        |        |        |        |        |                   |
| **Cumulative Total** | | | | | | |

### 7.4 Dis-benefits ⚪

<!--
Acknowledge the negative consequences or dis-benefits of the project.

Expected content:
- Costs or negative impacts that result from the project even though the net outcome is positive.
- Examples: disruption to current workflows, temporary productivity loss during transition, required organizational changes, training burden.
- 🟤🔵: Loss of familiar system, temporary feature reduction during migration, user retraining costs.
- How dis-benefits will be managed or minimized.
-->

| # | Dis-benefit | Impact | Mitigation / Management |
|---|-------------|--------|------------------------|
|   |             |        |                        |

---

## 8. Cost Estimate

### 8.1 Capital Expenditure (CapEx) ⚪

<!--
Estimate one-time costs required to deliver the project.

Expected content:
- Development costs (internal staff, contractors, consultancy).
- Infrastructure setup costs (cloud provisioning, hardware, network).
- Software licenses and tooling required for delivery.
- Migration tooling and execution costs 🔵.
- Training and change management costs.
- Data migration costs 🔵🟤 (data cleansing, transformation, validation).
- Contingency allocation with rationale for the percentage chosen.
- State the estimation methodology used (e.g., expert judgment, analogous estimating, parametric estimating, bottom-up).
- State the confidence level of the estimate (Rough Order of Magnitude / Budget / Definitive).
-->

| CapEx Category | Estimated Cost | Confidence | Notes |
|----------------|---------------|------------|-------|
| Development (Internal Staff) | | | |
| Development (Contractors / Consultancy) | | | |
| Infrastructure Setup | | | |
| Software & Tooling Licenses | | | |
| Data Migration 🔵🟤 | | | |
| Training & Change Management | | | |
| **Contingency** | | <!-- % --> | |
| **Total CapEx** | | | |

### 8.2 Operational Expenditure (OpEx) ⚪

<!--
Estimate recurring costs to operate and maintain the solution post-delivery.

Expected content:
- Cloud hosting or data center costs (compute, storage, networking).
- SaaS and software license renewals.
- Ongoing support and maintenance staffing.
- Monitoring, observability, and security tooling.
- Periodic compliance audits and certifications.
- 🟤🔵: Dual-running costs during transition (running both old and new systems).
- 🟤🔵: Legacy system costs that will be retired (negative OpEx—savings).
- Growth assumptions (e.g., user base growth of X% per year affecting cloud costs).
-->

| OpEx Category | Year 1 | Year 2 | Year 3 | Year 4 | Year 5 | Notes |
|---------------|--------|--------|--------|--------|--------|-------|
| Cloud / Infrastructure | | | | | | |
| SaaS & License Renewals | | | | | | |
| Support & Maintenance Staff | | | | | | |
| Monitoring & Tooling | | | | | | |
| Compliance & Audits | | | | | | |
| Dual-Running Costs 🟤🔵 | | | | | | |
| **Legacy Cost Retired 🟤🔵** | | | | | | *(savings — show as negative)* |
| **Net OpEx** | | | | | | |

### 8.3 Total Cost of Ownership (TCO) ⚪

<!--
Summarize the total cost of ownership over the analysis period.

Expected content:
- Combined CapEx + OpEx over 3–5 years.
- TCO comparison between options if applicable.
- 🟤🔵: TCO comparison of current system trajectory vs. proposed solution.
- Assumptions underlying the TCO calculation (e.g., discount rate, growth rate, inflation).
- State the analysis period (typically 3 or 5 years).
-->

| TCO Component | Year 1 | Year 2 | Year 3 | Year 4 | Year 5 | Total |
|---------------|--------|--------|--------|--------|--------|-------|
| CapEx | | | | | | |
| OpEx | | | | | | |
| **Total** | | | | | | |

### 8.4 Estimation Assumptions & Confidence ⚪

<!--
Document the key assumptions underlying the cost estimates.

Expected content:
- Staffing rate assumptions (internal cost per person-day, contractor day rates).
- Infrastructure pricing assumptions (cloud pricing tiers, reserved instance commitments).
- Inflation or cost escalation assumptions.
- Scope inclusions and exclusions that affect cost.
- Dependencies that could increase cost (e.g., vendor pricing changes, regulatory requirements).
- Confidence level for each major cost category (Low / Medium / High).
- Methodology used for estimation.
-->

| # | Assumption | Impact if Wrong | Confidence |
|---|------------|-----------------|------------|
|   |            |                 |            |

---

## 9. Financial Analysis

### 9.1 Cash Flow Projection ⚪

<!--
Present the projected cash flows over the analysis period.

Expected content:
- Year-by-year net cash flow (benefits minus costs).
- Distinguish between investment phase (negative cash flow) and return phase (positive cash flow).
- Include a cumulative cash flow row to show the payback point.
- Present for the expected case scenario.
- 🟤🔵: Include legacy system cost avoidance as a positive cash flow.
- 🟤🔵: Include dual-running costs as a negative cash flow during transition.
-->

| Cash Flow Item | Year 1 | Year 2 | Year 3 | Year 4 | Year 5 |
|----------------|--------|--------|--------|--------|--------|
| Gross Benefits | | | | | |
| Total Costs (CapEx + OpEx) | | | | | |
| **Net Cash Flow** | | | | | |
| **Cumulative Cash Flow** | | | | | |

### 9.2 Net Present Value (NPV) ⚪

<!--
Calculate the NPV of the project.

Expected content:
- The discount rate used and its rationale (e.g., corporate hurdle rate, weighted average cost of capital, risk-adjusted rate).
- NPV calculation for the expected case.
- Year-by-year discounted cash flows.
- Interpretation: positive NPV means the project creates value above the required rate of return.
-->

| Year | Net Cash Flow | Discount Factor | Discounted Cash Flow |
|------|--------------|-----------------|---------------------|
| 0 | | 1.000 | |
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |
| **NPV** | | | **<!-- sum -->** |

| Parameter | Value |
|-----------|-------|
| Discount Rate | <!-- e.g., 8% --> |
| Rationale | <!-- why this rate --> |

### 9.3 Internal Rate of Return (IRR) ⚪

<!--
Calculate the IRR of the project.

Expected content:
- IRR value.
- Comparison against the corporate hurdle rate or required rate of return.
- Interpretation: IRR above the hurdle rate indicates a financially attractive investment.
- Limitations of IRR (e.g., assumes reinvestment at IRR, can be misleading for non-conventional cash flows).
-->

### 9.4 Payback Period ⚪

<!--
Calculate the payback period.

Expected content:
- Simple (non-discounted) payback period.
- Discounted payback period (time to recoup investment in present-value terms).
- Whether the payback period is within acceptable organizational thresholds.
- Caveats: payback period ignores value created after the payback point.
-->

| Metric | Value |
|--------|-------|
| Simple Payback Period | <!-- e.g., 2.4 years --> |
| Discounted Payback Period | <!-- e.g., 2.8 years --> |
| Organizational Threshold | <!-- e.g., ≤ 3 years --> |
| Within Threshold? | <!-- Yes / No --> |

### 9.5 Benefit-Cost Ratio (BCR) ⚪

<!--
Calculate the benefit-cost ratio.

Expected content:
- Total discounted benefits divided by total discounted costs.
- BCR > 1.0 indicates the project creates more value than it costs.
- Interpretation of the BCR value.
-->

| Metric | Value |
|--------|-------|
| Total Discounted Benefits | |
| Total Discounted Costs | |
| Benefit-Cost Ratio | |

### 9.6 Sensitivity Analysis ⚪

<!--
Analyze how results change under different scenarios and assumptions.

Expected content:
- Best case, expected case, worst case scenarios.
- Key variables to stress-test (e.g., cost overrun, benefit delay, lower adoption, higher discount rate, extended timeline).
- Break-even analysis: what conditions would make NPV = 0.
- Scenario probabilities if estimable.
- Tornado diagram or table showing which variables have the greatest impact on NPV.
- 🟤🔵: Sensitivity to migration duration, dual-running cost extension, and legacy decommission delays.
-->

| Scenario | NPV | IRR | Payback | Probability |
|----------|-----|-----|---------|-------------|
| Best Case | | | | |
| Expected Case | | | | |
| Worst Case | | | | |
| Cost +20% | | | | |
| Benefits -20% | | | | |
| Benefits Delayed 6 Months | | | | |
| Discount Rate +3% | | | | |
| **Break-Even Point** | 0 | | | <!-- conditions --> |

### 9.7 Financial Summary ⚪

<!--
Summarize the key financial metrics for decision-makers.

Expected content:
- A concise table of all key financial indicators.
- Clear go/no-go indication from a financial perspective.
- Key assumptions that most affect the financial outcome.
-->

| Financial Indicator | Value | Threshold | Pass? |
|---------------------|-------|-----------|-------|
| NPV | | > 0 | |
| IRR | | > hurdle rate | |
| Payback Period | | ≤ X years | |
| BCR | | > 1.0 | |
| **Overall Financial Verdict** | | | <!-- Pass / Conditional Pass / Fail --> |

---

## 10. Risk Assessment

### 10.1 Risk Register ⚪

<!--
Catalog all identified risks that could affect the business case.

Expected content:
- Risk description.
- Category (Financial, Technical, Operational, Compliance, Market, Organizational, Migration, Vendor).
- Likelihood (Very Low / Low / Medium / High / Very High).
- Impact on the business case (Negligible / Minor / Moderate / Major / Catastrophic).
- Risk score (Likelihood × Impact).
- Mitigation strategy (Avoid / Reduce / Transfer / Accept).
- Risk owner.
- Residual risk after mitigation.
- Financial impact estimate if the risk materializes.
- 🟤🔵 specific: migration risks (data loss, extended downtime, feature regression, user resistance, rollback failure).
-->

| # | Risk | Category | Likelihood | Impact | Score | Mitigation | Owner | Residual Risk | Financial Impact |
|---|------|----------|------------|--------|-------|------------|-------|---------------|------------------|
|   |      |          |            |        |       |            |       |               |                  |

### 10.2 Risk Heat Map ⚪

<!--
Provide a visual or tabular summary of the most significant risks.

Expected content:
- A matrix plotting risks by likelihood (y-axis) and impact (x-axis).
- Color coding: 🟢 Low | 🟡 Medium | 🔴 High.
- Highlight the top 3–5 risks that most threaten the business case's financial viability.
- Note which risks could individually make NPV negative.
-->

### 10.3 Risk Appetite & Tolerances ⚪

<!--
Define the acceptable level of risk for this investment.

Expected content:
- The organization's risk appetite for this type of investment.
- Financial risk tolerances (e.g., maximum acceptable cost overrun, minimum acceptable NPV).
- Schedule risk tolerances (e.g., maximum acceptable delay).
- Technical risk tolerances (e.g., acceptable technology readiness level).
- Conditions that would trigger project reassessment or halt.
- Escalation criteria: who decides when risk thresholds are breached.
-->

| Risk Tolerance Dimension | Acceptable Level | Current Assessment | Within Tolerance? |
|--------------------------|-----------------|-------------------|-------------------|
| Maximum Cost Overrun | <!-- e.g., +20% --> | | |
| Minimum NPV | <!-- e.g., > €0 --> | | |
| Maximum Schedule Delay | <!-- e.g., 6 months --> | | |
| Minimum Technology Readiness | <!-- e.g., TRL 7+ --> | | |
| Maximum Migration Downtime 🟤🔵 | <!-- e.g., 4 hours --> | | |

---

## 11. Implementation Plan

### 11.1 Delivery Phases ⚪

<!--
Outline the high-level delivery phases and timeline.

Expected content:
- Phase names and descriptions (e.g., Discovery, Design, Build, Test, Migrate, Operate).
- Start and end dates for each phase (or quarter-level granularity).
- Key deliverables and milestones per phase.
- Dependencies between phases.
- Go/No-Go decision points between phases.
- 🟤🔵: Transition phase details (parallel run, phased cutover, rollback windows).
- 🟤🔵: Legacy decommission phase and timeline.
-->

| Phase | Description | Start | End | Key Deliverables | Go/No-Go Gate | Dependencies |
|-------|-------------|-------|-----|------------------|---------------|--------------|
|       |             |       |     |                  |               |              |

### 11.2 Key Milestones ⚪

<!--
List the major milestones and decision gates.

Expected content:
- Milestone name, date, and description.
- The decision or gate review associated with each milestone.
- Success criteria for each gate.
- Who is responsible for the gate decision.
- 🟤🔵: Migration cutover milestone with specific rollback criteria.
- 🟤🔵: Legacy system decommission milestone with sign-off requirements.
-->

| # | Milestone | Target Date | Gate Decision | Success Criteria | Decision Maker |
|---|----------|-------------|---------------|------------------|---------------|
|   |          |             |               |                  |               |

### 11.3 Change Management Plan ⚪

<!--
Describe how organizational change will be managed.

Expected content:
- Impact on current processes and workflows.
- Training plan for affected users and teams.
- Communication plan for stakeholder groups.
- Adoption strategy and user engagement approach.
- Resistance management strategy.
- 🟤🔵: Transition from legacy system to new system — user migration and retraining.
- 🟤🔵: Dual-running period and when users switch to the new system.
- Change champion or super-user network.
-->

| Change Dimension | Impact | Mitigation / Management | Owner |
|------------------|--------|------------------------|-------|
|                  |        |                        |       |

### 11.4 Transition Strategy 🟤🔵

<!--
Detail the strategy for transitioning from the current state to the target state.

Expected content:
- Transition approach: big bang cutover, phased rollout, parallel run, geographic rollout, feature-by-feature migration.
- Rollback strategy: how to revert if the transition fails, maximum rollback window.
- Data migration cutover approach: freeze, migrate, validate, switch.
- User communication and support during transition.
- Timeline for legacy system decommission.
- Criteria for declaring the transition complete.
- Risk of extended dual-running and its cost impact.
-->

| Transition Element | Approach | Timeline | Rollback Strategy | Owner |
|--------------------|----------|----------|-------------------|-------|
|                    |          |          |                   |       |

---

## 12. Resource Requirements

### 12.1 Team & Staffing ⚪

<!--
Define the team composition and staffing requirements.

Expected content:
- Required roles (e.g., product owner, Scrum master, architects, developers, QA, DevOps, UX/design, change manager).
- Number of people per role and seniority level.
- Internal staff vs. external contractors / consultancy split.
- Duration of each resource's involvement.
- Hiring or contracting timeline.
- Skill gaps and how they will be addressed.
- 🟤🔵: Additional resources for legacy system support during transition.
- 🟤🔵: Knowledge transfer resources and timeline.
-->

| Role | Count | Seniority | Internal / External | Duration | Start | Skill Gap |
|------|-------|-----------|---------------------|----------|-------|-----------|
|      |       |           |                     |          |       |           |

### 12.2 Technology & Infrastructure ⚪

<!--
Define the technology and infrastructure requirements.

Expected content:
- Development environments (local, CI/CD, staging, pre-production).
- Cloud or infrastructure resources required for delivery and production.
- Third-party services, APIs, and SaaS tools required.
- Hardware or networking requirements.
- Security tooling (SAST, DAST, secret scanning).
- 🟤🔵: Infrastructure for parallel running (both legacy and new).
- 🟤🔵: Migration tooling and environments.
-->

| # | Requirement | Type | Provisioning Timeline | Cost | Owner |
|---|-------------|------|----------------------|------|-------|
|   |             |      |                      |      |       |

### 12.3 Budget Profile ⚪

<!--
Present the budget phasing over the project lifecycle.

Expected content:
- Budget broken down by phase or quarter.
- CapEx vs. OpEx split per period.
- Funding release gates (when budget commitment is required vs. when it is released).
- Contingency reserve access criteria.
- 🟤🔵: Dual-running budget allocation.
- Total investment requested.
-->

| Period | CapEx | OpEx | Total | Cumulative | Gate / Approval |
|--------|-------|------|-------|------------|-----------------|
| Q1 | | | | | |
| Q2 | | | | | |
| Q3 | | | | | |
| Q4 | | | | | |
| Year 2 | | | | | |
| **Total** | | | | | |

---

## 13. Stakeholder Engagement

### 13.1 Stakeholder Register ⚪

<!--
Identify all stakeholders who influence, approve, or are affected by the investment.

Expected content:
- Internal stakeholders (executive sponsors, budget holders, development teams, operations, support, end-user departments).
- External stakeholders (customers, partners, regulators, vendors, auditors).
- Their role, interest, and influence level.
- Their attitude toward the project (champion, neutral, resistant).
- 🟤🔵: Stakeholders affected by the transition (current system users, legacy support teams, vendor contacts).
-->

| Stakeholder | Role / Interest | Influence Level | Attitude | Engagement Approach |
|-------------|-----------------|-----------------|----------|---------------------|
|             |                 |                 |          |                     |

### 13.2 Communication Plan ⚪

<!--
Define how stakeholders will be informed and engaged throughout the project.

Expected content:
- Communication objectives for each stakeholder group.
- Communication channels and frequency (e.g., monthly steering committee, weekly status report, quarterly town hall).
- Key messages per phase.
- Feedback mechanisms (e.g., surveys, retrospectives, open forums).
- Escalation paths for concerns.
-->

| Stakeholder Group | Channel | Frequency | Key Messages | Owner |
|-------------------|---------|-----------|---------------|-------|
|                   |         |           |               |       |

### 13.3 Governance & Decision Rights ⚪

<!--
Define the decision-making structure for the project.

Expected content:
- Steering committee composition and meeting cadence.
- Decision rights matrix: who decides what (e.g., scope changes, budget reallocation, timeline extensions, go/no-go gates).
- Escalation criteria and path.
- Change control process for scope, budget, or timeline changes.
- 🟤🔵: Governance for cutover decisions and rollback authorization.
-->

| Decision Type | Decision Maker | Advisory | Escalation Path |
|---------------|---------------|----------|-----------------|
| Scope Change | | | |
| Budget Reallocation | | | |
| Timeline Extension | | | |
| Go/No-Go Gate | | | |
| Cutover Decision 🟤🔵 | | | |
| Rollback Authorization 🟤🔵 | | | |

---

## 14. Dependencies & Assumptions

### 14.1 Dependencies ⚪

<!--
List all internal and external dependencies that the project relies on.

Expected content:
- Internal dependencies (e.g., other projects, shared services, infrastructure provisioning, HR hiring).
- External dependencies (e.g., vendor deliveries, third-party API availability, regulatory approvals, market conditions).
- Technical dependencies (e.g., platform releases, framework upgrades, security certificates).
- 🟤🔵: Legacy system dependencies that must be maintained or resolved before migration.
- 🟤🔵: Data migration dependencies (source data availability, data quality).
- For each dependency: owner, timeline, impact if not met, and mitigation.
-->

| # | Dependency | Type | Owner | Due Date | Impact if Not Met | Mitigation |
|---|------------|------|-------|----------|-------------------|------------|
|   |            |      |       |          |                   |            |

### 14.2 Assumptions ⚪

<!--
List all assumptions underlying the business case.

Expected content:
- Business assumptions (e.g., user adoption rate, market conditions, revenue projections).
- Technical assumptions (e.g., platform compatibility, API stability, performance benchmarks).
- Financial assumptions (e.g., discount rate, cost escalation, currency rates).
- Organizational assumptions (e.g., team availability, skill availability, stakeholder support).
- Regulatory assumptions (e.g., compliance requirements remain stable).
- 🟤🔵: Assumptions about legacy system stability during transition.
- 🟤🔵: Assumptions about data quality and completeness for migration.
- For each assumption: how it will be validated and the impact if it proves incorrect.
-->

| # | Assumption | Category | Impact if Wrong | Validation Method | Validated By | Date |
|---|------------|----------|-----------------|-------------------|-------------|------|
|   |            |          |                 |                   |             |      |

### 14.3 Constraints ⚪

<!--
List all constraints that limit the project's options or execution.

Expected content:
- Budget constraints (maximum investment, funding availability timing).
- Schedule constraints (hard deadlines, regulatory deadlines, market windows).
- Technical constraints (platform mandates, architecture standards, integration requirements).
- Resource constraints (team size limits, skill availability, facility constraints).
- Regulatory constraints (data residency, accessibility requirements, audit deadlines).
- 🟤🔵: Constraints from existing system (uptime requirements during migration, backward compatibility, contractual SLA obligations).
-->

| # | Constraint | Type | Impact on Project | Flexibility |
|---|------------|------|-------------------|-------------|
|   |            |      |                   |             |

---

## 15. Governance & Approval

### 15.1 Investment Approval ⚪

<!--
Define the approval process and required sign-offs.

Expected content:
- The approval body or individual who can authorize the investment.
- Approval threshold levels (e.g., who approves at what spend level).
- Required documentation for approval (e.g., this business case, financial model, risk assessment).
- Approval timeline and process.
- Conditions attached to approval (e.g., phased approval, stage-gate releases).
-->

| Approval Level | Approver | Threshold | Required Documentation | Timeline |
|----------------|----------|-----------|----------------------|----------|
|                |          |           |                      |          |

### 15.2 Stage-Gate Reviews ⚪

<!--
Define the stage-gate review process for the investment.

Expected content:
- List of stage-gate reviews throughout the project lifecycle.
- Criteria for passing each gate.
- Who conducts the review.
- What happens at each gate (approve to proceed, conditional approval, pivot, halt).
- Reporting requirements at each gate (updated financials, risk assessment, progress metrics).
- Provision for re-evaluating the business case at each major gate.
-->

| Gate | Phase Completed | Review Criteria | Reviewers | Possible Outcomes | Reporting Requirements |
|------|-----------------|-----------------|-----------|-------------------|----------------------|
|      |                 |                 |           |                   |                      |

### 15.3 Exception Reporting ⚪

<!--
Define how exceptions and variances will be reported and managed.

Expected content:
- Triggers for exception reporting (e.g., cost variance > X%, schedule variance > Y weeks, new critical risk).
- Escalation path and timeline for exceptions.
- Who has authority to approve exceptions or variances.
- How exceptions affect the original business case assumptions.
- Process for re-baselining the business case if significant variances occur.
-->

| Exception Trigger | Threshold | Escalation Path | Decision Authority | Response Timeline |
|-------------------|-----------|-----------------|-------------------|-------------------|
| Cost overrun | <!-- e.g., > 10% --> | | | |
| Schedule delay | <!-- e.g., > 4 weeks --> | | | |
| New critical risk | | | | |
| Benefit shortfall | <!-- e.g., > 20% --> | | | |
| Scope change request | | | | |

---

## 16. Post-Implementation Review Plan

### 16.1 Benefit Realization Tracking ⚪

<!--
Define how benefits will be measured and tracked after implementation.

Expected content:
- Which benefits from Section 7 will be tracked post-implementation.
- Measurement methodology and data sources.
- Measurement frequency (e.g., monthly for first 6 months, then quarterly).
- Responsibility for tracking and reporting.
- Actions if benefits are not realized as expected (e.g., remediation plan, investment reassessment).
- Timeline for benefit reviews (typically at 6, 12, 24, and 36 months post-implementation).
-->

| Benefit | KPI | Measurement Method | Frequency | Owner | Review Milestone |
|---------|-----|-------------------|-----------|-------|-----------------|
|         |     |                   |           |       |                 |

### 16.2 Post-Implementation Review Schedule ⚪

<!--
Define the schedule and scope for post-implementation reviews.

Expected content:
- When reviews will occur (e.g., 3 months, 6 months, 12 months, 36 months post-go-live).
- Scope of each review (what will be assessed).
- Who will conduct the review.
- How findings will be actioned.
- Comparison against the original business case assumptions and projections.
- Whether the project achieved its objectives and success criteria from Section 4.
-->

| Review | Timing | Scope | Reviewers | Deliverable |
|--------|--------|-------|-----------|-------------|
| Initial Review | <!-- e.g., 3 months post-go-live --> | <!-- scope --> | | <!-- e.g., Quick Start Review Report --> |
| Benefit Review 1 | <!-- e.g., 6 months --> | <!-- scope --> | | <!-- e.g., Benefit Realization Report --> |
| Benefit Review 2 | <!-- e.g., 12 months --> | <!-- scope --> | | |
| Full Post-Implementation Review | <!-- e.g., 24 months --> | <!-- scope --> | | <!-- e.g., PIR Report --> |

### 16.3 Lessons Learned Capture ⚪

<!--
Define how lessons learned will be captured and shared.

Expected content:
- When retrospectives or lessons learned sessions will occur.
- How lessons will be documented (e.g., lessons learned register).
- How lessons will be disseminated to other projects or teams.
- Who is responsible for ensuring lessons are actioned.
-->

---

## 17. Appendices

### Appendix A: Detailed Financial Model

<!--
Reference or include the full financial spreadsheets, assumptions, and calculations.

Expected content:
- Link to the financial model file (Excel, Google Sheets, or equivalent).
- Summary of all key financial assumptions.
- Year-by-year cash flow projection tables.
- TCO comparison: current system vs. proposed solution (🟤🔵).
- Discount rate derivation.
- Sensitivity analysis worksheets.
- Break-even analysis details.
-->

### Appendix B: Options Analysis Detail

<!--
Include the detailed evaluation of each option.

Expected content:
- Full scoring rationale for each option against each criterion.
- Assumptions specific to each option's cost and benefit estimates.
- Risk assessments specific to each option.
- Any technical proof-of-concept or prototype results that informed the evaluation.
-->

### Appendix C: Market Research & Demand Data

<!--
Include or reference supporting market and demand data.

Expected content:
- Survey results, interview summaries, or focus group transcripts.
- Market research reports and analyst forecasts.
- Competitive analysis details.
- User behavior analytics and adoption data.
- Links to source documents.
-->

### Appendix D: Technical Proof-of-Concept Results

<!--
Document any technical experiments or prototypes conducted to inform the business case.

Expected content:
- Objective of the PoC.
- Methodology and scope.
- Results and findings.
- How PoC results influenced the business case assumptions.
- Limitations of the PoC.
- Recommendations from PoC findings.
-->

### Appendix E: Risk Assessment Details

<!--
Include supplementary risk analysis data.

Expected content:
- Full risk register with all fields.
- Monte Carlo simulation results if available.
- Historical risk data from similar projects.
- Risk response cost-benefit analysis.
-->

### Appendix F: Current System Documentation (🟤🔵)

<!--
Reference or include documentation of the existing system that supports the business case.

Expected content:
- Architecture diagrams of the current system.
- API documentation and contracts.
- Known issues, incidents, and their business impact.
- Maintenance cost trends and projections.
- Vendor contract details and exit clauses.
- Compliance gap analysis.
-->

### Appendix G: Stakeholder Interview & Consultation Notes

<!--
Summarize key insights from stakeholder consultations.

Expected content:
- Date, participants, and format of each interview/workshop.
- Key themes and quotes.
- Areas of agreement and disagreement.
- How stakeholder input shaped the business case.
-->

### Appendix H: Regulatory & Compliance Mapping

<!--
Map specific regulatory requirements to the project's response.

Expected content:
- Regulation by article/section.
- How the project addresses each requirement.
- Cost of compliance per regulation.
- Risk of non-compliance.
-->

---

## Document History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | <!-- date --> | <!-- author --> | Initial template |

---

## Usage Guide

| Icon | Meaning | When Applicable |
|------|---------|-----------------|
| 🟢 | Green Field | Building new software from scratch |
| 🟤 | Brown Field | Extending or refactoring existing software |
| 🔵 | Software Modernization | Migrating or re-architecting legacy systems |
| ⚪ | All Types | Applicable to every project type |

**How to use this template:**
1. Classify your project type in Section 2.2.
2. Sections marked with 🟢 🟤 🔵 icons indicate particular relevance—prioritize those sections.
3. Mark sections as **[APPLICABLE]** or **[NOT APPLICABLE]** based on your project type.
4. Remove content within `<!-- -->` comments and replace with project-specific information.
5. Remove entire sections that are not applicable, noting the reason for exclusion.
6. The ⚪ (all types) sections are required unless explicitly justified as not applicable.
7. This business case should follow a viability study (if one was produced). Reference the viability study's findings and build upon them.
8. Update the financial analysis whenever material changes occur in scope, cost, or benefits.
9. Use the Post-Implementation Review Plan (Section 16) to hold the project accountable for delivering the promised benefits.

**Relationship to Viability Study:**
- The viability study answers: *"Is this project feasible and worth pursuing?"*
- The business case answers: *"Should we invest, how much, and in which option?"*
- If a viability study exists, this business case should reference and build upon its findings rather than repeating the analysis from scratch.