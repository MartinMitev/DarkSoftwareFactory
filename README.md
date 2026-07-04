# Dark Software Factory

The **Dark Software Factory** is a curated set of **skills**, **templates**, and lightweight **workflows** that enable very high automation across the Software Development Life Cycle (SDLC).

All artifacts are organized by SDLC phase:

- Analysis
- Design
- Development
- Testing
- Deployment
- Maintenance

Skills are designed to be **composable**: you can run a full phase end-to-end, or invoke an individual skill to generate a single artifact.

---

## Repository Structure

| Path | What it contains |
|------|------------------|
| `skills/` | Phase-grouped skills (each skill has a `SKILL.md`) |
| `templates/` | Phase-grouped document templates used by `generate-*` skills |
| `documentation/` | Target location for generated project artifacts (recommended) |
| `references/` | Optional reference material (standards, policies, regulations, etc.) |
| `external_sources/` | Vendored or imported external materials (read as upstream sources) |

Note: some skills may include an `assets/` folder with canonical snippets/templates and optional `scripts/`.

---

## Core Idea

The Dark Software Factory aims to reduce SDLC friction by:

- Standardizing artifact structures via templates (structure + semantics).
- Encoding repeatable work into stable skills.
- Maintaining traceability between outputs across phases (e.g., requirements → architecture → test concept).

The guiding principle:

- **Skills** should remain relatively stable across projects and customers.
- **Templates** are expected to be adapted per customer/project (terminology, governance, compliance, document structure).

---

## Skill Naming Convention

- `execute-*` skills define a workflow to execute a complete SDLC phase (or a major slice of it).
- `generate-*` skills produce a key SDLC artifact and always reference a template that defines the structure and semantics of the output.

Examples from this repository:

- `skills/analysis/execute-analysis-phase/SKILL.md`
- `skills/analysis/generate-business-case/SKILL.md` (uses `templates/analysis/business-case.md`)
- `skills/design/generate-software-architecture/SKILL.md` (uses `templates/design/software-architecture.md`)
- `skills/testing/generate-test-concept/SKILL.md` (uses `templates/testing/test-concept.md`)

---

## Included Skills (By SDLC Phase)

This list reflects the current repository contents under `skills/`.

### Analysis

- `execute-analysis-phase`
- `generate-viability-study`
- `generate-business-case`
- `generate-project-scope`
- `generate-user-stories`
- `generate-software-requirements-specification`
- `generate-project-plan`
- `idea-refine`
- `interview-me`

### Design

- `generate-software-architecture`

### Development

- `api-and-interface-design`
- `code-review-and-quality`
- `code-simplification`
- `doubt-driven-development`
- `frontend-ui-engineering`
- `git-workflow-and-versioning`
- `incremental-implementation`
- `observability-and-instrumentation`
- `performance-optimization`
- `security-and-hardening`
- `source-driven-development`
- `spec-driven-development`
- `test-driven-development`

### Testing

- `browser-testing-with-devtools`
- `debugging-and-error-recovery`
- `generate-project-risk-profile`
- `generate-test-concept`

### Deployment

- `ci-cd-and-automation`
- `documentation-and-adrs`
- `shipping-and-launch`

### Meta

- `context-engineering`

---

## Templates

Templates live in `templates/<phase>/...` and are referenced by `generate-*` skills.

Available templates include:

### Analysis

- `templates/analysis/viability-study.md`
- `templates/analysis/business-case.md`
- `templates/analysis/project-scope.md`
- `templates/analysis/user-stories.md`
- `templates/analysis/software-requirements-specification.md`
- `templates/analysis/project-plan.md`

### Design

- `templates/design/software-architecture.md`

### Testing

- `templates/testing/test-concept.md`
- `templates/testing/project-risk-profile.md`
- `templates/testing/functional-test-cases.md`
- `templates/testing/technical-test-cases.md`
- `templates/testing/non-functional-test-cases.md`
- `templates/testing/documentation-test-cases.md`
- `templates/testing/availability-live-test-cases.md`

---

## How To Use

### 1. Pick a Phase (Or a Single Artifact)

- If you want to run analysis end-to-end, start with: `skills/analysis/execute-analysis-phase/`.
- If you want a specific artifact, use the corresponding `generate-*` skill.

### 2. Customize Templates for Your Context

Templates are the primary customization point.

Typical template adaptations:

- Replace organization-specific governance terminology (roles, committees, approvals).
- Add sections required by internal policy or external regulation.
- Update classifications and metadata fields.
- Adjust quality gates, evidence expectations, and traceability tables.

Keep the skill logic stable; evolve templates to match the customer/project.

### 3. Store Outputs in `documentation/`

Most skills recommend saving generated artifacts under `documentation/` (or `docs/` if your repository standard is different). This repo contains `documentation/` as the default place for project outputs.

---

## Principles

- Evidence-based generation: prefer real project inputs; avoid inventing requirements.
- Explicit gaps: missing information should become questions, assumptions, risks, or prerequisites.
- Traceability: outputs should be cross-referencable across phases.
- Small, composable building blocks: combine skills to fit the project shape.

---

## Notes

- The `.kilo/` folder (if present in a consumer repo) is typically configuration for Kilo commands/agents/skills. In this repository it is ignored by default (see `.gitignore`).
- `external_sources/` contains imported upstream materials; treat these as references rather than core project content.
