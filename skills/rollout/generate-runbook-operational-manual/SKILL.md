---
name: generate-runbook-operational-manual
description: Generates an evidence-based Run Book / Operational Manual using the repository template `templates/rollout/runbook-operational-manual.md`. This skill should be used when establishing or documenting operations for go-live, handover to operations, or steady-state running — service levels, support and on-call, monitoring and alerting, incident handling, deployment and rollback, recovery and continuity, maintenance, and security operations — and when core project documents (Architecture, SRS, Business Case, Test Concept, Environment Setup, Project Plan) and the codebase exist and must be analyzed to derive the component inventory, external dependencies, service levels, routine operations, alert catalogue, incident and troubleshooting playbooks, and recovery procedures. Gaps, unclear statements, and contradictions — including conflicts between documents and code evidence — are resolved by asking targeted open questions with suggested valid answers before generation.
---

# Generate Run Book / Operational Manual

## Overview

Generate a complete, evidence-based Run Book / Operational Manual — the single authoritative source for operating a system day to day and during incidents — by extracting operationally relevant facts from existing project documents and the code itself, then translating them into the component inventory, external dependency catalogue, service level framework, access and break-glass model, routine operations schedule, deployment and rollback procedures, monitoring and alert catalogue, incident and troubleshooting playbooks, recovery and continuity procedures, maintenance and security operations, and the operational readiness gate.

The Run Book's value comes from the rigor of the analysis and clarification, not from filling a template: the skill deeply analyzes all available information, detects gaps, unclear statements, and contradictions (explicitly including code-vs-documentation conflicts), and asks targeted open questions with suggested possible valid answers before generating anything. A new operator must be able to run, monitor, troubleshoot, and recover the system using this document alone — without tribal knowledge.

## Activation

Use when the user asks to create, generate, or draft:

- A Run Book, operational manual, or operations documentation
- Handover-to-operations documentation ("handover to ops", "service transition")
- On-call, support, monitoring, or incident documentation
- Recovery/continuity documentation (backup, failover, DR run book)
- An operational readiness baseline or operations sign-off package

Primary evidence sources (in order of weight for operational facts):

- Environment Setup (stages, promotion flow, pipelines, quality gates, secrets, monitoring/on-call, backup/DR, support model — the closest operational document)
- Software Architecture (components, deployment model, hosting, technology stack, operations model)
- SRS / Requirements (NFRs → SLA/SLO targets, compliance → audit operations, integrations → external dependencies)
- Business Case (business criticality, risk appetite → RTO/RPO targets, operational investment scope)
- Test Concept (quality gates → pre/post-deployment checklists; availability/live test cases → readiness checklist)
- Project Plan (§17.5 cutover runbook, hypercare, knowledge transfer, transition planning)
- Risk Profile (operational risks → Executive Summary top risks)
- ADRs, existing runbooks, incident postmortems, support/operations notes
- **Codebase and configuration evidence** (see Phase 1 step 3 — the primary source when documents are missing or vague)

## Instructions

### Phase 1: Information Gathering & Deep Analysis

1. **Read the template** at `templates/rollout/runbook-operational-manual.md` to understand the full structure, all 18 sections and their subsections, and the per-section guidance comments. Pay special attention to:
   - The ID schemes used across inventories — `COMP-XXX` (components, Section 3.2), `DEP-XXX` (external dependencies, Section 3.3), `SLO-XXX` (service levels, Section 4.1), `OPS-XXX` (routine tasks, Section 6.1), `ALERT-XXX` (alerts, Section 9.2), `TS-XXX` (troubleshooting entries, Section 11.1), `KI-XXX` (known issues, Section 11.2). These IDs are cross-referenced between sections; they must be used unchanged.
   - The canonical cross-references: alert catalogue rows (9.2) reference `COMP-XXX` and their first response links to a `TS-XXX` row; SLO monitoring (9.4) references the `SLO-XXX` rows (4.1); escalation (10.3) references the on-call contacts (4.3) and Appendix A; incident communication (10.4) references the stakeholder channels (4.4); Appendix C indexes all IDs for navigation.
   - The readiness gate: Section 16 (16.1 checklist, 16.2 exit criteria, 16.3 sign-off) is the operational acceptance mechanism and must reference the actual content generated in Sections 3–15.
   - The linkage to `templates/testing/availability-live-test-cases.md` (Section 6, operational readiness and runbook tests) — readiness item 11 requires those runbook tests to have passed.
