---
name: unit-test-generation
description: Generates requirement-driven and user-story-driven unit tests for each module of an existing codebase. The skill deeply analyzes the SRS's functional and non-functional requirements, user stories with acceptance criteria, business rules, the software architecture's building blocks, the test concept, and the code itself — then generates unit tests for every module with high code coverage and systematic coverage of critical, boundary, and special cases. Every unit test traces to at least one requirement or user-story acceptance criterion. Tests assert the behavior the requirements demand, never the behavior the implementation happens to have. When gaps, ambiguities, or code-vs-requirement contradictions are detected, the skill asks targeted open questions with suggested valid answers before proceeding.
---

# Skill: Unit Test Generation

## Description

Generates a complete, rigorous unit test suite for each module of an existing codebase, driven by the project's requirements and user stories — not by the implementation. The skill deeply analyzes all available project information — the SRS's functional requirements, business rules, and testable non-functional requirements, user stories with their acceptance criteria, the software architecture's building blocks and module interfaces, the test concept's levels, techniques, and quality gates, user-story priority and criticality inputs, and the code itself with its existing test infrastructure — to generate unit tests for every module with high code coverage and systematic coverage of critical and special cases.

The skill's central principle: **tests are derived from requirements and user stories, never from the implementation.** A test written from the code enshrines the code's current behavior — including its bugs. A test written from the requirement specifies the behavior the code must have, and exposes every place the code falls short. The skill asserts the behavior the requirements demand; where the code contradicts the requirement, it reports a defect finding rather than silently adjusting the test.

When gaps, unclear statements, or contradictions are detected — in the requirements, between documents, or between the code and its requirements — the skill asks targeted open questions with suggested valid answers before proceeding.

## Activation

When the user requests to generate unit tests, create a unit test suite, add test coverage for modules, generate requirement-driven tests, cover code with tests from requirements, or audit existing test coverage against requirements.

## Instructions

### Phase 1: Information Gathering & Deep Analysis

1. **Orient in the codebase first:**
   - Detect the language and frameworks (`package.json`, `pom.xml`, `build.gradle`, `pytest.ini`/`pyproject.toml`, `go.mod`, `Gemfile`, `*.csproj`, etc.).
   - Detect the idiomatic test framework and runner (Jest/Vitest, JUnit 5, pytest, Go testing, xUnit/NUnit, RSpec...) and any existing test configuration.
   - Locate existing test directories, naming conventions, fixtures, builders, and factories.
   - Detect coverage tooling and current thresholds/configs (Istanbul/c8, JaCoCo, coverage.py, go test -cover, dotnet coverlet...).
   - Locate CI test steps (`.github/workflows`, `Jenkinsfile`, `.gitlab-ci.yml`) — the tests must pass in CI conditions.
   - Run the existing test suite and coverage report as the baseline.

2. **Read the requirements sources:**
   - Search for the SRS (`*requirements*`, `*srs*`). This is the **most critical** source. Extract:
     - Functional requirements (FR-xxx) with their acceptance criteria and validation rules — these become behaviors.
     - Business rules (BR-xxx) with their decision tables — each rule column becomes a test row.
     - Use cases (UC-xxx) with main, alternative, and exception flows — flows become behavior sequences.
     - Non-functional requirements (NFR-xxx) — identify which are testable at unit level (validation precision/rounding, formatting, i18n, pure-function latency budgets, security validation rules) and which belong to integration/E2E levels.
     - Interface and data requirements (IR-/DR-) — the data contracts the tests must respect.
   - Search for user stories (`*user-stories*`, `documentation/user-stories/`). Extract `US-XXX` IDs with acceptance criteria `US-xxx.AC-x`, noting their case classes (*Functional / Error / Edge / NFR*) and priorities — acceptance criteria are directly translatable into tests.
   - Search for project scope (`*project-scope*`) — scope boundaries and MoSCoW priorities order the modules.
   - Search for the risk profile (`*risk-profile*`) and business case — criticality ranking for "critical cases".

