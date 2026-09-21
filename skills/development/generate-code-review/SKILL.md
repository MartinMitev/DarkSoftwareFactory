---
name: generate-code-review
description: Generates an evidence-based Code Review document for a single change using the repository template `templates/development/code-review.md`. This skill should be used when a change (feature, refactoring, bug fix — human-, agent-, or AI-written) must be formally reviewed and recorded before merge. The skill deeply analyzes the change under review plus all available project information (spec/task/bug items, SRS, architecture, test concept, coding conventions, CI evidence) across the five review axes, and asks targeted open questions with suggested valid answers whenever gaps, unclear statements, or contradictions are detected.
---

# Skill: Generate Code Review

## Description

Generates a complete, rigorous Code Review document for one self-contained change based on the template `templates/development/code-review.md`. The skill deeply analyzes the change under review (diff, commit messages, PR description) together with all available project information — spec/task/bug items the change implements, related project documents (SRS, architecture/ADRs, test concept, environment setup, coding conventions), verification evidence (tests, builds, benchmarks, screenshots), and the codebase itself — to produce a structured review record: change context, five-axis checklist results, labeled findings, verification story, verdict with merge gate, and follow-up items. When gaps, unclear statements, or contradictions are detected, the skill asks targeted open questions with suggested valid answers before proceeding.

This skill generates the **formal per-change record**. It applies the review standards of the `code-review-and-quality` skill (five axes, severity labels, sizing, verification, merge gate) as the analytical basis, and captures the outcome in the document. Conducting an informal review without the record, or generating the record without the analysis, both miss the point.

## Activation

When the user requests to create, generate, or draft a code review document, review record, review findings report, merge-gate review for a PR/change, or asks to "review and document" a change. Also applies when the user asks to review changes produced by agents or other models and a formal record is required.

## Instructions

### Phase 1: Information Gathering & Deep Analysis

1. **Read the template** at `templates/development/code-review.md` (canonical copy: `assets/code-review.md` in this skill) to understand the full structure, all 9 sections, their subsections, and expected content. Pay special attention to:
   - The identification scheme — CR-XXX for the review, FIND-XXX for findings, FU-XXX for follow-up items.
   - The review order (Section 4.0) — context first, tests first, then the implementation per axis, then findings, then verification.
   - The severity labels (Appendix B) — *(no prefix)* required, Critical, Nit, Optional/Consider, FYI. Every comment must carry a label.
   - The verdict options (Section 7.1) — ✅ Approve / ❌ Request Changes / 🔴 Block — and the approval standard: approve when the change definitely improves overall code health.
   - The merge gate (Section 7.4) and follow-up rules (Section 8): a deferral is never "I'll clean it up later" — it requires justification, self-assignment, and a tracked reference.
   - The disagreement resolution hierarchy (Appendix C) — technical facts > style guides > design principles > codebase consistency.

2. **Discover and read the change under review** (primary evidence source):
   - Identify the change: branch, PR/change ID, or working-tree diff. If no PR exists, use `git diff`/commit range against the base branch.
   - Compute change size: lines changed, files changed (Section 3.3 sizing targets: ~100 good, ~300 acceptable if single logical change, ~1000 → split).
   - Read commit messages and PR description — assess the first line (short, imperative, standalone) and body (what and why, context not visible in code, links, acknowledged shortcomings) against Section 3.2.
   - Read the full diff file by file — this is the object of the five-axis walkthrough.

3. **Discover spec/task/bug items the change implements:**
   - Search for task/bug references in commit messages, branch name, and PR description (issue numbers, task IDs, bug IDs).
   - Search the workspace for specs, design docs, task descriptions, and bug reports related to the change. Read the relevant requirements or acceptance criteria in full.
   - Record each item with what part of the change implements it (Section 3.4 table).

4. **Discover related project documents:**
   - SRS/Requirements (`*requirements*.md`, `*srs*.md`) — the correctness axis measures against these.
   - Architecture and ADRs (`*architecture*.md`, `adr*/*.md`) — the architecture axis measures against these; unresolved or contradicted decisions become findings.
   - Test concept (`*test-concept*.md`) — required test levels and quality gates the change must satisfy.
   - Environment setup and coding conventions (`*environment-setup*.md`, `*coding-conventions*.md`, CONTRIBUTING, style guides) — the readability axis measures against these.
   - Project metadata sources (business case, SRS header, README) — project name, system name, project type, roles, classification for the Metadata table.