2. **Discover and read all existing project information:**
   - Search `documentation/` first (the recommended artifacts location), then the workspace: architecture (`software-architecture*.md`, `*architecture*.md`), requirements (`software-requirements-specification*.md`, `*srs*.md`, `*requirements*.md`), business case (`business-case*.md`), test concept (`test-concept*.md`, availability/live test cases), environment setup (`environment-setup*.md`, `*environment*.md`), project plan (`project-plan*.md`, `project-scope*.md`), risk profile (`*risk-profile*.md`), ADRs (`adr*/*.md`, `*adr*.md`), existing runbooks (`*runbook*.md`), incident postmortems (`*postmortem*.md`, `*incident*.md`), user manuals, and README/docs folders.
   - If `documentation/` is empty or no operational documents exist, proceed from code alone: record the gap explicitly, shift question priority toward [Critical], and mark every derived fact as an assumption with a validation action.
   - For a revision of an existing run book, adopt and extend rather than restart; record deltas in Document History and Appendix E (operational procedure change log).
3. **Analyze the codebase for operational facts.** The code is evidence about how the system actually runs — the run book must match reality, not aspiration:
   - **Components (→ Section 3.2):** entry points, repository structure, Dockerfile(s), docker-compose, k8s manifests, serverless configs, background jobs/schedulers/workers. Derive type, purpose, and initial criticality per component; single-instance components without redundancy are SPOF candidates.
   - **External dependencies (→ Section 3.3):** API clients and SDKs, connection strings, webhook receivers, provider configurations, SaaS references. Derive integration type and, from the code, the actual behavior during dependency outages (retry policies, circuit breakers, queueing, fail-open/fail-closed).
   - **Environments and configuration (→ Sections 3.4, 8.1, 5.4):** IaC, CI/CD configs, `.env.example`, secret-manager references. Derive stage usage, configuration sources of truth, drift-detection implications, and secret handling evidence.
   - **Deployment method (→ Sections 7.3, 7.5, 7.6):** pipeline definitions, blue-green/canary evidence, database migration tooling and migration patterns. Derive the actual deployment methods; destructive migrations directly constrain rollback feasibility (7.5).
   - **Observability (→ Sections 9.1, 9.2, 9.3):** health endpoints, metrics export, log framework and structured fields, tracing instrumentation, dashboards-as-code, alert-rule files. Derive what monitoring actually exists — never invent a monitoring stack that the code does not show.
   - **Recovery (→ Sections 12.1, 12.2, 12.3):** backup scripts/configs, replication evidence, failover configurations. Derive backup scope and restore tooling; absence of backup evidence is a 🔴 readiness gap, not something to assume away.
   - **Operational automation (→ Sections 6.1, 11.3, Appendix B):** Makefile targets, `scripts/`, admin endpoints, maintenance/cron jobs. Derive routine-task tooling and the highest-value commands for the cheat sheets.
   - **Security (→ Sections 5.1, 5.2, 14):** authentication mechanisms, audit logging, certificate and secret management, privileged operations. Derive the access matrix draft and audit capabilities.
4. **Classify the project type** based on available evidence (template Metadata field "Project Type"):
   - **Green Field**: new system — much of the operational surface is planned rather than built; the run book documents the target operating model and the readiness gate drives what must be built before go-live.
   - **Brown Field**: existing system enhancement — the run book documents actual operations as-is, including undocumented tribal knowledge (workarounds, shadow tooling, shared credentials).
   - **Software Modernization**: legacy replacement — link the run book to the project plan's cutover runbook (§17.5), dual-running operations, and legacy decommission support.
   - If a preceding document already classified the project type, adopt it unless new evidence contradicts it — note any contradiction as a Phase 2 question.
