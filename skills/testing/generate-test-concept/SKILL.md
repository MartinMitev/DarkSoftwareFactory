---
name: generate-test-concept
description: Generates an evidence-based Software Test Concept document using the repository template `templates/testing/test-concept.md`. This skill should be used when establishing the testing approach for a release or project and when core project documents (Business Case, User Stories, SRS/Requirements, and Software Architecture) exist and must be analyzed to derive test targets, strategy, quality gates, formal test-driven requirements, prerequisites, and internal regulation considerations.
---

# Generate Test Concept

## Overview

Generate a complete Test Concept by extracting test-relevant information from key project documents and translating it into test targets, test strategy, quality gates, coverage models (Functional View and Business Object Lifecycle View), and traceability evidence.

## Activation

Use when the user asks to create/generate a test concept, test strategy document, test plan (concept level), testing approach, quality gates definition, or release testing readiness documentation.

Primary evidence sources (in order):
- Business Case (constraints, success criteria, risk appetite)
- User Stories (features, flows, acceptance criteria, sequencing)
- SRS/Requirements (functional clusters, NFRs, compliance requirements)
- Architecture (components, integrations, deployment/ops model)

## Workflow

### Phase 1: Load Template and Discover Inputs

1. Read the Test Concept template at `templates/testing/test-concept.md`.
2. Discover candidate source documents across the workspace:
   - Business Case (`business-case*.md`, `*business case*.md`)
   - User Stories (`user-stories*.md`, `*user stories*.md`)
   - Requirements (`software-requirements-specification*.md`, `*srs*.md`, `*requirements*.md`)
   - Architecture (`software-architecture*.md`, `*architecture*.md`, `adr*/*.md`)
   - Optional: risk profile (`*risk-profile*.md`), release plan, runbooks
3. Select canonical versions (prefer baselined/approved/latest revised).
4. If any key document is missing:
   - Proceed, but record gaps as risks/constraints in the Test Concept.
   - Do not invent requirements; propose explicit assumptions and validation actions.

### Phase 2: Deep Analysis and Derivation

#### 2.1 Derive Test Targets

From User Stories + SRS:
- Compile the feature/capability inventory (Functional View).
- Identify critical user journeys (golden paths).

From Architecture:
- Identify major components/services/modules as test targets.
- Identify integrations and protocols (API, events, batch).
- Identify surfaces (web/mobile/API/jobs) and supported platforms.

From Business Case:
- Identify critical business outcomes and SLAs that imply critical test targets.

Populate template sections:
- 3.1 SUT
- 3.2 Test Target Inventory
- 3.3 Supported Platforms
- 3.4 Integrations

#### 2.2 Derive Business Object Lifecycle View

From SRS + Architecture + User Stories:
- Identify business objects (domain entities) that have states and transitions.
- For each business object:
  - Define states (including invariants) and transitions (including triggers/guards/side effects).
  - Define invalid transitions that must be prevented.
- If lifecycle definitions are not present in source docs:
  - Derive a first-pass lifecycle model from story flows and domain rules.
  - Mark the lifecycle model as an assumption and add a validation prerequisite.

Populate template section 8:
- 8.1 business object inventory
- 8.2 lifecycle model per object
- 8.3 lifecycle coverage matrix
- 8.4 lifecycle test case template usage guidance

#### 2.3 Derive Test Strategy

From SRS NFRs + Architecture:
- Map NFRs to required test levels and test types (performance, security, accessibility, recovery).
- Define required test design techniques (decision tables, state transition testing).

From User Stories:
- Determine the balance between E2E vs component/integration tests based on volatility and critical flows.

From Business Case constraints:
- Adjust strategy for timelines, budget, and risk appetite (e.g., increase automation for regression safety).

Populate template section 4:
- 4.1 objectives
- 4.2 test levels/responsibilities
- 4.3 design techniques
- 4.4 automation strategy
- 4.5 risk-based prioritization

#### 2.4 Derive Quality Gates

From architecture and delivery model:
- Define PR/merge gate requirements (unit tests, lint, SAST, dependency scanning).
- Define RC gate requirements (integration + contract + regression + lifecycle coverage).
- Define go-live gate requirements (sign-offs, compliance evidence, rollback readiness).

From Business Case:
- Reflect risk appetite (e.g., no critical security findings; minimum SLOs met).

Populate template section 5:
- Gate definitions (blocking vs non-blocking)
- Severity rules
- Exit criteria by test level (include lifecycle coverage threshold)

#### 2.5 Derive Formal Requirements, Prerequisites, and Regulations

From SRS and internal policy references:
- Identify requirements that must be evidenced by tests (compliance controls, audit logs, retention, security controls).

From Architecture:
- Identify prerequisites: environments, test data, access, observability, stubs/mocks, CI/CD readiness.

From Business Case / organization governance:
- Identify internal regulations impacting testing (secure SDLC, change management, privacy).

Populate template section 6:
- Formal requirements (FR-TEST-xxx)
- Prerequisites (PR-xxx)
- Internal regulations (REG-xxx) and required evidence artifacts

#### 2.6 Derive Traceability and Coverage Evidence

1. Build the Feature-to-Test mapping plan:
   - Ensure each feature has at least one test case planned.
   - Ensure critical features are covered by automated regression.
2. Build the lifecycle coverage plan:
   - Ensure each state has invariant tests.
   - Ensure each valid transition has tests.
   - Ensure invalid transitions have negative tests.
3. Map SRS requirements to features and business objects.

Populate sections 7-9.

### Phase 3: Generate the Test Concept Document

1. Follow `templates/testing/test-concept.md` section-by-section.
2. Replace all `<!-- -->` placeholders with project-specific content.
3. Keep the document evidence-based:
   - Use explicit references to the source documents.
   - If information is missing, document assumptions and convert them to prerequisites.
4. Write the Executive Summary last.

### Phase 4: Quality Checks

Before delivering the generated document, verify:
- No placeholders remain (except date/status fields intended for humans).
- Section 7 covers all features with a concrete inventory and mapping approach.
- Section 8 defines business objects with states and transitions (or explicitly marks gaps and prerequisites).
- Quality gates are measurable and tied to CI/release steps.
- Formal requirements are linked to evidence artifacts.
- Prerequisites are actionable, owned, and time-bound.

## Output

Save the generated document to a project-appropriate location. Default to `documentation/test-concept.md` unless the repository has an established docs folder.

## Resources

### assets/
Contains the canonical template used for generation.

### scripts/
Optional: no scripts are required for this skill.

### references/
Optional: store organization-specific quality gate policies or compliance mappings.

