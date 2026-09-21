---
name: generate-environment-setup
description: Generates an evidence-based Environment Setup document using the repository template `templates/development/environment-setup.md`. This skill should be used when establishing the environments, repositories, collaboration platform, and CI/CD setup for a project or release and when core project documents (Architecture, SRS, Business Case, Test Concept) exist and must be analyzed to derive the canonical stages, promotion flow, VCS and collaboration inventories, pipelines, quality gates, prerequisites, and operations setup (DNS, secrets, networking, backup/DR, monitoring, support). Gaps, unclear statements, and contradictions are resolved by asking targeted open questions with suggested valid answers before generation.
---

# Generate Environment Setup

## Overview

Generate a complete, evidence-based Environment Setup document — the provisioning and acceptance baseline for a project's environments, repositories, collaboration spaces, and pipelines — by extracting environment-relevant facts from existing project documents and translating them into the canonical stage model, promotion flow, VCS and collaboration inventories, CI/CD pipeline definitions, quality gates, provisioning prerequisites, and operations setup.

The Environment Setup is the single source of truth that lets every team member find access, tools, and endpoints without tribal knowledge, and serves as the provisioning and acceptance baseline for DevOps / platform work. Its value comes from the rigor of the analysis and clarification, not from filling a template: the skill deeply analyzes all available information, detects gaps, unclear statements, and contradictions, and asks targeted open questions with suggested possible valid answers before generating anything.

## Activation

Use when the user asks to create, generate, or draft:

- An Environment Setup document or environment plan
- A staging/deployment environment documentation ("our environments", "our stages")
- A repository + collaboration + pipeline inventory
- A provisioning checklist or environment acceptance baseline

Primary evidence sources (in order of weight for environment facts):

- Software Architecture (components, deployment model, deployment nodes, hosting, technology stack, infrastructure resources)
- SRS/Requirements (NFRs → SLA/SLO targets, compliance requirements, integrations → partner connectivity)
- Business Case (constraints, budget, risk appetite, sponsor)
- Test Concept (quality gates — the CI/CD gates and go-live gate must align with these)
- Project scope / plan, risk profile, release plan, runbooks, ADRs
- Codebase and configuration evidence (build files, CI configs, IaC, `.env.example`, docker-compose)
- Existing environment documents, READMEs, and stakeholder/operations notes

## Instructions

### Phase 1: Information Gathering & Deep Analysis

1. **Read the template** at `templates/development/environment-setup.md` to understand the full structure, all 11 sections and their subsections, and the per-section guidance comments. Pay special attention to:
   - The ID schemes used across inventories — `REPO-XXX` (repositories, Section 5.1), `COL-XXX` (collaboration workspaces/channels, Section 6.2), `PIPE-XXX` (pipelines, Section 7.1), `G-XXX` (quality gates, Section 7.5), `PR-XXX` (provisioning checklist, Section 8.3). These IDs are cross-referenced between sections; they must be used unchanged.
   - The canonical terms (Section 2.3): Stage, Promotion, Quality Gate, Version Control Repository, Collaboration Platform, CI/CD Pipeline, IaC, SLO.
   - The explicit cross-references: Section 5 must align with the `git-workflow-and-versioning` skill if used; Section 7 quality gates must align with the Test Concept (Section 5, "Quality Gates"); PROD entry gates reference the go-live gate.
   - The stage model: the template prescribes the four stages DEV / TEST / INT / PROD unless the project justifies deviations — deviations are allowed but must be documented with the same per-stage template.