5. **Map existing information to template sections.** For each of the 18 sections and their subsections, determine:
   - **Covered**: sufficient evidence exists to populate the section factually.
   - **Partially Covered**: information exists but is vague or incomplete (e.g., "monitoring exists" without alert conditions or routing; "backups happen nightly" without scope or restore steps).
   - **Gap**: no information exists.
   - **Contradiction**: sources conflict — with special weight on code-vs-documentation conflicts (e.g., documents claim blue-green deployment but pipelines show a single-target rolling model; documents claim on-call exists but no rotation tooling or schedule is discoverable).
6. **Perform deep runbook-fact analysis.** Go beyond surface-level mapping:

   **Component inventory completeness (Section 3.2):** Every `COMP-XXX` row needs dependencies and blast radius ("depended on by"), an initial criticality tier, and SPOF marking. A component without dependency mapping silently underestimates blast radius during incidents. Job/scheduler components are routinely forgotten — include them.

   **Service level derivability (Section 4.1):** `SLO-XXX` rows must derive from SRS NFRs where they exist; if no NFR targets exist, do not invent numbers — record them as questions or assumptions. An error budget policy (what happens when the budget is exhausted) must be stated, or the SLOs are decorative.

   **Alert actionability (Section 9.2 ↔ 11.1):** Every `ALERT-XXX` row needs a condition, severity, first response, and routing; the first response must link to a `TS-XXX` troubleshooting row. Alerts without first responses are noise generators, not run book content.

   **Incident severity consistency (Sections 4.2 / 10.1 / 10.4):** The acknowledge SLAs (10.1) must be deliverable by the support model and operating hours (4.2), and the update cadence (10.1) must match the communication channels (4.4). A 15-minute Sev1 acknowledge SLA with no 24/7 coverage is 🔴 Not Ready.

   **Rollback feasibility (Sections 7.3 ↔ 7.5):** Rollback steps must match the actual deployment method found in pipeline evidence, and database migration constraints (destructive vs. additive migrations found in code) must be stated explicitly. A rollback procedure that the deployment method cannot execute is worse than none.

   **Recovery capability truth (Section 12):** RTO/RPO targets must align with business-case criticality; a backup that has never been restored is not a backup — record the restore test cadence and last successful test (12.1/12.5). Absent DR evidence with Tier-1 criticality is 🔴.

   **Cross-source consistency:** Architecture's deployment model vs environment-setup stages vs code evidence; SRS integration requirements vs derived external dependencies; business-case criticality vs incident severity definitions. Surface every conflict as a question rather than silently choosing one source.

   **Operations readiness (Sections 4, 6, 14, 15):** Support model, on-call, routine task schedule, patching cadence, handover checklist. These are the most commonly completely undocumented areas — treat any 🟡 here as 🔴 priority for questions.

   **Implicit facts from code evidence:** A health endpoint implies a post-deployment verification method (7.4); metrics export implies a dashboard stack that must be confirmed; admin endpoints imply privileged operations for the access matrix (5.1); scheduled jobs imply routine checks (6.1). Surface these implied facts explicitly and ask the user to confirm, challenge, or refine them.

7. **Build a readiness map** — for each section, tag readiness:
   - 🟢 **Ready**: detailed, specific, sufficient to write evidence-based content.
   - 🟡 **Partially Ready**: exists but vague, incomplete, or inconsistent across sources.
   - 🔴 **Not Ready**: missing, unquantified, or contradictory — cannot be documented without clarification.

   Sections with 🔴 or 🟡 readiness are priority candidates for Phase 2 questions.

### Phase 2: Clarification Questions

Before generating the document, ask the user targeted questions for every 🔴 Not Ready, 🟡 Partially Ready, Gap, or Contradiction area identified in Phase 1.

#### Question Design Principles

