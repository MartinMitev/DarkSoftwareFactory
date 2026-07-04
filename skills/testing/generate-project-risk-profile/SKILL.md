---
name: generate-project-risk-profile
description: Generates an evidence-based Software Project Risk Profile document using the repository template `templates/testing/project-risk-profile.md`. This skill should be used when preparing risk reviews, stage-gate decisions, or release readiness assessments and when core project documents (Business Case, User Stories, SRS/Requirements, and Software Architecture) exist and must be analyzed for risks, gaps, and contradictions.
---

# Generate Project Risk Profile

## Overview

Generate a complete Project Risk Profile document by deeply analyzing key project documents and translating them into a structured risk register, top risk summary, risk heat map, and mitigation roadmap.

## Activation

Use when the user asks to create/generate a risk profile, risk register, project risk assessment, release risk assessment, stage-gate risk report, or "risk profile" document for a software project.

Primary evidence sources (in order):
- `documents/analysis/business-case.md` output (Business Case)
- `documents/analysis/user-stories.md` output (User Stories)
- `documents/analysis/software-requirements-specification.md` output (SRS)
- `documents/design/software-architecture.md` output (Software Architecture)

## Workflow

### Phase 1: Load Template and Discover Inputs

1. Read the risk profile template at `templates/testing/project-risk-profile.md`.
2. Discover candidate source documents across the workspace:
   - Business Case (`business-case*.md`, `*business case*.md`)
   - User Stories (`user-stories*.md`, `*user stories*.md`)
   - Requirements (`software-requirements-specification*.md`, `*srs*.md`, `*requirements*.md`)
   - Architecture (`software-architecture*.md`, `*architecture*.md`, `adr*/*.md`)
3. Select the canonical versions (prefer baselined/approved/latest revised versions). Record their paths/links in the generated document.
4. If any of the four key documents are missing:
   - Continue, but explicitly record the gap as a 🔴 risk and mark assumptions.
   - Avoid inventing facts. Derive risk hypotheses from what exists.

### Phase 2: Deep Analysis (Evidence Extraction)

Perform deep analysis with a bias toward extracting concrete, testable statements.

#### 2.1 Business Case Analysis (Investment/Delivery Risk)

Extract:
- Objectives, success criteria, KPIs, constraints (budget/timeline)
- Options and assumptions (including "do nothing")
- Cost drivers, dual-running, retirement savings (if applicable)
- Risks explicitly mentioned and implicit risk drivers (tight payback, uncertain benefits)

Derive risk themes:
- Value realization risk (adoption, benefits uncertainty)
- Funding/budget risk (runway vs scope)
- Timeline risk (hard deadlines, gate dependencies)
- Operational transition risk (dual-running, migration)

#### 2.2 User Stories Analysis (Scope/Change/Risk Hotspots)

Extract:
- Epics/features and MoSCoW priorities
- Dependencies, sequencing, and “must-have” release scope
- Acceptance criteria quality (testability, ambiguity)
- Known fragile/complex journeys (multi-step flows, cross-system interactions)

Derive risk themes:
- Scope volatility and backlog churn
- Requirements ambiguity risk (non-testable AC)
- Integration and workflow risk (cross-system, manual steps)
- Usability/adoption risk (complex UX, training burden)

#### 2.3 SRS/Requirements Analysis (Correctness/NFR/Compliance Risk)

Extract:
- Functional requirements clusters
- NFRs (availability, latency, throughput, RTO/RPO, security controls)
- Regulatory/compliance requirements and verification expectations
- Interface contracts and data requirements (PII, retention)

Derive risk themes:
- Non-functional validation risk (targets missing or untestable)
- Security/privacy/compliance gaps
- Contract and versioning risk
- Data integrity and lifecycle risk

#### 2.4 Architecture Analysis (Tech/Operational Risk)

Extract:
- Key architectural decisions (ADRs), trade-offs, and unresolved decisions
- Deployment model and operational model (on-call, observability)
- Data architecture and migration strategy (if applicable)
- Critical dependencies (vendors, shared platforms)

Derive risk themes:
- Scalability/performance risk
- Resilience/operability risk
- Complexity and coupling risk
- Vendor lock-in risk and exit gaps

#### 2.5 Cross-Document Consistency Checks (Contradictions)

Identify contradictions and gaps across documents:
- Scope vs Business Case options and budget assumptions
- User stories vs SRS requirements (missing stories, missing requirements)
- Architecture vs SRS NFRs (no mechanism to meet targets)
- Architecture vs delivery plan (complexity incompatible with timeline)

Each contradiction becomes:
- A documented risk (likely 🔴/🟡)
- A clarification question (if blocking) or an explicit assumption

### Phase 3: Risk Register Construction

1. Use the template taxonomy categories.
2. Write risks as: "If [cause], then [impact] because [mechanism]."
3. For each risk, fill:
   - Trigger / early warning indicators
   - Treatment strategy (Avoid/Reduce/Transfer/Accept)
   - Mitigation actions (concrete and time-bound)
   - Risk owner (role if person unknown)
   - Residual risk score (required for non-green)
4. Calibrate likelihood/impact using the project context:
   - Impact should tie to business outcomes (customer, compliance, cost, schedule)
   - Likelihood should tie to evidence (unknowns, complexity, org readiness)
5. Maintain a balanced register:
   - Include delivery, quality, security, ops, architecture, dependency risks
   - Do not over-index on one category unless evidence demands it

### Phase 4: Generate the Project Risk Profile Document

1. Follow `templates/testing/project-risk-profile.md` section-by-section.
2. Replace all `<!-- -->` placeholders with project-specific content.
3. Populate:
   - Section 4 snapshot and heat map (top risks only)
   - Section 5 top risks (ranked)
   - Section 6 full risk register
   - Sections 7-12 with category-specific risks and evidence
   - Section 13 mitigation roadmap (30/60/90 days)
   - Section 15 residual risk acceptance checklist (if relevant to release/cutover)
4. Ensure the Executive Summary is consistent with the register and top risks.

### Phase 5: Quality Checks

Before delivering the generated document, verify:
- No placeholders remain (except date/status fields intended for humans).
- All high risks have owners, mitigations, and due dates.
- Mitigations are measurable (gates, criteria, artifacts).
- Contradictions are explicitly recorded as risks with clarification path.
- The document references the canonical Business Case, User Stories, SRS, and Architecture sources.

## Output

Save the generated document to a project-appropriate location. Default to `documentation/project-risk-profile.md` unless the repository has an established docs folder.

## Resources

### assets/
Contains the canonical template used for generation.

### references/
Optional: store internal risk scoring rules or org-specific policy mappings.

### scripts/
Optional: no scripts are required for this skill.