2. **Discover and read all existing project information:**
   - Search for architecture documents (`software-architecture*.md`, `*architecture*.md`, `adr*/*.md`, `*adr*.md`). Extract main components, deployment model, hosting approach, deployment nodes, infrastructure resources, and operations model.
   - Search for requirements (`software-requirements-specification*.md`, `*srs*.md`, `*requirements*.md`). Extract NFRs (availability, performance targets → PROD SLA/SLO fields), compliance/regulatory requirements (→ data privacy profiles, access controls), and external integrations (→ INT connectivity requirements).
   - Search for business case (`business-case*.md`). Extract constraints, budget, risk appetite, sponsor, and success criteria that shape the environment investment.
   - Search for test concept (`test-concept*.md`). Extract the quality gate definitions (Test Concept Section 5) that the CI/CD gates and go-live gate must align with, plus test environment prerequisites.
   - Search for project scope/plan (`project-scope*.md`, `project-plan*.md`), risk profile (`*risk-profile*.md`), release plan, and runbooks (`*runbook*.md`).
   - Search for configuration evidence that reveals the actual environment landscape:
     - Build/runtime files: `package.json`, `pom.xml`, `build.gradle`, `requirements.txt` — runtimes, build tooling
     - CI configs: `.github/workflows/*`, `azure-pipelines*.yml`, `.gitlab-ci.yml`, `Jenkinsfile` — existing pipelines to inventory as-is
     - IaC: `terraform/**`, `*.bicep`, `*.tf`, k8s manifests, `docker-compose.yml` — provisioning approach and per-stage resources
     - Secret/config handling: `.env.example`, `.env*` patterns, secret-manager references — configuration sources and secret store evidence
   - Search for existing environment documents (`environment-setup*.md`, `*environment*.md`) and README/docs folders. For a revision, adopt and extend rather than restart; record deltas in Document History.
   - Search for stakeholder and operations inputs: meeting notes, support/incident documentation, monitoring policies, on-call schedules.
3. **Classify the project type** based on available evidence (template Metadata field "Project Type"):
   - **Green Field**: new system from scratch — nothing exists yet; the document defines what must be provisioned.
   - **Brown Field**: existing system enhancement — environments, repos, and pipelines exist and must be documented as-is, with deltas identified.
   - **Software Modernization**: legacy replacement — environments exist on both sides; parity, dual-running, migration, and decommission must be addressed.
   - If a preceding document already classified the project type, adopt that classification unless new evidence contradicts it — note any contradiction as a Phase 2 question. If classification is ambiguous, note it as a [Critical] question.
4. **Map existing information to template sections.** For each of the 11 sections and their subsections, determine:
   - **Covered**: sufficient evidence exists to populate the section factually.
   - **Partially Covered**: information exists but is vague or incomplete (e.g., "the team handles prod" without roles; a single undefined "staging" stage).
   - **Gap**: no information exists.
   - **Contradiction**: sources conflict (e.g., architecture documents two stages but the business case budget assumes four; the template's example branch patterns differ from the project's actual workflow evidence).
5. **Perform deep environment-fact analysis.** Go beyond surface-level mapping:

   **Stage fact readiness (Section 4):** For every stage the project actually uses, check that purpose, target platform, deployment model, data privacy profile (synthetic / masked / real), refresh cadence, access controls, configuration sources, and observability are determinable. A stage without a data privacy profile or access control definition is 🔴 Not Ready — it silently permits personal data in DEV or uncontrolled PROD access. Check whether the default four-stage model applies or whether the project justifies a deviation (e.g., preview environments instead of TEST, UAT inside INT).

   **Promotion flow coherence (Section 4.3):** Every promotion row needs a trigger, automation level, approvals, quality gates, and rollback strategy. "Validated builds are promoted" without measurable gates is Not Ready. Rollback strategy must exist for every transition, not just PROD.

   **Gate alignment with the Test Concept (Section 7.5):** The CI/CD gates (PR merge gate, test stage gate, INT gate, go-live gate) must trace to the Test Concept's quality gate definitions. If a Test Concept exists, align names, criteria, and blocking semantics; unaligned or conflicting gate definitions are 🟡/🔴. If no Test Concept exists, document gates as assumptions and add a validation prerequisite — do not invent gate criteria silently.

   **Branch-to-stage mapping coherence (Sections 5.2 ↔ 4.3):** The branching inventory must map branches/tags to stages consistently with the promotion flow (e.g., which branch deploys to which stage, which tags release to INT/PROD). Reconcile the template's example branch patterns (feature/, bugfix/, release/, hotfix/) with the project's actual workflow: if the project follows the `git-workflow-and-versioning` skill's recommended trunk-based model (short-lived feature branches into `main`, always deployable), document the project's real model and note the delta from the template's example patterns — do not force-fit gitflow patterns that the team does not use.

   **Cross-source consistency:** Architecture's deployment model vs business-case hosting constraints vs SRS integration requirements. INT must treat configuration parity with PROD as a requirement (template guidance). PROD SLA/SLO fields must derive from SRS NFRs where they exist.

   **Security and compliance readiness (Sections 7.4, 9.1, 9.2, 9.3, Metadata):** Secret stores per stage and rotation process, TLS certificate sources and renewal, network topology and partner connectivity (especially INT), classification (Public/Internal/Confidential), and regulations (privacy → data profiles, change management → approval flows).

   **Operations readiness (Sections 9.4–9.6):** Monitoring/alerting/on-call, backup/DR with RTO/RPO targets, support channels and incident severities, runbook locations. These are the most commonly completely undocumented areas — treat any 🟡 here as 🔴 priority for questions.

   **Implicit facts from configuration evidence:** An existing `.env.example` implies configuration sources and a secrets convention; docker-compose implies runtimes/databases → connection-string secret requirements; existing CI config files imply pipelines that must be inventoried as-is in Section 7 rather than invented. Surface these implied facts explicitly and ask the user to confirm, challenge, or refine them.