- **Ask open questions** that invite thoughtful responses and deeper thinking — not yes/no questions.
- **Always suggest 2–3 possible valid answers** for each question to help the user think through the options and to demonstrate understanding of the domain.
- **Contextualize each question** — briefly explain why the information matters for the Run Book and what happens if it remains unanswered (e.g., "Without an on-call rotation, the Sev1 acknowledge SLA (10.1) is undeliverable and readiness item 3 (16.1) fails").
- **Group questions by template section** so the user can address them systematically.
- **Prioritize questions** — mark questions as:
  - **[Critical]**: Blocks generation — the section cannot be filled without this information (e.g., who operates the system, business criticality, deployment approval flow).
  - **[Important]**: Affects the quality and completeness of the document — it can be drafted but will contain gaps or unverifiable claims.
  - **[Optional]**: Refines the document; can be documented as an assumption with a validation plan.
- **Reference the source** of the gap or contradiction (e.g., "The promotion flow documents blue-green deployment, but the pipeline evidence shows a single-target rolling deployment with destructive migrations").
- **Surface implicit facts** from code evidence and ask the user to confirm, challenge, or refine them.
- **Do not ask questions that can be answered by reading existing documentation or code** — if the answer exists in a file already read, use it directly.
- **Distinguish information that must be resolved now from information that can be documented as assumptions with validation plans** — for [Optional] questions, offer to proceed with a stated assumption.
- **Batch by priority**: lead with [Critical] questions, then [Important]; do not present one unprioritized giant list, and do not drip questions one at a time over many turns.

#### Question Template

For each question, use this format:

---

**[Priority] Section X.Y — [Topic]**

[Context: why this matters for the Run Book and what happens if unanswered]

[The open question]

Suggested answers:
- *Option A*: [description and implications for the document]
- *Option B*: [description and implications for the document]
- *Option C*: [description and implications for the document]
- *Custom*: [your own answer]

---

#### Minimum Required Questions (All Project Types)

These must be resolved (or explicitly documented as assumptions with validation plans) before generation:

1. What is the business criticality tier, and what SLA/SLO targets apply — derive from SRS NFRs, or commit new targets?
2. Who operates the system — dedicated operations team, dev-team on-call, or hybrid — and what are the support tiers and operating hours?
3. Which on-call tooling and rotation applies, and what is the escalation ladder (4.3)?
4. Who approves production deployments, what change classification applies (8.4), and what is the hotfix path (7.6)?
5. What are the incident severity definitions and their response/update SLAs (10.1)?
6. What monitoring and alerting actually exists vs. is planned — the code analysis findings must be confirmed as-is or replaced by the target stack?
7. What is backed up, on what schedule, and what RTO/RPO targets apply (12.1/12.3)?
8. Where do secrets live, who may rotate them, and what is the break-glass procedure (5.2/5.4)?
9. What maintenance windows and patching cadence apply (6.4/13.1)?
10. Who fills the Metadata roles — Operations Lead, DevOps Lead, Security Lead, Technical Lead, Product Owner?

**Green Field additional questions:**
- Which operational capabilities are built vs. planned — health endpoints, metrics export, backup tooling, alert routing found in code may be development-only?
- What is the handover plan from project to operations (15.1) — who accepts on-call, access, and tooling ownership?
- What readiness prerequisites must exist before first PROD release (16.1) — rotation live, restore tested, alerts routed?

**Brown Field additional questions:**
- What undocumented tribal knowledge must be captured as-is — workarounds, shadow tooling, shared credentials, manual steps nobody has written down?
- Which operational facts are stable vs. being modified by this project — what deltas must the run book record?
- What backward-compatibility constraints apply (fixed URLs partner systems point at, pinned service accounts)?

**Software Modernization additional questions:**
- How does this run book link to the project plan's cutover runbook (§17.5) — who operates during dual-running, and how do incidents route across old and new systems?
- What support must remain for the legacy system during transition, and what changes at decommission?
- What is the operations parity target between legacy and target systems — identical run book coverage, or intentionally different?

#### Worked Example Questions

**Example Question (Contradiction — Deployment Method, Code vs. Docs)**

---

**[Critical] Sections 7.3 / 7.5 — Deployment Method and Rollback Feasibility**

The Environment Setup documents a blue-green deployment for production, but the pipeline evidence (deploy job definitions, IaC, migration tooling) shows a single-target rolling deployment, and the database migration history contains destructive migrations. Sections 7.3 (procedure per method), 7.5 (rollback steps and database migration constraints), and 7.4 (verification) cannot be generated consistently until this is settled — and rollback is only executable if the documented method matches what actually runs.