5. **Discover verification evidence:**
   - CI runs, test results, build logs (Section 6). Run the test suite and build if no results exist and running is feasible.
   - For bug fixes: a regression test must exist — verify it would fail without the fix.
   - For UI changes: screenshots or before/after evidence.
   - For performance-relevant changes: benchmarks or before/after comparison.
   - Lint/static analysis/audit output (dependency review, Section 4.6).

6. **Explore the codebase for review context:**
   - Existing patterns in the touched modules (architecture axis: does the change follow or justify a new pattern?).
   - Coding conventions in the touched files.
   - Orphaned code after refactoring (dead code hygiene, Section 4.7) — list elements that are now unreachable or unused.

7. **Map existing information to template sections.** For each section (Metadata, 3.1–3.6, 4.0–4.7, 5–8, Appendices), determine:
   - **Covered**: Sufficient evidence exists to populate with concrete, evidence-based content.
   - **Partially Covered**: Some information exists but is incomplete or too vague to evaluate (e.g., task link without acceptance criteria, verification claim without evidence).
   - **Gap**: No information exists (e.g., no spec link, no reviewers, no CI evidence, no classification).
   - **Contradiction**: Sources conflict (e.g., description claims a bug fix but the diff adds a feature; claimed tests do not exist in the diff; change is large but the description claims a single logical change; security-sensitive change has no security reviewer).

8. **Perform deep review analysis** following the review order (Section 4.0):
   - **Context**: State what the change tries to accomplish, which spec/task it implements, and the expected behavior change. If this cannot be stated confidently from available information, that is a 🔴 gap and a [Critical] question.
   - **Tests first**: Read the tests before the implementation. Do they test behavior (not implementation details)? Do they cover edge cases? Do they have descriptive names? Would they catch a regression? Missing or weak tests are findings (required, or Critical for bug fixes without regression tests).
   - **Implementation per axis**: Walk through each changed file against the five axes (Section 4.1–4.5) and fill each checklist table with concrete Yes/No/NA verdicts and notes. Quantify problems where possible ("this N+1 query adds ~50ms per item", not "this could be slow").
   - **Dependency review (4.6)**: For every new dependency, evaluate existing-stack alternatives, size/bundle impact, maintenance, known vulnerabilities, license compatibility.
   - **Dead code hygiene (4.7)**: List now-unused elements, mark Safe to Remove, and record the ask-first decision. Never silently delete what you are unsure about.
   - **Findings (5)**: Label every finding with a severity and axis, assign FIND-XXX IDs, record location (file:line), description with evidence, quantified impact where possible, and required action. Do not soften real issues and do not rubber-stamp.
   - **Verification (6)**: Record what was verified by author vs reviewer, with evidence links. Reviewer-verified checks must be named concretely (what was re-run or checked).
   - **Outcome (7)**: Derive the verdict from the findings and verification — not from politeness. Per-axis summary with blocking findings; disagreements resolved via the Appendix C hierarchy; merge-gate checklist from the actual state.

9. **Build a readiness map** — for each section, tag readiness:
   - 🟢 **Review-Ready**: Evidence is concrete and sufficient to fill the section with defensible content.
   - 🟡 **Partially Ready**: Section can be drafted but with weak or inferred content that should be confirmed.
   - 🔴 **Not Ready**: Missing evidence, unclear statements, or contradictions — the section cannot be filled honestly without clarification.

   Sections with 🔴 readiness are priority candidates for Phase 2 questions.

### Phase 2: Clarification Questions

Before generating the document, ask the user targeted questions for every **Partially Covered**, **Gap**, **Contradiction**, or **Not Ready** area identified in Phase 1.

#### Question Design Principles