6. **Build a readiness map** — for each section, tag readiness:
   - 🟢 **Ready**: detailed, specific, sufficient to write evidence-based content.
   - 🟡 **Partially Ready**: exists but vague, incomplete, or inconsistent across sources.
   - 🔴 **Not Ready**: missing, unquantified, or contradictory — cannot be documented without clarification.

   Sections with 🔴 or 🟡 readiness are priority candidates for Phase 2 questions.

### Phase 2: Clarification Questions

Before generating the document, ask the user targeted questions for every 🔴 Not Ready, 🟡 Partially Ready, Gap, or Contradiction area identified in Phase 1.

#### Question Design Principles

- **Ask open questions** that invite thoughtful responses and deeper thinking — not yes/no questions.
- **Always suggest 2–3 possible valid answers** for each question to help the user think through the options and to demonstrate understanding of the domain.
- **Contextualize each question** — briefly explain why the information matters for the Environment Setup and what happens if it remains unanswered (e.g., "Without per-stage data profiles, DEV could accumulate personal data with no reset strategy, and TEST/INT masking requirements would be unverifiable").
- **Group questions by template section** so the user can address them systematically.
- **Prioritize questions** — mark questions as:
  - **[Critical]**: Blocks generation — the section cannot be filled without this information (e.g., which CI/CD tool, what hosting model, whether the four-stage model applies).
  - **[Important]**: Affects the quality and completeness of the document — it can be drafted but will contain gaps or unverifiable claims.
  - **[Optional]**: Refines the document; can be documented as an assumption with a validation plan.
- **Reference the source** of the gap or contradiction (e.g., "The architecture documents only dev and prod stages, but the Test Concept requires a pre-production validation stage").
- **Surface implicit facts** from configuration evidence and ask the user to confirm, challenge, or refine them.
- **Do not ask questions that can be answered by reading existing documentation** — if the answer exists in a file already read, use it directly.
- **Distinguish information that must be resolved now from information that can be documented as assumptions with validation plans** — for [Optional] questions, offer to proceed with a stated assumption.
- **Batch by priority**: lead with [Critical] questions, then [Important]; do not present one unprioritized giant list, and do not drip questions one at a time over many turns.

#### Question Template

For each question, use this format:

---

**[Priority] Section X.Y — [Topic]**

[Context: why this matters for the Environment Setup and what happens if unanswered]

[The open question]

Suggested answers:
- *Option A*: [description and implications for the document]
- *Option B*: [description and implications for the document]
- *Option C*: [description and implications for the document]
- *Custom*: [your own answer]

---

#### Minimum Required Questions (All Project Types)

These must be resolved (or explicitly documented as assumptions with validation plans) before generation:

1. What are the canonical stages — do DEV / TEST / INT / PROD apply, or does the project deviate, and why?
2. What is the hosting/deployment model per stage — cloud provider and regions, on-prem, or hybrid?
3. Which VCS host and repositories exist (or must be created), and which branch/tag deploys to which stage?
4. Which collaboration platform and tenant is used, and what workspaces/channels are needed?
5. Which CI/CD tool is used and which pipelines exist (or must be created) from commit to production?
6. Who owns each stage and who approves promotions — roles first, names where known?
7. What are the data privacy constraints per stage (synthetic / masked / real data, prohibited data)?
8. Where do secrets live and what is the rotation process?
9. What classification (Public / Internal / Confidential) and compliance constraints apply?
10. What monitoring, backup/DR (RTO/RPO), and support/on-call expectations exist?
11. Who fills the Metadata roles — Sponsor, Product Owner, Project Manager, Technical Lead, DevOps Lead, Security Lead?

**Green Field additional questions:**
- What must be provisioned from zero — there are no existing repos, workspaces, or pipelines to inventory, so the document defines the target set?
- How are stages provisioned — IaC, manual setup, or platform defaults?
- What service plans / instance sizes are intended per stage (cost is unbounded without this)?

