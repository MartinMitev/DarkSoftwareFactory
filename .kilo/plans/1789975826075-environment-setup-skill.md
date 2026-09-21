# Plan: Environment Setup Generation Skill

## Goal

Create a new skill `skills/development/generate-environment-setup/SKILL.md` that generates an Environment Setup document based on the repository template `templates/development/environment-setup.md`. The skill must deeply analyze all existing project information, detect gaps, unclear statements, and contradictions, and ask targeted open questions with suggested possible valid answers before generating the document.

## Target Files

- `skills/development/generate-environment-setup/SKILL.md` (new; `skills/development/` already exists)
- No other files modified (template already exists; README/template-list updates out of scope unless requested)

## Design Decisions (resolved)

1. **Skill name: `generate-environment-setup`** — matches the repo's `generate-*` document-generation skills (`generate-test-concept`, `generate-software-architecture`, `generate-software-requirements-specification`, `generate-project-plan`).
2. **Format follows `skills/analysis/generate-software-requirements-specification/SKILL.md`**, the repo's canonical pattern for "deep analysis + clarification questions with suggested valid answers" — which is exactly the user's requirement. Not the simpler `generate-test-concept` format (that one only records gaps, never asks).
3. **Template referenced directly** (`templates/development/environment-setup.md`) — no duplication into an `assets/` folder (SRS skill pattern).
4. **YAML frontmatter** (`name`, `description`) like `generate-test-concept`, for skill discovery.
5. **Generated document default output**: `documentation/environment-setup.md` unless the project has an established docs location.
6. **Questions asked as one consolidated clarification round after analysis completes** (SRS pattern: Phase 1 analysis → Phase 2 prioritized questions), not drip-fed one-by-one. Open questions, never yes/no, each with 2–3 suggested valid answers + *Custom*, grouped by template section, priority-tagged.

## Template Context (what the skill generates)

`templates/development/environment-setup.md` (v1.0) defines 11 sections + Document History:

1. Executive Summary (template comment: "Write this section last")
2. Purpose, Scope, Definitions — canonical terms: Stage, Promotion, Quality Gate, Version Control Repository, Collaboration Platform, CI/CD Pipeline, IaC, SLO
3. Project Overview — system, components, deployment model, tech stack, operations model, audience
4. Stages (Environments) — default four stages DEV / TEST / INT / PROD; per-stage detail tables (purpose, target env, deployment model, data profile, access controls, config sources, quality gates, observability; PROD adds entry gates + SLA/SLO); promotion flow table (4.3)
5. Version Control Repositories — inventory (REPO-XXX), branching/versioning model (5.2 guidance: feature/, bugfix/, release/, hotfix/), protection/review rules (5.3); guidance: "align with the git-workflow-and-versioning skill if used"
6. Collaboration Platform — platform overview, workspaces/channels (COL-XXX), artifact linking, notifications/alerts
7. CI/CD Pipelines — inventory (PIPE-XXX), CI jobs (build/unit/lint/SAST-SCA), CD stages with approvals/rollback, variables & secrets, quality gates (G-XXX, blocking vs non-blocking); guidance: "Align quality gates with the Test Concept (Section 5)"
8. Prerequisites & Access Management — accounts/roles, licenses/tools, provisioning checklist (PR-XXX with status)
9. Additional Setup — DNS/certificates, secrets management & rotation, networking/connectivity, backup/DR (RTO/RPO), monitoring/alerting/on-call, support & incident mgmt; every subsection marked n/a explicitly if not applicable
10. Acceptance & Sign-off — exit criteria summary, sign-off table (PO, Tech Lead, DevOps Lead, Security Lead, PM)
11. Appendices — A: setup checklist, B: provisioning phases snapshot, C: troubleshooting notes

Repo conventions: blockquote header (Template Version / Last Updated / Document Status), Metadata table, anchored TOC, HTML comment guidance blocks per section, `<!-- -->` placeholder cells, inventory IDs.

## Skill Content Outline (what the implementer writes)

### Frontmatter

```
---
name: generate-environment-setup
description: Generates an evidence-based Environment Setup document using the repository template `templates/development/environment-setup.md`. This skill should be used when establishing the environments, repositories, collaboration platform, and CI/CD setup for a project or release and when core project documents (Architecture, SRS, Business Case, Test Concept) exist and must be analyzed to derive the canonical stages, promotion flow, VCS and collaboration inventories, pipelines, quality gates, prerequisites, and operations setup (DNS, secrets, networking, backup/DR, monitoring, support). Gaps, unclear statements, and contradictions are resolved by asking targeted open questions with suggested valid answers before generation.
---
```