Which deployment and rollback model does the document record?

Suggested answers:
- *Option A*: "Record the as-is rolling model: single-target rolling update, rollback = redeploy previous artifact; add an explicit constraint row to 7.5 that destructive migrations make rollback impossible past the migration step, with expand/contract migration adoption as the recorded target. The run book matches how the system actually ships."
- *Option B*: "Record the as-is model now plus a maintenance item (13.1) to introduce blue-green before the next major release; the document becomes the target state with the delta recorded as a readiness prerequisite (16.1)."
- *Option C*: "Split by component: rolling for app services, blue-green for stateless frontends only; 7.3 documents per-component methods with `COMP-XXX` references, and 7.5 states per-method rollback steps."
- *Custom*: [your own answer]

---

**Example Question (Gap — No On-Call Defined)**

---

**[Critical] Sections 4.2 / 4.3 / 10 — Support Model and On-Call**

No document or code evidence names who operates the system, an on-call rotation, or an escalation path. Support tiers (4.2), on-call contacts (4.3), severity acknowledge SLAs (10.1), and escalation triggers (10.3) all depend on this — without it the incident section is unexecutable and readiness item 3 (16.1) fails.

Who operates the system, and what on-call model applies?

Suggested answers:
- *Option A*: "Dev team on-call: weekly rotating primary/secondary, published schedule (e.g., PagerDuty), escalation to Tech Lead then Product Owner. Documented as-is for a small team; named backups recorded for every role."
- *Option B*: "Dedicated operations team as L1/L2 with engineering L3 on business hours; the operations team supplies names and the rotation link during handover (15.1)."
- *Option C*: "No on-call yet — document the gap explicitly, define the target model, and add handover checklist items (15.1) requiring the rotation to be live before first PROD release; the readiness gate (16) holds sign-off until it is."
- *Custom*: [your own answer]

---

**Example Question (Implicit Fact — Monitoring Found in Code)**

---

**[Important] Sections 9.1 / 9.2 — Monitoring Evidence From Code**

Code analysis found a `/health` endpoint, a metrics export (Prometheus-format), and alert-rule files, but no document mentions monitoring at all. The dashboards (9.1) and alert catalogue (9.2) should inventory these findings as-is rather than inventing a monitoring stack — but production thresholds and routing must be confirmed.

Which of the monitoring facts found in the code should the document catalogue as-is?

Suggested answers:
- *Option A*: "Catalogue the health endpoint and exported metrics as-is; mark the in-code alert definitions as 'code-defined, thresholds unconfirmed' with a validation action to confirm thresholds and routing before the readiness gate."
- *Option B*: "Full adoption: convert each in-code alert rule into an `ALERT-XXX` row with `COMP-XXX` references, confirm routing with the on-call setup (4.3), and record the alert-rule files as the catalogue's source of truth."
- *Option C*: "Treat the in-code monitoring as development-only; the target monitoring stack is planned separately (Environment Setup 9.5) — document the gap and record the readiness prerequisite instead."
- *Custom*: [your own answer]

---

### Phase 3: Document Generation

Once all critical and important questions are resolved, generate the Run Book.

#### Generation Rules