**Brown Field additional questions:**
- What existing stages, repositories, and pipelines must be documented as-is, including undocumented tribal knowledge (workarounds, shadow environments, shared credentials)?
- What changes versus what is preserved — which environment facts are stable and which are being modified?
- What backward-compatibility constraints apply to existing environments (partner systems pointing at fixed URLs, pinned service accounts)?

**Software Modernization additional questions:**
- What is the parity target between legacy and target environments — identical stage structure, or intentionally different?
- Are dual-running environments needed during transition, and how is data consistency maintained between old and new environments?
- What is the environment/data migration and decommission plan, and what is the rollback strategy if cutover fails?

#### Worked Example Questions

**Example Question (Gap — Stage Model Deviation)**

---

**[Critical] Section 4 — Canonical Stage Model**

The architecture documents only a development and a production deployment, but the template's canonical model is DEV / TEST / INT / PROD, and the Test Concept assumes a pre-production validation stage for regression and UAT. If the stage model is not settled, Sections 4.2, 4.3, 7.1 (pipeline targets), and 7.5 (gates per stage) cannot be generated consistently, and the promotion flow will not match how the team actually ships.

Which stage model does the project use?

Suggested answers:
- *Option A*: "Full four-stage model — DEV, TEST, INT, PROD. TEST runs automated suites, INT holds UAT and partner integration with prod-like masked data. This matches the template default and the Test Concept's gate sequence."
- *Option B*: "Three stages — DEV, TEST (combined QA + pre-production), PROD. UAT happens in TEST with masked prod-like data; the TEST gate covers both regression and UAT sign-off. Fewer environments, lower cost, but prod-parity testing is weaker."
- *Option C*: "Two stages plus preview environments — trunk-based deploys to a shared dev on merge, per-PR preview deployments replace TEST, production is manual. The document notes this as a justified deviation from the template's four-stage default; gates collapse into the PR merge gate and the go-live gate."
- *Custom*: [your own answer]

---

**Example Question (Vague — Approvals Without Owners)**

---

**[Important] Sections 4.2.4 / 4.3 / 7.3 — Production Deployment Approvals**

Existing documents say "the team deploys to production" but name no approvers, no change window, and no break-glass procedure. Without this, the PROD entry gates (Section 4.2.4), the INT→PROD promotion row (Section 4.3), and the deploy-prod approvals (Section 7.3) are unverifiable, and the change-management requirement implied by the SRS compliance section cannot be met.

Who approves production deployments, and under what change process?

Suggested answers:
- *Option A*: "Change board approves: DevOps Lead + Product Owner, within a defined weekly change window (e.g., Tuesday 10:00–12:00 CET). Break-glass: Tech Lead + DevOps Lead jointly, documented post-hoc. This satisfies the change-management requirement in the SRS."
- *Option B*: "Tech Lead sign-off suffices — small team, low blast radius. Approvals recorded in the pipeline's approval step; break-glass is the Tech Lead alone with mandatory incident report within 24h."
- *Option C*: "Automatic deployment after the go-live gate passes (all sign-offs collected in INT) — no additional manual approval at PROD entry, but a 15-minute post-deployment monitoring window with automatic rollback on alert. The document must then define the go-live gate as the human checkpoint."
- *Custom*: [your own answer]

---

**Example Question (Contradiction — Branching Model)**

---

**[Important] Section 5.2 — Branching and Versioning Model**

The template's example branch patterns (feature/, bugfix/, release/, hotfix/ with release/* → INT and tags → PROD) follow a gitflow-style model, but the project evidence (CI triggers on push to `main`, short-lived feature branches merged within days, no release branches in git history) indicates trunk-based development — which is also the recommended default in the `git-workflow-and-versioning` skill. Section 5.2 must map branches to stages consistently with the promotion flow in Section 4.3, so the model must be settled before generating.

Which branching and versioning model should the document inventory?

Suggested answers:
- *Option A*: "Document trunk-based as-is: short-lived feature/* branches (no direct stage deploys), `main` → DEV/TEST deploys, version tags `vX.Y.Z` → INT/PROD. Keep the template's table structure but record the trunk-based patterns; note the delta from the template's example patterns explicitly."
- *Option B*: "Adopt the template's example patterns going forward: introduce release/* branches for release candidates and hotfix/* for emergency fixes, with the corresponding protection rules. The document becomes the target state, and the delta from current practice is a migration note in the provisioning checklist."
- *Option C*: "Hybrid: trunk-based for regular work, release branches only when a stabilization cycle is needed. Document both patterns with the trigger conditions that switch between them (e.g., release branch created when INT testing spans more than one sprint)."
- *Custom*: [your own answer]