3. **Read the software architecture document (`*architecture*`):**
   - The building block view (Section 6): module responsibilities and the **module interfaces** — what each block exposes is the unit-under-test boundary. Tests drive the public API surface of each building block, never its internals.
   - Quality scenarios (Section 11): behaviors that quality demands (error handling, resilience, precision) — testable ones become unit tests.
   - Cross-cutting concepts (Section 9): validation, error handling, security, and resilience patterns imply unit-testable behaviors in every module that applies them.
   - 🟤🔵: which building blocks are unchanged, modified, replaced, or retired — unchanged blocks may only need regression coverage; modified blocks need full requirement-driven coverage.

4. **Read the test concept (`test-concept.md`) if present:**
   - Test levels and responsibilities (§4.2): what belongs at unit level vs. integration/E2E — generated tests must respect this split and record mappings for anything delegated upward.
   - Test design techniques (§4.3): equivalence partitioning, boundary value analysis, decision tables, state transition testing — these structure the case derivation.
   - Quality gates and exit criteria (§5.1, §5.3): coverage thresholds and unit-test gate requirements — generated suite targets must align.
   - Traceability (§9.1): the requirements-to-tests mapping this skill's output must feed.

5. **Build the module inventory map.** For each module (from architecture building blocks + code structure):
   - **Responsibility**: from the architecture's building block description.
   - **Implemented requirements/user stories**: from the architecture's traceability, or inferred by matching requirement keywords to module code — every inference is flagged as an assumption for Phase 2.
   - **Public API surface**: exported functions/classes/services — the unit boundary.
   - **Current test status**: none / partial / suite, with existing tests' quality noted.
   - **Criticality**: High / Medium / Low (from risk profile, business case, user-story volume, and 🟤🔵 change status).
   - **Dependencies**: what the module calls — determining where test doubles are legitimate (module boundaries vs. external systems).

6. **Derive behaviors per requirement.** Convert each in-scope FR/UC/US.AC into concrete, observable behaviors and tag each with its source ID and case class (*Functional / Error / Edge / NFR*):
   - **Golden path**: the main success scenario, verbatim from the requirement.
   - **Boundary values**: every numeric/range/length constraint the requirement states — test at min, min+1, max-1, max, and outside (boundary value analysis).
   - **Equivalence classes**: every valid and invalid input class the requirement's validation rules define.
   - **Business-rule combinations**: every decision-table row for applicable BRs — each combination of conditions and its expected action.
   - **State transitions**: every valid transition from use cases/workflows, plus every **invalid transition that must be prevented** (negative tests).
   - **Error contract**: what the requirement specifies for each failure — error type, message, recovery — the test asserts this contract exactly.
   - **Special cases**: empty, null/None, zero, max-length/overflow, duplicates, unicode/emoji, locale-specific formats (per NFRs), first-use/empty-repository states, idempotent re-execution, concurrent modification and timeout/rollback paths where the SRS or architecture states them.

7. **Scan for code-vs-requirement contradictions.** For requirements whose implementation is inspectable, compare expected behavior with actual behavior. Log every mismatch as a candidate defect finding — mismatching behaviors become failing tests written to the requirement, not passing tests written to the code. This scan is the skill's highest-value analysis.

8. **Build the readiness map** — per module, tag:
   - 🟢 **Ready**: requirements/user stories for the module are known, specific, and traceable.
   - 🟡 **Partially Ready**: some requirements exist but are vague, incomplete, or the module↔requirement mapping is partly inferred.
   - 🔴 **Not Ready**: no requirements or acceptance criteria found for the module — tests cannot be requirement-driven without clarification (legacy/undocumented modules are the typical 🔴 case).

   🔴 and 🟡 modules are priority candidates for Phase 2 questions.

### Phase 2: Clarification Questions

Before generating tests, ask targeted questions for every **Partially Ready**, **🔴 Not Ready**, contradiction, or ambiguity area identified in Phase 1.

#### Question Design Principles

- **Ask open questions** that invite thoughtful responses — not yes/no questions.
- **Always suggest 2–3 possible valid answers** for each question, with implications for the test suite.
- **Contextualize each question** — explain why it matters and what happens if unanswered (e.g., "Without a coverage target, the skill cannot decide how much of the module's glue code is intentionally excluded and delegated to integration tests, and coverage becomes an arbitrary number").
- **Lead with contradiction questions** — code-vs-requirement conflicts are the most consequential findings and must be resolved before generating tests, or the suite will encode the wrong behavior.
- **Group questions by module and priority.**
- **Prioritize questions:**
  - **[Critical]**: Blocks test generation for the affected modules — the tests would be arbitrary, requirement-less, or would encode disputed behavior.
  - **[Important]**: Affects suite quality, coverage targets, or traceability. Tests can be generated but will have weak justification or gaps.
  - **[Optional]**: Refines the suite; can proceed as a documented assumption with a validation plan.