- **Ask open questions** that invite thoughtful responses — not yes/no questions.
- **Always suggest 2–3 possible valid answers** for each question, each with its implications for the review record, to help the user think through the options and to demonstrate domain understanding.
- **Contextualize each question** — briefly explain why the information matters for the review record and what happens if it remains unanswered (e.g., "Without verification evidence, the merge gate cannot be checked and the verdict must be 🔴 Block regardless of code quality").
- **Group questions by template section** so the user can address them systematically.
- **Prioritize questions**:
  - **[Critical]**: Blocks the review record — the verdict, merge gate, or a checklist table cannot be filled honestly without it (e.g., missing verification evidence, unknown spec/task being implemented, unresolved contradiction between description and diff).
  - **[Important]**: Affects record quality or reviewability (e.g., missing reviewer names, vague task relevance, unquantified impact).
  - **[Optional]**: Refines the record; can proceed as a documented assumption with a validation plan (e.g., estimated line counts, assumed classification).
- **Reference the source** of the contradiction or gap precisely (e.g., "The commit message says 'fix race condition' but the diff contains no changes to concurrency handling — only a renamed variable").
- **Do not ask questions that existing evidence already answers** — if the answer is in the diff, CI logs, or documents the skill has read, use it directly.
- **Distinguish what must be resolved now vs. what can be documented as an assumption with a validation plan** — for [Optional] items, offer to proceed with the stated assumption recorded in the document.
- **Respect review speed** (Section 3.6 guidance): batch by priority, lead with critical questions, and offer to proceed with assumptions for lower-priority items so the review completes within its cadence target.

#### Question Template

For each question, use this format:

---

**[Priority] Section X.Y — [Topic]**

[Context: Why this matters for the review record and what happens if unanswered]

[The open question]

Suggested answers:
- *Option A*: [description and implications for the review record]
- *Option B*: [description and implications for the review record]
- *Option C*: [description and implications for the review record]
- *Custom*: [your own answer]

---

#### Minimum Required Questions (All Changes)

Resolve these before the review record can be completed:

- What spec, task, or bug does this change implement, and which part of the change implements it? (Without this, correctness cannot be evaluated — Section 4.1 has no reference point.)
- What is the expected behavior change, and how does the change's description map to what the diff actually does?
- Who are the author(s), reviewer(s), and the human making the final call? For agent/AI-written code: was a different model used for review per the multi-model pattern?
- Is this change security-sensitive (auth, input handling, secrets, external data, dependencies)? If yes, who performs the security-focused review?
- What verification evidence exists (tests run, build, manual checks, screenshots, benchmarks), and can it be linked or re-run now?
- What classification (Public | Internal | Confidential) applies to this document, and who are the metadata role holders (Sponsor, PO, PM, Tech Lead, Security Lead) — or which project document lists them?
- If the change exceeds ~300 lines: what is the split decision — review as-is, or split (stack / by file group / horizontal / vertical)?

#### Type-Specific Questions (Only When Applicable)

- **Bug fix (🩹)**: What is the reproduction scenario, and does a regression test exist that fails without the fix?
- **UI change (🖼️)**: Where are the before/after screenshots or how should the reviewer verify visually?
- **Security-sensitive (🔐)**: Which threat model applies (input boundaries, data trust, secrets)? Who is the security reviewer?
- **New dependency (📦)**: What existing-stack alternative was considered, and what is the audit result, maintenance status, and license?
- **Performance-relevant (⚡)**: What benchmark or measurement demonstrates the before/after impact?
- **Refactoring (🧹)**: Which elements are now dead code, and are they safe to remove — removed now, filed as FU-XXX, or kept intentionally?
- **Agent/AI-written code (🤖)**: Which model wrote the change, which reviewed it, and what were the model-specific blind spots to check?

#### Contradiction Questions (Highest Priority)

When sources conflict, surface the contradiction explicitly and ask how to resolve it:

- **Description vs. diff**: description claims X, diff implements Y — which is authoritative, or is the description to be corrected?
- **Size vs. single-change claim**: change is ~1000+ lines but described as one logical change — split, or justify as a large-but-single change (e.g., complete file deletion, automated refactor)?
- **Claimed tests vs. actual tests**: verification claims passing tests, but the diff adds no tests and CI evidence is missing — where is the evidence?
- **Change vs. conventions/ADR**: implementation deviates from coding conventions or an architectural decision — is the deviation justified (record as justified) or a finding (required/Critical)?
- **Spec vs. implementation**: requirement says X, code does a variation — intentional interpretation or drift?