---

**Example Question (Implicit Fact — Secrets Store Gap)**

---

**[Optional] Sections 7.4 / 9.2 — Secret Storage Location**

Configuration evidence shows an `.env.example` file, but no secret store is documented anywhere. The Environment Setup must state where pipeline and runtime secrets actually live (Sections 7.4, 9.2) and this feeds provisioning item PR-008 ("Secrets created in secret store and referenced"). Without an answer, the secret tables would be placeholders.

Where do pipeline and runtime secrets live, and who owns rotation?

Suggested answers:
- *Option A*: "Platform-native secret store per stage (e.g., GitHub Actions secrets for CI, cloud key vault for runtime). Rotation: DevOps Lead, quarterly, emergency rotation within 24h of exposure. This is the pragmatic default for a small team."
- *Option B*: "Central organization vault (e.g., HashiCorp Vault / corporate Key Vault) — all stages reference it. Rotation is centrally managed; the project registers its secrets with the vault owners. Slightly more setup, but satisfies stricter compliance expectations."
- *Option C*: "No store yet — document 'no secret store in place' as the current state, add a provisioning item to introduce one before first PROD release, and record the interim manual handling rules (no secrets in code, `.env` not committed, masked in logs) as temporary constraints."
- *Custom*: [your own answer]

---

### Phase 3: Document Generation

Once all critical and important questions are resolved, generate the Environment Setup document.

#### Generation Rules

1. **Use the template structure exactly** — follow `templates/development/environment-setup.md` section by section (1–11 plus Document History), including all subsections and their tables.
2. **Replace all `<!-- -->` placeholders** with project-specific content derived from the analysis and the user answers; fill every table with concrete, specific content.
3. **Keep the document evidence-based** — use explicit references to source documents (e.g., "per Architecture Section 8, deployment model is …"). Where information is missing, state the assumption explicitly with an owner and a validation action rather than inventing facts.
4. **Use the template's ID schemes unchanged** (`REPO-XXX`, `COL-XXX`, `PIPE-XXX`, `G-XXX`, `PR-XXX`) and keep inventories cross-referenced: gate G-XXX rows reference the promotion rows in Section 4.3 and the PIPE-XXX pipelines that enforce them; provisioning items PR-XXX cover every inventory item.
5. **Make quality gates measurable and aligned with the Test Concept** — blocking vs non-blocking, measurable criteria, and a promotion-flow tie-in. If no Test Concept exists, record the gates as assumptions and add a validation prerequisite to align them with a Test Concept before first release.
6. **Align Section 5.2 with the project's confirmed branching model** — keep the template's table structure; record the project's actual patterns and, where they deviate from the template's example patterns, note the deviation rather than force-fitting.
7. **Write the Executive Summary (Section 1) last** — synthesize scope, stages in use, VCS and collaboration at a glance, CI/CD summary, and main risks/constraints after all other sections are final.
8. **Populate PROD SLA/SLO fields from SRS NFRs where available**; otherwise state assumptions and add validation prerequisites.
9. **Mark n/a explicitly in Section 9 subsections** that do not apply — never leave them silently empty.
10. **Save the generated document** to an appropriate location, suggested: `documentation/environment-setup.md` unless the repository has an established docs folder.

#### Quality Checks Before Delivery

After generating the document, perform these self-checks:

- [ ] No `<!-- -->` placeholders remain (except the date, status, baseline, and sign-off fields that require human input).
- [ ] All four stage detail tables (Section 4.2) are populated with the confirmed stage model, or a justified deviation is documented.
- [ ] The promotion flow (4.3) is consistent with the CD pipeline stages (7.3) and the quality gates (7.5) — every transition has trigger, automation, approvals, gates, and rollback.
- [ ] Quality gates are measurable, blocking/non-blocking is stated, and gate names/criteria align with the Test Concept where one exists.
- [ ] The repository inventory (5.1) is consistent with the branching model (5.2) — every stage that deploys from a branch/tag is mapped.
- [ ] The collaboration workspaces (6.2) cover the notification sources from CI/CD (7) and operations (9.5).
- [ ] The provisioning checklist (8.3) covers every inventory item — repositories, workspaces, stages, pipelines, secrets, monitoring.
- [ ] Every Section 9 subsection is populated or explicitly marked n/a with a one-line rationale.
- [ ] The exit criteria (10.1) reference the actual inventories generated in Sections 4–9.
- [ ] The Executive Summary accurately reflects the final content.
- [ ] No contradictions exist between sections (if one is unavoidable, flag it explicitly in the document).
- [ ] Document History records the version, date, and author.