1. **Use the template structure exactly** — follow `templates/rollout/runbook-operational-manual.md` section by section (1–18 plus Document History), including all subsections and their tables.
2. **Replace all `<!-- -->` placeholders** with project-specific content derived from the analysis and the user answers; fill every table with concrete, specific content.
3. **Keep the document evidence-based** — use explicit references to source documents and code ("per Environment Setup Section 9.5, on-call wiring exists"; "per deploy pipeline definition, rolling update"). Where information is missing, state the assumption explicitly with an owner and a validation action rather than inventing facts. Record scope inclusions/exclusions (Section 2.2) explicitly, and populate the definitions (Section 2.3) with every term and ID scheme the document uses.
4. **Use the template's ID schemes unchanged** (`COMP-XXX`, `DEP-XXX`, `SLO-XXX`, `OPS-XXX`, `ALERT-XXX`, `TS-XXX`, `KI-XXX`) and keep inventories cross-referenced: alert rows reference components and their first response links to a `TS-XXX` row; SLO monitoring references `SLO-XXX` rows; Appendix C indexes all IDs.
5. **Make every alert actionable** — condition, severity, threshold, first response, and routing are mandatory fields; an alert without a first response is not run book content.
6. **Define severity levels by user/business impact** — keep definitions consistent across the support model (4.2), incident SLAs (10.1), and communication cadence (10.4); state who declares and who may upgrade/downgrade.
7. **Write procedures executable by a new operator** — exact steps, expected duration, decision points, and commands; put commands in 11.3/Appendix B and mark troubleshooting entries that have never been executed as untested.
8. **State rollback and database migration constraints explicitly** (7.5) and give the hotfix path (7.6) a never-skipped quality bar and a retroactive documentation obligation.
9. **Derive RTO/RPO and SLA/SLO targets from documents or questions — never invent them**; if no source exists, record the assumption with a validation action.
10. **Populate Sections 12–15 or mark n/a explicitly with a one-line rationale** — never leave recovery, maintenance, security operations, or transition silently empty.
11. **For Software Modernization, link the run book to the cutover runbook** (Project Plan §17.5) and record dual-running and legacy-support operations (Section 15).
12. **Write the Executive Summary (Section 1) last** — synthesize scope, criticality, service levels, support model, top risks, and the emergency starting point after all other sections are final.
13. **Complete Section 16 as the operational acceptance gate** — the readiness checklist (16.1) references every section plus the availability/live runbook tests; exit criteria (16.2) mirror it at area granularity; sign-off (16.3) requires all criteria met.
14. **Save the generated document** to an appropriate location, suggested: `documentation/runbook-operational-manual.md` unless the repository has an established docs folder.

#### Quality Checks Before Delivery

After generating the document, perform these self-checks:

- [ ] No `<!-- -->` placeholders remain (except the date, status, baseline, and sign-off fields that require human input).
- [ ] The component inventory (3.2) is complete — every `COMP-XXX` row has dependencies, blast radius, criticality, and SPOF marking; jobs/schedulers included.
- [ ] Every `ALERT-XXX` row has a condition, severity, threshold, first response, routing, and a matching `TS-XXX` troubleshooting row.
- [ ] Incident severity SLAs are deliverable by the support model and consistent across 4.2, 10.1, and 10.4.
- [ ] The escalation ladder (10.3) references the on-call contacts (4.3) and Appendix A, with a vendor path for external-cause incidents (3.3).
- [ ] Rollback (7.5) matches the actual deployment method and states database migration constraints; the hotfix path (7.6) has a never-skip bar.
- [ ] Backup/restore (12.1) states scope, schedule, restore steps, and the restore-test cadence; RTO/RPO (12.3) is stated with its source.
- [ ] Sections 12–15 are populated or explicitly marked n/a with rationale.
- [ ] The readiness checklist (16.1) covers all sections and the availability/live runbook tests; exit criteria (16.2) mirror it; sign-off (16.3) is reserved for humans.
- [ ] Appendix C indexes every `COMP/DEP/SLO/OPS/ALERT/TS/KI` ID used.
- [ ] Untested procedures are marked untested — never presented as verified.
- [ ] The Executive Summary accurately reflects the final content and states the emergency starting point.
- [ ] No contradictions exist between sections (if one is unavoidable, flag it explicitly in the document).
- [ ] Document History records the version, date, and author.

### Phase 4: Post-Generation Review

After the document is generated:

1. **Present the document** to the user.
2. **Highlight key judgments made** during generation — where the skill made interpretive calls (e.g., deriving severity definitions, confirming code-found monitoring as-is, deriving SLO fields from NFRs, classifying SPOFs), point them out so the user can verify.
3. **Present the inventory summary** — components, external dependencies, service levels, alerts, routine tasks, and known issues counts, with the incident severity and escalation ladder at a glance.
4. **Flag remaining uncertainties** — areas where information was insufficient and assumptions were made, the risk each assumption poses, and suggested validation activities.
5. **Offer to refine** any section the user wants to adjust.
6. **Suggest next steps** — rehearse one incident scenario per Section 11.1, execute the readiness checklist (16.1), collect sign-offs (16.3), baseline the document, and update Document History.