- **Reference the source** of every gap or contradiction (requirement ID, document section, code file/line).
- **Do not ask questions the code or documents already answer** — use available information directly.
- **Offer to proceed with stated assumptions** for [Optional] items.

#### Contradiction Question Template

---

**[Critical] Module X — Code-vs-Requirement Contradiction: [FR-xxx / US-xxx.AC-x]**

The requirement states [expected behavior], but the implementation in [file/line] does [actual behavior]. A requirement-driven test for this behavior will fail. The suite cannot be generated without deciding which behavior is authoritative — generating tests from the code would enshrine the contradiction instead of exposing it.

Which behavior is authoritative for Module X's tests?

Suggested answers:
- *Option A*: "The requirement is authoritative — generate the failing test and report the mismatch as a defect finding. The fix flows through the test-driven-development Prove-It pattern (the failing test is the reproduction test)."
- *Option B*: "The requirement is outdated — the code implements the agreed behavior. Flag FR-xxx for update through requirement change control, and generate the test against the corrected requirement once updated."
- *Option C*: "The deviation is intentional and accepted — document it as an accepted deviation in the traceability matrix, and generate the test against the agreed behavior with a comment referencing the deviation decision."
- *Custom*: [your own answer]

---

#### General Question Template

---

**[Priority] Module X — [Topic]**

[Context: Why this matters for the suite and what happens if unanswered]

[The open question]

Suggested answers:
- *Option A*: [description and implications for the suite]
- *Option B*: [description and implications for the suite]
- *Option C*: [description and implications for the suite]
- *Custom*: [your own answer]

---

#### Minimum Required Questions

**All projects** must resolve these before generation:

- Which modules are in scope, in what order (all modules, criticality-ranked, or specific modules)?
- What are the coverage targets per module — line and branch percentages, and are they aligned to the test concept's quality gates if present? (Default proposal: ≥ 80% line, ≥ 75% branch, 100% of golden paths and error paths; heavy-I/O adapters excluded and delegated to integration level.)
- What are the test placement and naming conventions? (Follow existing project convention; propose the stack's idiom if none exists.)
- What is the test data strategy — builders/fixtures/factories vs. inline literals? (DAMP guidance: builders acceptable only when they increase clarity.)
- For 🔴 modules (no traceable requirements): how should they be handled — see below.
- For 🟤🔵: which modules are frozen (regression-only characterization tests) vs. in scope for requirement-driven tests?

**🔴 Legacy/undocumented modules — the decision set:**

- *Option A*: "Reconstruct requirements from observable behavior — write characterization tests that pin current behavior, clearly marked in the traceability matrix as behavior-derived (not requirement-derived), and log a follow-up to formalize requirements. Coverage improves; bugs stay hidden until requirements are formalized."
- *Option B*: "Defer — exclude the module from this generation round and log it as a coverage gap with a remediation plan (requirement reconstruction workshop, story refinement). No requirement-less tests are generated."
- *Option C*: "Treat as defect-risk — generate characterization tests AND a defect-risk report for the module, prioritizing a requirements audit for its most business-critical functions."
- *Custom*: [your own answer]

### Phase 3: Test Generation

Once all critical and important questions are resolved, generate the unit tests.

#### Generation Rules

1. **One test = one behavior.** Each test verifies exactly one requirement-derived behavior. Tests that combine behaviors are split.
2. **Every test is traceable.** The test name or an adjacent comment references its source ID — requirement behavior in the name where the convention allows (e.g., `it('rejects order when credit limit is exceeded (FR-012)')`, `it('keeps remaining quantity after partial fulfillment (US-014.AC-2)')`), source ID in a comment otherwise. Untraceable tests are rejected in review.
3. **Expected behavior comes from the requirement.** Assertions state what the SRS/user story/architecture demands — never what the code currently does. The skill never reads implementation internals to decide assertions.
4. **AAA structure.** Arrange (requirement-relevant state), Act (the public API call under test), Assert (the requirement's outcome). One assertion per concept; split assertions that verify different behaviors.
5. **Test the public API surface only.** The unit boundary is the module's interface from the architecture's building block view. Never test private methods or internal state. No interaction assertions except where the architecture/requirement mandates a boundary behavior (e.g., NFR "must publish event X on order completion" — the event publication is the required behavior, not an implementation detail).
6. **Test doubles: real > fake > stub > mock.** Use the simplest double that works. Doubles are legitimate only at boundaries the architecture defines: external systems, slow/non-deterministic/side-effecting dependencies (clock, email, external APIs, persistence at module boundaries). Use an architecture-defined fake where one exists; never mock the module under test's internals.
7. **Cover every derived case class.** Per requirement: golden path, every boundary value, every equivalence class, every decision-table row, every valid and invalid state transition, and the exact error contract. Error and edge paths are mandatory — a requirement fully tested on its happy path is not fully tested.
8. **Parameterize systematically without hiding case IDs.** Parameterized tests keep each case class named and traceable (named cases or case tables), so the traceability matrix stays exact.
9. **NFR mapping at unit level.** Testable NFRs (precision/rounding, formatting, i18n, validation latency budgets with CI-appropriate tolerance) become unit tests with their NFR ID; unit-untestable NFRs (end-to-end latency, availability, penetration) are recorded with their target integration/E2E level in the traceability matrix.
10. **DAMP over DRY.** Tests read like a specification — each test is self-contained and understandable without tracing shared helpers. Builders/factories acceptable when they increase clarity, never when they hide the scenario.
11. **No flaky constructs.** No sleeps, no real wall-clock dependencies (use injectable time), no network, no inter-test order dependence, no shared mutable state. Every test passes in isolation and in any order.
12. **No anti-patterns.** No snapshot abuse, no tests of third-party framework behavior, no assertion-free coverage-chasing tests, no duplicated E2E coverage at unit level.
13. **Run the generated tests.** Tests against conforming code must pass. Failing tests are investigated: requirement violation (report as defect finding — do not adjust the test) or analysis error (correct the test). **Never weaken an assertion to make the suite green.**
14. **Iterate to the coverage targets.** After the requirement-driven cases are complete, run the coverage report; every gap is either (a) a missed requirement-derived case — derive and add it, (b) justified glue code — documented as excluded with its integration-level mapping, or (c) dead code — reported as a finding, not tested.
15. **Produce the traceability matrix.** Map every FR/UC/BR/NFR/US.AC in scope → test case IDs, and reverse: every generated test → source ID. Include per-module coverage vs. targets, accepted deviations, deferred 🔴 modules, and unit→integration NFR mappings. Suggested location: `documentation/unit-test-traceability.md`, aligned with the test concept's §9.1 format when the test concept exists.
16. **Save tests per project convention** — existing test directories and naming; if none, the framework's idiom (e.g., `tests/` for pytest, `src/**/__tests__/` for Jest, colocated `*_test.go` for Go).

#### Per-Module Generation Workflow

For each in-scope module, in criticality order:

1. Load the module's derived behaviors (Phase 1.6) and the resolved decisions (Phase 2).
2. Generate the test file(s) with the module's describe-block per public API group.
3. Run the new tests; investigate and resolve every failure per Rule 13.
4. Run module coverage; close gaps per Rule 14.
5. Record the module's rows in the traceability matrix before moving to the next module.

#### Quality Checks Before Delivery

- [ ] Every generated test traces to at least one source ID (FR/UC/BR/NFR/US.AC).
- [ ] Every in-scope requirement maps to at least one test — zero-coverage requirements are flagged with reasons.
- [ ] No test asserts implementation internals, private state, or interaction sequences (except architecture-mandated boundary behaviors).
- [ ] Every failure path stated in the requirements has a test asserting the exact error contract.
- [ ] Every decision-table row for in-scope BRs has a test.
- [ ] Every valid state transition has a test; every invalid transition has a negative test.
- [ ] Boundary values are tested at the constraint edges stated in the requirements.
- [ ] No test depends on execution order, real time, network, or shared mutable state; the suite is deterministic.
- [ ] Test doubles are used only at architecture-defined boundaries; the preference order (real > fake > stub > mock) is respected.
- [ ] All tests pass (conforming code) — every remaining failure is a documented defect finding or open question, not a skipped test.
- [ ] No tests were skipped, disabled, or weakened to make the suite pass.
- [ ] Coverage meets the agreed targets per module, or every gap is justified (glue → integration level with mapping, or dead-code finding).
- [ ] The traceability matrix is complete, includes accepted deviations and deferred 🔴 modules, and aligns with the test concept's §9.1 where present.
- [ ] The full existing suite still passes — no regressions introduced.
- [ ] The suite runs green in CI conditions (commands verified).

### Phase 4: Verification & Post-Generation Review

After generation:

1. **Run the full suite** (new + existing) and report: generated test count, pass/fail status, per-module coverage vs. targets, runtime.
2. **Present the requirement coverage summary** — every in-scope FR/UC/BR/NFR/US.AC mapped to its tests; flag requirements with zero tests and the reason for each.
3. **Present the defect findings** — every code-vs-requirement mismatch discovered: module, requirement ID, expected vs. actual, severity (from criticality ranking), and suggested fix path (TDD Prove-It pattern). These findings are the skill's highest-value output — a suite that only goes green has exposed nothing.
4. **Flag assumptions and mappings** — inferred module↔requirement mappings, unit→integration NFR delegations, excluded glue code with rationale, and 🔴 modules deferred with their remediation plan.
5. **Highlight interpretive judgments** — derived edge cases not explicitly stated in requirements, chosen doubles at boundaries, prioritization calls. Point them out for user verification.
6. **Offer to refine** any module's suite, targets, or conventions.
7. **Suggest next steps** — defect remediation via `test-driven-development` (Prove-It), integration test generation for delegated levels, updating the test concept's traceability section (§9.1), wiring coverage gates into CI quality gates (§5.1), requirement change-control for outdated requirements.

## Examples

### Example Question (Contradiction — Code-vs-Requirement)

---

**[Critical] Module OrderValidation — Code-vs-Requirement Contradiction: FR-012**

FR-012 states: "The system shall reject an order when the requested quantity exceeds the customer's remaining credit limit, with a 422 error specifying the exceeded amount." The implementation in `order-validation.ts` (lines 88–104) rejects the order with a generic 500 Internal Server Error and no exceeded-amount detail. A requirement-driven test asserting the 422 contract will fail.

Which behavior is authoritative for the OrderValidation tests?

Suggested answers:
- *Option A*: "The requirement is authoritative — generate the failing test asserting the 422 contract with the exceeded-amount detail, and report the mismatch as a High-severity defect finding (clients depend on error contracts; a 500 hides a validation error and triggers incorrect retry behavior). The fix flows through the TDD Prove-It pattern."
- *Option B*: "The requirement is outdated — the API contract was changed to 500-with-retry semantics after the SRS was baselined. Flag FR-012 for update through requirement change control; once corrected, generate the test against the agreed behavior."
- *Option C*: "Split decision — the 422 status is correct and required, but the exceeded-amount detail is an intentional deviation for data-minimization reasons (avoiding credit-limit exposure in error payloads). Document the accepted deviation in the traceability matrix and generate the test asserting 422 without the amount."
- *Custom*: [your own answer]

---

### Example Question (Gap — Business Rule Without Decision Table)

---

**[Important] Module PricingService — BR-003 Discount Stacking Rule Has No Decision Table**

The SRS defines BR-003 "only one discount type per order, the highest applicable discount wins" and lists five discount types (loyalty, volume, seasonal, employee, promotional) — but provides no decision table of condition combinations, and no stated priority order among the five types. The tests need concrete expected outcomes for each combination; with five discount types and a stacking prohibition, there are 26 non-trivial combinations whose expected "highest" winner is ambiguous without a priority definition.

What is the discount priority order that defines the "highest applicable discount" for each combination?

Suggested answers:
- *Option A*: "Priority order: employee > promotional > seasonal > loyalty > volume (business rationale: fixed commitments beat flexible ones). The tests assert each type individually, every pairwise combination (10 rows), and the full five-way combination — 16 decision-table rows total, all traced to BR-003. This priority order should be added to BR-003 through change control."
- *Option B*: "No fixed order — resolve by value: the discount with the highest percentage (or amount) wins for each order. Tests use the value-resolution rule: each combination's winner is computable, so assert the winner per row and include equal-value tie-breaks (first-matched type by a stated enumeration order). Confirm the tie-break order."
- *Option C*: "The rule is narrower than it reads — in practice only loyalty and volume can co-occur (the other types are mutually exclusive by business process, which the SRS doesn't state). Tests cover the 3 loyalty/volume combinations plus each type individually; the broader matrix is deferred with a documented assumption and a validation action to confirm the mutual-exclusion claim."
- *Custom*: [your own answer]

---

### Example Question (🔴 Legacy Module — No Traceable Requirements)

---

**[Critical] Module LegacyInvoiceCalculator — No Requirements Found**

The module inventory maps `LegacyInvoiceCalculator` as 🟡🔴: it implements invoice total calculation (high criticality — it produces financial documents), but no requirement, business rule, or user story defines its behavior. The SRS predates the module; the code contains significant undocumented rounding and tax logic. Tests cannot be requirement-driven from the available sources.

How should the LegacyInvoiceCalculator suite be handled?

Suggested answers:
- *Option A*: "Reconstruct requirements from observable behavior — generate characterization tests that pin the current calculation logic (including the rounding and tax edge cases the code actually implements), trace them to a `BEHAVIOR-DERIVED` marker instead of a requirement ID, and log a follow-up action to formalize the calculation rules as BRs. Coverage is restored; bugs remain hidden until formalization — log that risk explicitly."
- *Option B*: "Audit first, test after — schedule a requirements reconstruction workshop with finance stakeholders before any tests are generated. The module is deferred this round with a documented coverage gap and remediation owner. Rationale: characterization tests on a financial calculator may enshrine long-standing miscalculations that audit would catch first."
- *Option C*: "Hybrid — generate characterization tests now for the 10 highest-traffic calculation paths (protection against regressions during the upcoming refactor 🟤) AND open a High-priority defect-risk report for the rounding/tax logic, with a stakeholder audit as the remediation. Trace the 10 paths as behavior-derived; defer the long tail to the audit."
- *Custom*: [your own answer]

---

### Example Question (Coverage Target Calibration — I/O-Heavy Module)

---

**[Important] Module ReportExportAdapter — Coverage Targets for I/O Glue**

The module combines pure report-calculation logic with heavy I/O: file-system streaming, third-party PDF library calls, and SFTP upload. Applying the default targets (≥ 80% line, ≥ 75% branch) to the whole module would force mocking the PDF library and file streaming — producing tests that verify mock behavior, not requirement behavior (NFR-R02 "reports render per the formatting NFRs" is about content, not streaming). The test concept (§4.2) assigns streaming and upload to integration level.

What are the coverage targets for ReportExportAdapter?

Suggested answers:
- *Option A*: "Split the boundary: extract/target the pure calculation core with full targets (≥ 85% line, ≥ 80% branch — financial formatting demands it, traced to NFR-R01/R02 formatting rules: currency precision, date formats, page-break rules at data boundaries). Exclude the streaming/upload glue from unit targets with a documented mapping to integration tests (test-concept §4.2 alignment). The architecture's building-block interface (calculation exposed separately from transport) makes this split legitimate without refactoring."
- *Option B*: "Full targets with architecture-defined fakes — build an in-memory fake of the PDF library and file system at the module boundary (architecture fake, not a mock), and apply the standard targets to the whole module. Higher suite confidence that composition works; cost: maintaining the fakes, which the architecture does not yet provide — flag that as a prerequisite."
- *Option C*: "Reduced targets module-wide (≥ 60% line) accepting the mock-heavy approach for I/O paths. Not recommended — flag the trade-off explicitly: interaction tests on mocked libraries verify mock behavior and provide low regression protection for the formatting NFRs the module exists to satisfy."
- *Custom*: [your own answer]

---

## Anti-Patterns to Avoid

- **Don't derive tests from the implementation** — reading the code to decide assertions produces tests that enshrine current behavior, including bugs. The requirement decides the assertion; the code is on trial.
- **Don't adjust tests to match buggy code** — a code-vs-requirement mismatch is a defect finding, not a test to fix. Weakening assertions to reach green is the suite lying.
- **Don't test internals or private methods** — the architecture's module interface is the boundary. Tests that verify call sequences or internal state break on every refactor while proving nothing.
- **Don't chase coverage percentage with meaningless tests** — assertion-free, trivial, or third-party-behavior tests inflate numbers and prove nothing. Requirement coverage is the primary metric; line/branch coverage is a verification aid.
- **Don't skip error and edge paths** — the happy path covers the lines but not the requirement. Every failure contract, boundary, and invalid transition the requirement states has a test.
- **Don't mock everything** — real > fake > stub > mock. Tests that verify mock behavior provide low confidence; doubles only at architecture-defined boundaries.
- **Don't generate flaky tests** — sleeps, real wall-clock, network, order dependence, and shared state produce suites nobody trusts.
- **Don't test third-party framework behavior** — only the project's own code is on trial.
- **Don't generate tests for 🔴 modules without asking first** — requirement-less tests are either behavior-derived (explicit decision, clearly marked) or deferred. Silent requirement-invention is forbidden.
- **Don't leave requirement coverage gaps unreported** — every in-scope requirement maps to a test or a documented reason why not.
- **Don't duplicate higher-level coverage at unit level** — respect the test pyramid and the test concept's level split; map delegated items instead of mocking the world.
- **Don't write vague test names** — "works", "handles errors", "test 3" name nothing. Names state the required behavior and reference the source ID.
- **Don't run the same suite twice without an intervening change** — after a clean run, re-running adds nothing unless code changed.
- **Don't deliver without the traceability matrix** — the requirement↔test mapping is the primary deliverable; the test files are its executable form.

## Related Skills

- **`test-driven-development`**: TDD drives implementation (write the failing test first, then code). Unit-test-generation audits and regression-covers **existing** modules from requirements (requirements-first). Defect findings discovered here flow into TDD Prove-It fixes: the failing requirement-driven test becomes the reproduction test.
- **`generate-test-concept`**: the test concept defines levels, techniques, gates, and traceability this skill consumes; generated results update its §9.1 requirements-to-tests matrix and evidence section.
- **`debugging-and-error-recovery`**: failing generated tests and defect findings flow into debugging workflows.
- **`browser-testing-with-devtools`**: UI behaviors that cannot be unit-tested (rendering, interaction, accessibility tree) belong to integration/E2E levels and flow to browser testing.

## Document Hierarchy Context

Unit tests sit in the testing level of the project lifecycle. They consume:

| Document | Relationship | Consumed for unit tests? |
|----------|-------------|--------------------------|
| **SRS** | Authoritative source of required behavior — FR/UC/BR/IR/DR define the behaviors; NFRs define the testable quality constraints | Yes — every test's expected behavior derives from it |
| **User Stories** | Delivery-level behavior with acceptance criteria (`US-xxx.AC-x`, typed Functional/Error/Edge/NFR) | Yes — acceptance criteria translate directly into tests |
| **Software Architecture** | Defines building blocks, module interfaces (the unit boundary), and cross-cutting behaviors | Yes — module decomposition and doubles policy derive from it |
| **Test Concept** | Defines levels, design techniques, quality gates, and traceability format | When present — targets and mappings align to it |
| **Risk Profile / Business Case** | Rank criticality for prioritization and defect severity | When present |

And they feed:

| Artifact | Relationship | Fed by unit tests? |
|----------|-------------|-------------------|
| **Defect findings / bug backlog** | Code-vs-requirement mismatches become defects for TDD remediation | Yes — the primary output beyond the suite |
| **Traceability matrix (test concept §9.1)** | Requirement↔test evidence for quality gates | Yes — updated with generated mappings |
| **Integration / functional / E2E tests** | Delegated NFRs and glue-level behaviors map to higher levels | Yes — mappings recorded, not tested here |
| **CI quality gates (§5.1)** | Suite + coverage run in merge gates | Yes — suite must pass in CI conditions |

When generating unit tests, keep in mind that the primary output is **a requirement-driven, traceable, deterministic test suite plus the defect findings it exposed** — not just a green build. A suite that only turns green has verified nothing; the value is in what the requirements revealed about the code.