### Phase 3: Document Generation

Once all critical and important questions are resolved, generate the Code Review document.

#### Generation Rules

1. **Use the template structure exactly** — follow `templates/development/code-review.md` section by section, including all subsections and appendices.
2. **Replace all `<!-- -->` placeholders** with project-specific content derived from the analysis and user answers.
3. **Fill every table with concrete, specific content** — no placeholder values remain in the final document.
4. **Assign identifiers consistently**: CR-XXX for the review, FIND-XXX for findings, FU-XXX for follow-up items.
5. **Record review identification (3.1)** with the change's actual repository, branch, and PR/change ID; record review date(s) per round.
6. **Assess change size (3.3) from the actual diff**, not from claims; record the split decision with rationale if the change exceeds sizing targets.
7. **Populate the five-axis tables (4.1–4.5) from the actual walkthrough** — every row gets Yes/No/NA plus a concrete note; write "NA" with a reason, never leave a row unevaluated.
8. **Label every finding with severity and axis (5.1)** and give each a required action where applicable; expand important findings in 5.2 with evidence and quantified impact; record unlabeled-comment cleanup in 5.3.
9. **Write the verification story (6) from actual evidence** — author-verified vs. reviewer-verified checks separated, with CI links, test names, steps performed, or explicit NA with reason. Bug fixes without a regression test and UI changes without evidence fail the merge gate.
10. **Derive the verdict (7.1) from findings and verification, not from preference** — apply the approval standard (approve when the change definitely improves overall code health) and record the human decision maker. Never approve with unresolved Critical findings; never block merely because the code differs from how the reviewer would have written it.
11. **Record deferrals and overrides honestly (7.3)** with the resolution basis from the Appendix C hierarchy; a cleanup deferral is only valid with a filed FU-XXX.
12. **Check the merge gate (7.4) against reality** — tick ☑ only what is actually satisfied; leave ☐ with the missing item named otherwise.
13. **File every follow-up (8) with self-assignment and a tracked reference** — no deferral without an owner and a reference.
14. **Keep the appendices (9) as the reusable references** — fill Appendix A with the per-change checklist state, and use Appendix B/C as references rather than duplicating them.
15. **Write the Executive Summary (1) last** — outcome, blocking findings and their resolution status, verification summary, and deferrals with their Section 8 references.
16. **Complete Document History** with version, date, author, and changes.
17. **Mark uncertainty explicitly** — where an assumption was made, record it in the relevant section (e.g., "assumed NA: no UI touched — confirmed by diff review") rather than silently filling a value.

#### Quality Checks Before Delivery

After generating the document, perform these self-checks:

- [ ] No `<!-- -->` placeholders remain (except fields explicitly reserved for humans: sign-off names and dates where the human action has not yet occurred).
- [ ] Review identification (3.1) matches the actual change (repo, branch, PR/change ID).
- [ ] Change size is computed from the diff, and the sizing assessment is consistent with the split decision.
- [ ] Every row of every five-axis table has a verdict and note; no row is blank.
- [ ] Every finding has a severity label, axis, location, and required action (empty only for Nit/FYI).
- [ ] Every Critical/required finding is resolved, deferred with FU-XXX, or reflected in the verdict (❌/🔴).
- [ ] The verification story separates author-verified from reviewer-verified checks and cites concrete evidence.
- [ ] The verdict is consistent with the findings inventory, per-axis summary, and merge-gate state (no contradiction between sections).
- [ ] Every FU-XXX has an owner (self-assignment) and a tracked reference.
- [ ] Assumptions are marked as assumptions with their validation path.
- [ ] The Executive Summary is consistent with the body (outcome, blocking findings, verification, deferrals).

### Phase 4: Post-Generation Review

After the document is generated:

1. **Present the document location and verdict summary** — verdict, per-axis results, findings count by severity, merge-gate state.
2. **Highlight key judgments made during the review** — where interpretive calls were made (e.g., severity assignment, NA justifications, dead-code decisions, interpretation of vague requirements), point them out so the user can verify.
3. **Flag remaining uncertainties** — areas where information was insufficient and assumptions were made, with the risk each assumption poses and a suggested validation action.
4. **State the merge implications clearly** — if ❌ Request Changes or 🔴 Block, list exactly what the author must do before re-review; if ✅ Approve, confirm merge-gate completion.
5. **Offer to refine** any finding, severity, or verdict the user disputes — apply the Appendix C hierarchy to resolve disputes.
6. **Suggest next steps** — address findings, file FU-XXX items in the tracker, re-run CI, update the PR description if the record exposed description gaps, merge and baseline the document, or feed recurring finding patterns back into `code-review-and-quality` conventions.

## Examples

### Example Question (Gap — No Verification Evidence)

---

**[Critical] Section 6 — Verification Story**

The change modifies the order-calculation module and the description claims "all tests pass," but no CI run is linked, and the diff adds no tests for the new proration logic. Without verification evidence, the merge gate (7.4) cannot be checked, and the verdict must be 🔴 Block regardless of code quality.

What verification evidence exists for this change, and how can it be produced or linked now?

Suggested answers:
- *Option A*: "The change was verified locally — I can run the full test suite now and attach the output as evidence. The skill should also add a required finding (FIND-XXX) for the missing proration tests, since the new logic is currently untested."
- *Option B*: "CI is configured on the PR but has not completed — the skill should record the pending run as the verification source, mark the merge gate ☐ 'pending CI', and set the verdict provisionally to ❌ Request Changes until the run is green."
- *Option C*: "No verification has happened yet. The skill should set the verdict to 🔴 Block, list 'no test evidence' as a blocking item, and file FU-XXX for authoring the proration tests with self-assignment to the author."
- *Custom*: [your own answer]

---

### Example Question (Contradiction — Description vs. Diff)

---

**[Critical] Section 3.2 & 4.1 — Change Description vs. Actual Change**

The commit message says "Fix race condition in job scheduler," but the diff contains no changes to locking, synchronization, or scheduling logic — it renames a variable and extracts a helper function in an unrelated module. Correctness (4.1) cannot be evaluated because there is no stated intent that matches the code. Reviewing a change whose description misrepresents its content defeats the purpose of the record: someone searching history for the race-condition fix would find this commit and be misled.

What does this change actually implement, and how should the description be corrected?

Suggested answers:
- *Option A*: "The description is wrong — this is the refactor part of a two-part fix; the concurrency fix will follow in a separate change. The skill should rewrite the description to 'Extract scheduler helper for upcoming concurrency fix', link the follow-up task, and record a Nit finding that the original commit message is misleading."
- *Option B*: "The description is right but the diff is incomplete — the concurrency-relevant changes were accidentally left out. The skill should set ❌ Request Changes with a Critical finding: the change does not implement what it claims; the missing scheduler changes must be added or the change resubmitted."
- *Option C*: "The variable rename is the actual race-condition mitigation (the old name encouraged unsafe reuse). The skill should record this interpretation in the description body so it stands alone in history, and mark the correctness axis 'Pass with findings' — with a required finding to document the invariant the rename enforces."
- *Custom*: [your own answer]

---

### Example Question (Unclear Statement — Vague Task Link)

---

**[Important] Section 3.4 — Spec/Task Relevance**

The PR references task TCK-142, but the task description says only "improve checkout" with no acceptance criteria. Correctness (4.1) measures the change against requirements — "improve checkout" cannot distinguish what was required from what was volunteered, so the review cannot tell whether the change is over- or under-implemented.

What exactly does TCK-142 require, and what part of the change implements it?

Suggested answers:
- *Option A*: "TCK-142 is the umbrella task; the acceptance criteria live in its subtasks TCK-143 (abandoned-cart reminder) and TCK-144 (checkout progress bar). This change implements TCK-144 only — the skill should record both subtasks with relevance notes, and evaluate correctness against TCK-144's criteria."
- *Option B*: "TCK-142 has no acceptance criteria — it was written as an epic placeholder. The skill should treat the diff itself as the de facto requirement, record 'requirements pending' in 3.4, and file FU-XXX to have the Product Owner write acceptance criteria so future changes in this area are reviewable."
- *Option C*: "TCK-142 is deliberately open-ended (exploration task). The skill should record the change as an enabler with the intent stated in the description body, mark correctness 'Pass' against the stated intent only, and add an FYI finding that formal acceptance criteria are missing for the follow-up work."
- *Custom*: [your own answer]