## Anti-Patterns to Avoid

- **Don't generate the document without asking questions** — the value is in the rigorous analysis and resolved ambiguities, not in filling a template.
- **Don't ask questions that existing documentation or code already answers** — read carefully and use available information directly.
- **Don't ask a single unprioritized giant question list, and don't drip questions one per turn** — batch by priority: [Critical] first, then [Important]; offer to proceed with stated assumptions for [Optional] items.
- **Don't invent components, dependencies, alerts, dashboards, or SLOs that are neither evidenced nor confirmed** — document what exists as-is, or record the target as an assumption with a validation action.
- **Don't leave alerts without first responses, severities, or routing** — an unactionable alert catalogue is the run book's most common failure.
- **Don't fabricate RTO/RPO targets, SLA/SLO numbers, severity definitions, or on-call schedules** — derive them from documents, the business case, or questions; never from imagination.
- **Don't treat recovery, maintenance, and security operations (Sections 12–14) as optional fillers** — they are the most commonly missing and most operationally critical content; if undocumented, they are top-priority questions.
- **Don't present untested procedures as verified** — mark troubleshooting entries and playbooks that have never been executed as untested.
- **Don't let the run book contradict the deployment reality found in code** — code-vs-docs conflicts are questions, not silent judgment calls.
- **Don't duplicate Environment Setup, Architecture, or SRS content** — reference the sources and extract only operationally relevant facts.
- **Don't leave the readiness checklist or sign-off empty or optional** — Section 16 is the document's acceptance mechanism.
- **Don't write the Executive Summary first** — write it last, after all inventories and procedures are final.

## Document Hierarchy Context

The Run Book builds upon and extracts facts from:

| Document | Relationship | Feeds Run Book |
|----------|-------------|----------------|
| **Environment Setup** | Defines stages, pipelines, gates, secrets, monitoring, backup/DR, support wiring | Yes — Sections 3.4, 5, 7.1, 8.1, 9, 12 |
| **Software Architecture** | Defines components, deployment model, hosting, and operations model | Yes — Sections 3.1, 3.2, 3.3 |
| **SRS / Requirements** | Defines NFRs, compliance, and integrations | Yes — Section 4.1 (SLOs), 5 (access/compliance), 3.3 (dependencies) |
| **Business Case** | Defines criticality, risk appetite, and operational investment | Yes — Section 1 (criticality), 12.3 (RTO/RPO), 14 (security posture) |
| **Test Concept** | Defines quality gates and operational readiness tests | Yes — Sections 7.2, 7.4, 16.1 (availability/live runbook tests) |
| **Project Plan** | Defines cutover runbook, hypercare, and knowledge transfer | Yes — Section 15 (transition/hypercare), 7.6 (hotfix during transition) |
| **Risk Profile** | Defines delivery and operational risks | Yes — Section 1 (top risks), 10 (incident readiness emphasis) |
| **ADRs / Postmortems / Existing Run Books** | Define operational decisions and incident learnings | Yes — Sections 10, 11 (playbooks and known issues) |

And it precedes and enables:

| Activity | Relationship |
|----------|-------------|
| **Go-live readiness** (`shipping-and-launch` skill) | The readiness checklist (16.1) and exit criteria (16.2) are the operational input to the launch gate |
| **CI/CD automation** (`ci-cd-and-automation` skill) | The deployment, rollback, and hotfix procedures (Section 7) specify the automation's operational behavior |
| **Observability work** (`observability-and-instrumentation` skill) | The dashboard and alert catalogue (Section 9) define what instrumentation must deliver |
| **Security hardening** (`security-and-hardening` skill) | Security operations (Section 14) and access/break-glass (Section 5) reference what hardening provides |
| **Steady-state operations** | Sections 4–14 are the day-to-day and incident operating reference; Section 16 is its acceptance gate |