### Phase 4: Post-Generation Review

After the document is generated:

1. **Present the document** to the user.
2. **Highlight key judgments made** during generation — where the skill made interpretive calls (e.g., selecting the stage model, deriving approvals, adopting a branching model, deriving SLO fields from NFRs), point them out so the user can verify.
3. **Present the inventory summary** — stages, repositories, collaboration workspaces, pipelines, quality gates, and provisioning item counts, with the promotion flow at a glance.
4. **Flag remaining uncertainties** — areas where information was insufficient and assumptions were made, the risk each assumption poses, and suggested validation activities.
5. **Offer to refine** any section the user wants to adjust.
6. **Suggest next steps** — execute the provisioning checklist (Section 8.3), collect sign-offs (Section 10.2), run each pipeline end-to-end once, then baseline the document and update Document History.

## Anti-Patterns to Avoid

- **Don't generate the document without asking questions** — the value is in the rigorous analysis and resolved ambiguities, not in filling a template.
- **Don't ask questions that existing documentation already answers** — read carefully and use available information directly.
- **Don't ask a single unprioritized giant question list, and don't drip questions one per turn** — batch by priority: [Critical] first, then [Important]; offer to proceed with stated assumptions for [Optional] items.
- **Don't invent environments, pipelines, or repositories that are neither evidenced nor confirmed** — document existing facts as-is, or record targets as provisioning items.
- **Don't force the default four stages when the project justifies a deviation** — document the deviation and its justification with the same per-stage rigor.
- **Don't leave gates unmeasurable** — "no critical defects" needs a severity definition and a measurement source; every gate needs measurable criteria.
- **Don't force the template's example branch patterns onto a team that works differently** — reconcile with the `git-workflow-and-versioning` skill's recommendation and the project's actual practice.
- **Don't duplicate architecture or SRS content** — reference the sources and extract only environment-relevant facts.
- **Don't leave Section 9 subsections silently empty** — populate them or mark n/a explicitly.
- **Don't skip the provisioning checklist or the sign-off sections** — they are the document's acceptance mechanism.
- **Don't write the Executive Summary first** — write it last, after inventories, gates, and provisioning items are final.
- **Don't treat operations topics (monitoring, backup/DR, on-call, support) as optional fillers** — they are the most commonly missing and most operationally critical content; if undocumented, they are top-priority questions.

## Document Hierarchy Context

The Environment Setup document builds upon and extracts facts from:

| Document | Relationship | Feeds Environment Setup |
|----------|-------------|------------------------|
| **Software Architecture** | Defines components, deployment model, hosting, and infrastructure | Yes — Sections 3 (overview), 4 (stage target platforms), 9.3 (networking) |
| **SRS / Requirements** | Defines NFRs, compliance, and integrations | Yes — PROD SLA/SLO (4.2.4), data privacy profiles, INT connectivity, access controls |
| **Business Case** | Defines constraints, budget, and risk appetite | Yes — hosting constraints, stage investment scope, sponsor (Metadata) |
| **Test Concept** | Defines quality gates and test environment needs | Yes — CI/CD gates and go-live gate (7.5), test stage usage (4.2.2) |
| **Project Plan / Scope / Risk Profile** | Define delivery sequencing and risks | Yes — provisioning phases (Appendix B), constraints and risks (Section 1) |

And it precedes and enables:

| Activity | Relationship |
|----------|-------------|
| **CI/CD setup** (`ci-cd-and-automation` skill) | The pipeline inventory and gates (Section 7) are the specification the automation implements |
| **Git workflow adoption** (`git-workflow-and-versioning` skill) | The branching inventory (Section 5) records the model the workflow skill prescribes |
| **Environment provisioning** | Section 8.3 is the working checklist during setup; Section 10 is its acceptance gate |
| **Release operations** | Stage details, rollback strategies, and on-call/support setup (Sections 4, 9) are the operational reference |