---

### Example Question (Gap — Security-Sensitive Change Without Security Review)

---

**[Critical] Section 3.5 & 4.4 — Security Review Coverage**

The change introduces a new file-upload endpoint that accepts user-supplied files and stores them on disk. The security axis (4.4) requires validation of user input at system boundaries, and the template requires a security-focused reviewer for security-sensitive changes (3.5) — no security reviewer is currently recorded. Uploading unvalidated user files is the classic path to path traversal and arbitrary-file-write vulnerabilities.

Is this change security-sensitive, and who performs the security-focused review?

Suggested answers:
- *Option A*: "Yes — the change is security-sensitive. The skill should assign the security reviewer from the project's Security Lead (recorded in the SRS metadata), record their review of file-type validation, size limits, storage path sanitization, and access control in 3.5, and hold the merge gate until their pass is recorded."
- *Option B*: "Yes, and no security reviewer is available this sprint. The skill should set 🔴 Block with 'security review pending' as the blocking item, add a required finding to validate the upload path (extension allowlist, size cap, randomized filenames, no user-controlled path segments), and file FU-XXX for the security review with the Tech Lead as interim owner."
- *Option C*: "No — uploads are proxied to an internal service that already validates files; this change only forwards the request. The skill should record that rationale in the 4.4 notes, mark the security axis 'Pass' with the delegation noted, and downgrade the missing security reviewer to an FYI finding referencing the proxy service's validation contract."
- *Custom*: [your own answer]

---

## Anti-Patterns to Avoid

- **Don't generate the document without the analysis** — the record's value is the evidence-based walkthrough, not template completion.
- **Don't ask questions the evidence already answers** — read the diff, CI logs, and documents first.
- **Don't ask too many questions at once** — batch by priority, lead with [Critical], offer assumption-based continuation for [Optional] items.
- **Don't rubber-stamp** — "LGTM" without evidence of review is a record of nothing. Every verdict must trace to the findings and verification sections.
- **Don't soften real issues** — "might be a minor concern" for a production-bound bug is dishonest; label it honestly and quantify.
- **Don't invent verification evidence** — record only what was actually run, linked, or observed; mark the rest as missing.
- **Don't leave five-axis rows blank or unevaluated** — every row gets a verdict and note; write "NA" with a reason.
- **Don't skip the tests-first pass** — reviewing implementation before tests biases the review toward the code's framing instead of the intended behavior.
- **Don't accept unlabeled feedback** — retroactively label any comment that lacks a severity (Section 5.3).
- **Don't defer cleanup without a follow-up item** — "I'll clean it up later" is not a disposition; FU-XXX with owner and reference is.
- **Don't silently delete dead code you are unsure about** — ask first (Section 4.7).
- **Don't duplicate the process skill** — reference `code-review-and-quality` for review standards; the document records outcomes, not the methodology.
- **Don't copy content from source documents verbatim** — reference the SRS, task, or ADR; the record captures the review's conclusions about them.
- **Don't block on style preference** — the approval standard is overall code health, not the reviewer's personal style; Nits are optional.

## Document Hierarchy Context

The Code Review document is a **per-change record**, not a project-phase document. It sits in this context:

| Document | Relationship |
|----------|--------------|
| **SRS / Requirements** | Defines what the change must do — the correctness axis measures against it |
| **Software Architecture / ADRs** | Defines the system's design — the architecture axis measures against it |
| **Test Concept** | Defines required test levels and quality gates — the verification story must satisfy them |
| **Environment Setup / Coding Conventions** | Define the standards — the readability axis measures against them |
| **Spec / Task / Bug items** | Define what this specific change implements — recorded in 3.4 and traced in 4.1 |
| **Merge / Baseline** | The review record is a merge gate: ✅ Approve permits merge; the baselined record becomes part of the change's history |

Related Documents (Metadata table) should link the concrete documents used during the review so the record is auditable.