### Structure

1. **# Generate Environment Setup**
2. **## Overview / Description** — generate a complete Environment Setup (the provisioning and acceptance baseline for environments, repos, collaboration, and pipelines) by extracting environment-relevant facts from project documents; document value proposition: single source of truth, no tribal knowledge, provisioning baseline for DevOps work.
3. **## Activation** — when the user asks to create/generate an environment setup document, environment plan, staging/deployment setup documentation, repository + collaboration + pipeline inventory, or provisioning checklist. Primary evidence sources (in order): Architecture, SRS, Business Case, Test Concept, plus codebase/config evidence.
4. **## Instructions**
   - **### Phase 1: Information Gathering & Deep Analysis**
     1. Read template at `templates/development/environment-setup.md` — all 11 sections, per-section guidance comments, ID schemes (REPO-XXX, COL-XXX, PIPE-XXX, G-XXX, PR-XXX), and cross-references (Test Concept Section 5 quality gates; `git-workflow-and-versioning` skill for Section 5).
     2. Discover and read all existing project information (search patterns):
        - Architecture (`software-architecture*.md`, `*architecture*.md`, `adr*/**`) — components, deployment model, deployment nodes, hosting, tech stack, infrastructure resources
        - SRS (`software-requirements-specification*.md`, `*srs*.md`) — NFRs (availability/SLO targets → PROD SLA/SLO fields), compliance, integrations (partner systems → INT connectivity)
        - Business Case (`business-case*.md`) — constraints, budget, risk appetite, sponsor
        - Test Concept (`test-concept*.md`) — quality gates Section 5 (CI/CD gates + go-live gate must align with these)
        - Project scope / plan (`project-scope*.md`, `project-plan*.md`), risk profile, release plan, runbooks
        - Configuration evidence: `package.json`/`pom.xml`/`build.gradle`, `docker-compose.yml`, `.env.example`, `.github/workflows/*`, `azure-pipelines*.yml`, `.gitlab-ci.yml`, `terraform/**`, `*.bicep`, k8s manifests, `Dockerfile` — reveal VCS host, CI tool, IaC, secret handling, runtimes
        - Existing environment docs (`environment-setup*.md`, `*environment*`), README, ADRs, docs — for revision cases adopt/revise rather than restart
        - Stakeholder/ops inputs: meeting notes, support/incident docs, monitoring policies
     3. Classify project type (Green Field / Brown Field / Software Modernization); adopt preceding documents' classification unless contradicted; mark contradictions as Phase 2 questions.
     4. Map existing information to template sections and tag readiness — 🔴 Not Ready (missing/unquantified → priority questions), 🟡 Partially Ready (vague, e.g. "the team handles prod" without roles; "staging" as a single undefined stage), 🟢 Ready.
     5. Perform deep environment-fact analysis beyond surface mapping:
        - **Stage fact readiness**: per stage — target platform, data privacy profile (synthetic/masked/real), refresh cadence, access controls, config sources, observability. Does the project justify the default four stages, or does the team use a different set? (Template allows deviations but demands documented justification.)
        - **Promotion flow coherence**: DEV→TEST→INT→PROD triggers, approvals, rollback strategies — measurable, not asserted ("validated builds" without gates is Not Ready).
        - **Gate alignment with Test Concept**: CI/CD gates (7.5) and go-live gates trace to the Test Concept's gate definitions; unaligned or missing test-concept gates = 🟡/🔴.
        - **Branch→stage mapping coherence**: Section 5.2 must map branches/tags to stages consistently with 4.3 promotion flow; reconcile the template's branch-pattern guidance (feature/bugfix/release/hotfix) against the project's actual workflow; if the project uses the `git-workflow-and-versioning` skill's recommended trunk-based model, align the inventory with it and flag the delta from the template's example patterns rather than force-fitting gitflow.
        - **Cross-source consistency**: architecture deployment model vs business-case hosting constraints vs SRS integration requirements; PROD configuration-parity requirement for INT (Section 4.2.3 guidance).
        - **Security & compliance readiness**: secret stores and rotation, certificates, classification (Public/Internal/Confidential), regulations impacting environment setup (privacy → data profiles, change management → approvals).
        - **Operations readiness** (most often completely undocumented → 🔴): monitoring/on-call, backup/DR RTO/RPO, support/incident process, runbooks.
        - **Implicit facts from config evidence**: `.env.example` implies config sources; docker-compose implies runtimes/databases → connection-string secret requirements; CI config files imply existing pipelines to inventory (Section 7 must document as-is rather than invent).
     6. Build the readiness map; 🔴/🟡 sections are Phase 2 candidates.
   - **### Phase 2: Clarification Questions**
     - Ask the user targeted open questions for every 🔴 Not Ready, 🟡 Partially Ready, Gap, or Contradiction area before generating. Adopt the SRS skill's question design principles, adapted:
       - Open questions; never yes/no.
       - Always suggest 2–3 possible valid answers (+ *Custom*) with implications for the document.
       - Contextualize: why the fact matters and what remains undefined if unanswered (e.g., "Without per-stage data profiles, DEV could accumulate personal data with no reset strategy, and TEST/INT masking requirements would be unverifiable").
       - Group by template section; reference the source of the gap/contradiction; don't ask what already-read documents answer.
       - Distinguish resolve-now ([Critical]/[Important]) from proceed-with-assumption-plus-validation-plan ([Optional]).
       - Surface implicit facts (config evidence, ADRs) and ask to confirm/challenge/refine.
       - Batch by priority: lead with [Critical], then [Important]; offer to proceed with stated assumptions for [Optional].
       - Priority definitions: **[Critical]** blocks generating the section (e.g., which CI/CD tool, what cloud/hosting, does the four-stage model apply); **[Important]** affects completeness/quality (approvals, refresh cadence, secret rotation); **[Optional]** refinements (workspace channel naming conventions, license versions).
     - Question template (same format as SRS skill): `[Priority] Section X.Y — [Topic]` + context + open question + `Suggested answers:` A/B/C/Custom.
     - Minimum required questions (all project types) — the [Critical] set:
       1. What are the canonical stages, and do DEV/TEST/INT/PROD apply (or does the project deviate, and why)?
       2. What is the hosting/deployment model (cloud provider + regions, on-prem, hybrid) per stage?
       3. Which VCS host and repositories exist, which branch/tag deploys to which stage?
       4. Which collaboration platform and tenant?
       5. Which CI/CD tool and pipelines exist, from commit to production?
       6. Who owns each stage and approves promotions (roles; names where known)?
       7. What are the data privacy constraints per stage?
       8. Where do secrets live and what is the rotation process?
       9. What classification/compliance constraints apply?
       10. What monitoring, backup/DR, and support expectations exist?
       11. Who fills the Metadata roles (Sponsor, PO, PM, Tech Lead, DevOps Lead, Security Lead)?
     - Project-type-specific minimums:
       - **Green Field**: what must be provisioned from zero (no existing repos/workspaces/pipelines to inventory); provisioning approach (IaC vs manual vs platform defaults); service plans per stage.
       - **Brown Field**: existing stages/repos/pipelines documented as-is; undocumented environment tribal knowledge; what changes vs what is preserved; backward-compatibility constraints on environments.
       - **Software Modernization**: parity between legacy and target environments; dual-running environment needs; environment/data migration and decommission plan; rollback if cutover fails.
     - Include 4 worked example questions (same style as SRS skill's Examples):
       1. **[Critical] Gap — Stage model deviation**: architecture documents only dev + prod; template default is four stages. Ask which stage set applies (suggest: A full four-stage model, B dev/test/prod with UAT inside TEST, C two-stage trunk-based with preview environments; implications for sections 4/7).
       2. **[Important] Vague — Approvals**: "changes are deployed by the team" without approvers. Ask who approves INT→PROD (suggest: A PO + change board with defined window, B Tech Lead sign-off, C automatic after gate with break-glass; implications for 4.2.4, 4.3, 7.3).
       3. **[Important] Contradiction — Branching model**: template guidance shows gitflow patterns (release/*, hotfix/*) but project evidence (CI triggers on main, short-lived branches) indicates trunk-based. Ask which model the inventory documents (suggest: A document trunk-based as-is and note template-pattern delta, B adopt the template's example patterns going forward, C document current model now + target model transition).
       4. **[Optional] Implicit fact — Config evidence reveals secrets gap**: `.env.example` exists but no secrets store is documented. Ask where runtime secrets live (suggest: A platform-native secret store, B organization vault, C no store yet — document as a provisioning item with rotation deferred; implications for 7.4, 9.2, PR-XXX items).
   - **### Phase 3: Document Generation**
     - Generation rules:
       1. Follow the template section-by-section (1–11 + Document History), including all subsections and their tables.
       2. Replace all `<!-- -->` placeholders with evidence-based project content; every table filled with concrete content.
       3. Evidence-based: explicit references to source documents (e.g., "per Architecture Section 8, deployment is …"); missing info → stated assumptions with owners + validation actions, traceable to the user answers.
       4. Use the template's ID schemes unchanged (REPO-XXX, COL-XXX, PIPE-XXX, G-XXX, PR-XXX) so inventories are cross-referenced consistently (e.g., gate G-002 references promotion row TEST→INT and PIPE-XXX items).
       5. Quality gates measurable, blocking vs non-blocking, tied to promotion flow and aligned with Test Concept gates; if Test Concept absent, document gates as assumptions + validation prerequisites.
       6. Align section 5.2 with the project's actual (or confirmed) branching model; where it deviates from the template's example patterns, keep the template structure and record the project-specific patterns.
       7. Executive Summary last (scope, stages, VCS + collaboration at a glance, CI/CD summary, risks/constraints).
       8. Populate PROD SLA/SLO fields from SRS NFRs where available; otherwise assumptions.
       9. Mark n/a explicitly in Section 9 subsections per the template guidance.
       10. Save to `documentation/environment-setup.md` unless the project has an established docs location.
     - Quality checks before delivery (checklist): no placeholders remain (except date/status/sign-off fields for humans); all four stage detail tables populated with the confirmed stage model; 4.3 promotion rows consistent with 7.3 CD stages and 7.5 gates; 5.1 repos consistent with 5.2 branch→stage mapping; 6.2 workspaces cover notification sources from 7/9; 8.3 provisioning checklist covers every inventory item (repos, workspaces, stages, pipelines, secrets, monitoring); Section 9 subsections all populated or explicitly n/a; exit criteria (10.1) reference the actual inventories; Executive Summary reflects final content; no contradictions between sections.
   - **### Phase 4: Post-Generation Review**
     - Present the document; highlight interpretive judgments (stage-model decisions, gate priorities, assumption-derived fields); summarize inventories (stages, repos, workspaces, pipelines, gates, provisioning items); flag remaining uncertainties + assumption risks + validation activities; offer refinement; suggest next steps (execute Section 8.3 provisioning checklist, round sign-off, first end-to-end pipeline run, baselining + Document History update).
5. **## Anti-Patterns** (adapted from SRS skill):
   - Don't generate without asking questions — the analysis and clarification are the value, not filling a template.
   - Don't ask what already-read documentation answers.
   - Don't ask a single unprioritized giant question list — batch by priority, offer to proceed with assumptions for [Optional].
   - Don't invent environments, pipelines, or repos not evidenced or confirmed — document as-is or as provisioning items.
   - Don't force the default four stages when the project justifies a deviation — document the deviation and its justification.
   - Don't leave gates unmeasurable ("no critical defects" without definition) — every gate needs measurable criteria.
   - Don't duplicate architecture/SRS content — reference and extract environment-relevant facts only.
   - Don't mark Section 9 subsections empty — populate or explicitly n/a.
   - Don't skip the provisioning checklist or sign-off sections — they are the document's acceptance mechanism.
   - Don't write the Executive Summary first.
6. **## Document Hierarchy Context** — table: Architecture/SRS/Business Case/Test Concept precede the Environment Setup (facts extracted from them); Environment Setup precedes/provides the provisioning baseline for CI/CD setup, environment provisioning, and release operations; note the SRS skill, architecture skill, and `ci-cd-and-automation` skill as upstream/sibling references.

## Implementation Steps

1. Create `skills/development/generate-environment-setup/SKILL.md` with the full content outlined above (frontmatter + all six structural elements).
2. Keep wording style consistent with existing skills (imperative instructions, guidance comments style, prioritized question template, worked examples, anti-pattern tables).
3. Do NOT modify the template or any other file.

## Validation

- Frontmatter name/description match repo skill conventions; description mentions the template path.
- Skill references the exact template path `templates/development/environment-setup.md` and its real section numbering and ID schemes (verified against the template file).
- Cross-references are real: Test Concept Section 5 quality gates (verify in `templates/testing/test-concept.md`), `git-workflow-and-versioning` skill name, `ci-cd-and-automation` skill name.
- Terminology consistency: Stage/Promotion/Quality Gate definitions match template Section 2.3; project types (Green Field / Brown Field / Software Modernization) match template Metadata field.
- All example questions follow the prioritized question template with 2–3 suggested answers + Custom.
- Markdown lint/anchor consistency (section headings match references).

## Open Questions

None material. Recommended defaults (user-overridable):
- Skill name: `generate-environment-setup`
- Skill file: `skills/development/generate-environment-setup/SKILL.md`
- Generated doc default: `documentation/environment-setup.md`
- Question round: consolidated Phase 2 after analysis (SRS pattern), with [Critical]/[Important]/[Optional] priorities
