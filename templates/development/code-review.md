# Code Review Document

> **Template Version:** 1.0  \
> **Last Updated:** <!-- date -->  \
> **Document Status:** <!-- Draft | Under Review | Approved | Baselined -->

---

## Metadata

| Field | Value |
|------|-------|
| **Project Name** | <!-- project name --> |
| **System / Application** | <!-- system name --> |
| **Project Type** | <!-- Green Field | Brown Field | Software Modernization --> |
| **Sponsor** | <!-- sponsor --> |
| **Product Owner** | <!-- PO --> |
| **Project Manager** | <!-- PM --> |
| **Technical Lead** | <!-- tech lead --> |
| **Security Lead** | <!-- security lead --> |
| **Author(s)** | <!-- author(s) --> |
| **Reviewer(s)** | <!-- reviewer(s) --> |
| **Date Created** | <!-- date --> |
| **Date Revised** | <!-- date --> |
| **Classification** | <!-- Public | Internal | Confidential --> |
| **Baseline Version** | <!-- once approved --> |
| **Related Documents** | <!-- SRS / architecture / test concept / environment setup / coding conventions --> |

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Purpose, Scope, and Definitions](#2-purpose-scope-and-definitions)
3. [Change Context](#3-change-context)
4. [Review Criteria (Five-Axis Checklist)](#4-review-criteria-five-axis-checklist)
5. [Review Findings](#5-review-findings)
6. [Verification Story](#6-verification-story)
7. [Review Outcome and Decisions](#7-review-outcome-and-decisions)
8. [Follow-up Management](#8-follow-up-management)
9. [Appendices](#9-appendices)

---

## 1. Executive Summary

<!--
Write this section last.

Expected content:
- The change under review (one line: what it does and where it lands).
- The review outcome: Approve, Request Changes, or Block.
- Blocking findings, if any, and their resolution status.
- Verification summary: tests, build, manual checks.
- Deferrals: what was explicitly deferred and where it is tracked (Section 8).
-->

<!-- Placeholder: 2-4 bullets. -->

---

## 2. Purpose, Scope, and Definitions

<!--
Expected content:
- Why this document exists: it is the per-change record of the code review, used before merging any change (no exceptions).
- Scope: what the review covers (all changes: features, refactoring, bug fixes including regression tests; human-, agent-, and AI-written code).
- Out of scope: what is not part of this record (e.g., merge policy administration, architecture decision records — link instead).
- Definitions table (below).
-->

### Definitions

| Term | Definition |
|------|------------|
| **Change** | A single self-contained modification: addresses one thing, includes related tests, and keeps the system functional after submission |
| **Review Axis** | One of five review dimensions: correctness, readability & simplicity, architecture, security, performance |
| **Finding** | A review comment labeled with its severity so the author knows what is required vs optional |
| **Severity Label** | The prefix on every finding: (no prefix) required, Critical, Nit, Optional/Consider, FYI |
| **Verification Story** | Evidence of how the change was verified: tests run, build result, manual checks, UI evidence |
| **Review Round** | One reviewer pass over the change; multiple rounds are normal for a typical change |
| **Deferral** | An issue explicitly not fixed in this change; requires justification and a follow-up item with self-assignment |

---

## 3. Change Context

<!--
Expected content:
- Review identification: review ID, PR/change ID, repository, branch, review date(s).
- Change description: first line short, imperative, standalone ("Delete the FizzBuzz RPC", not "Deleting the FizzBuzz RPC") + body with what and why. Link to bug numbers, benchmark results, or design docs. Acknowledge approach shortcomings when they exist.
- Change size: ~lines changed and whether it fits the sizing targets; if too large, record the split decision (stack, by file group, horizontal, vertical strategies).
- Spec, task, and bug links with what part of the change implements them.
- Author(s) and reviewer(s). Note AI/model-assisted review where used (multi-model pattern: one writes, another reviews, the human makes the final call).
- Review round log with dates, reviewers, findings added, and verdict per round.
-->

### 3.1 Review Identification

| Field | Value |
|------|-------|
| **Review ID** | <!-- CR-XXX --> |
| **PR / Change ID** | <!-- PR number or change ID --> |
| **Repository** | <!-- repository name or URL --> |
| **Branch** | <!-- branch name --> |
| **Review Date(s)** | <!-- date(s) --> |

### 3.2 Change Description

<!--
First line: short, imperative, standalone. Must be informative enough that someone searching history can understand the change without reading the diff.
Body: what is changing and why; context, decisions, and reasoning not visible in the code itself. Acknowledge shortcomings when they exist.
-->

<!-- First line -->

<!-- Body -->

### 3.3 Change Size

| Field | Value |
|------|-------|
| **Lines Changed (approx.)** | <!-- ~lines --> |
| **Files Changed** | <!-- count --> |
| **Sizing Target Assessment** | <!-- ~100 lines: good (reviewable in one sitting) / ~300 lines: acceptable if single logical change / ~1000 lines: too large → split --> |
| **Split Decision** | <!-- None | Stack | By file group | Horizontal | Vertical — with rationale if split --> |

### 3.4 Spec, Task, and Bug Links

| ID | Type (Spec / Task / Bug / Design Doc) | Link | Relevance |
|------|------|------|------|
| <!-- ID --> | <!-- type --> | <!-- link --> | <!-- what part of the change implements it --> |

### 3.5 Author(s) and Reviewer(s)

| Role | Name | Notes |
|------|------|-------|
| **Author** | <!-- name --> | <!-- human or model used --> |
| **Reviewer (correctness, architecture)** | <!-- name --> | <!-- e.g., different model than the author, per multi-model pattern --> |
| **Reviewer (security)** | <!-- name --> | <!-- required for security-sensitive changes --> |
| **Final Call (human)** | <!-- name --> | <!-- the human makes the final decision --> |

### 3.6 Review Round Log

| Round | Date | Reviewer | Findings Added | Verdict |
|------|------|------|------|------|
| 1 | <!-- date --> | <!-- name --> | <!-- FIND-XXX, ... --> | <!-- Approve | Request Changes --> |
| 2 | <!-- date --> | <!-- name --> | <!-- ... --> | <!-- ... --> |

<!--
Review speed guidance:
- Respond within one business day — this is the maximum, not the target.
- Fast individual responses beat quick final approval; a typical change completes multiple review rounds in a single day.
- Ask the author to split large changes rather than reviewing one massive changeset.
-->

---

## 4. Review Criteria (Five-Axis Checklist)

<!--
Expected content:
- The five-axis checklist, evaluated in review order: context first, tests first, then the implementation per axis.
- Per axis: a checklist table (criterion, met?, notes) plus the axis-specific review questions.
- Additional subsections: dependency review and dead code hygiene.
- Review order: understand the intent → review the tests first → walk through the implementation → categorize findings (Section 5) → verify the verification (Section 6).
-->

### 4.0 Review Order

<!--
Understand the context before looking at code: what is this change trying to accomplish, what spec or task does it implement, what is the expected behavior change.
Review the tests first: they reveal intent and coverage (do they test behavior, not implementation details; would they catch a regression; descriptive names).
Then walk through the implementation per axis.
-->

| Step | Checklist | Done |
|------|------|------|
| **Context** | <!-- I understand what this change does and why --> | <!-- ☐ --> |
| **Tests first** | <!-- Tests exist, test behavior, cover edge cases, descriptive names, catch regressions --> | <!-- ☐ --> |
| **Implementation** | <!-- Walk through each file with the five axes --> | <!-- ☐ --> |
| **Findings** | <!-- All comments carry severity labels (Section 5) --> | <!-- ☐ --> |
| **Verification** | <!-- Verify the verification story (Section 6) --> | <!-- ☐ --> |

### 4.1 Correctness

<!--
Does the code do what it claims to do? Review questions:
- Does it match the spec or task requirements?
- Are edge cases handled (null, empty, boundary values)?
- Are error paths handled (not just the happy path)?
- Does it pass all tests? Are the tests actually testing the right things?
- Are there off-by-one errors, race conditions, or state inconsistencies?
-->

| Criterion | Met? | Notes |
|------|------|------|
| <!-- Change matches spec/task requirements --> | <!-- Yes | No | NA --> | <!-- notes --> |
| <!-- Edge cases handled (null, empty, boundary values) --> | <!-- ... --> | <!-- ... --> |
| <!-- Error paths handled (not just the happy path) --> | <!-- ... --> | <!-- ... --> |
| <!-- Tests cover the change adequately and test behavior (not implementation details) --> | <!-- ... --> | <!-- ... --> |
| <!-- No off-by-one errors, race conditions, or state inconsistencies --> | <!-- ... --> | <!-- ... --> |

### 4.2 Readability and Simplicity

<!--
Can another engineer (or agent) understand this code without the author explaining it? Review questions:
- Are names descriptive and consistent with project conventions (no temp/data/result without context)?
- Is the control flow straightforward (avoid nested ternaries, deep callbacks)?
- Is related code grouped, with clear module boundaries?
- Are there clever tricks that should be simplified?
- Could this be done in fewer lines (1000 lines where 100 suffice is a failure)?
- Are abstractions earning their complexity (do not generalize until the third use case)?
- Would comments help clarify non-obvious intent (but not comment obvious code)?
- Dead code artifacts: no-op variables, backwards-compat shims, or "removed" comments?
-->

| Criterion | Met? | Notes |
|------|------|------|
| <!-- Names are descriptive and consistent with project conventions --> | <!-- ... --> | <!-- ... --> |
| <!-- Control flow is straightforward --> | <!-- ... --> | <!-- ... --> |
| <!-- Related code is grouped; module boundaries are clear --> | <!-- ... --> | <!-- ... --> |
| <!-- No unnecessary cleverness or complexity --> | <!-- ... --> | <!-- ... --> |
| <!-- Could this be done in fewer lines (complexity earns itself) --> | <!-- ... --> | <!-- ... --> |
| <!-- Abstractions earn their complexity (no premature generalization) --> | <!-- ... --> | <!-- ... --> |
| <!-- Comments clarify non-obvious intent only --> | <!-- ... --> | <!-- ... --> |
| <!-- No dead code artifacts (no-op variables, compat shims, "removed" comments) --> | <!-- ... --> | <!-- ... --> |

### 4.3 Architecture

<!--
Does the change fit the system's design? Review questions:
- Does it follow existing patterns or introduce a new one (if new, is it justified)?
- Does it maintain clean module boundaries?
- Is there code duplication that should be shared?
- Are dependencies flowing in the right direction (no circular dependencies)?
- Is the abstraction level appropriate (not over-engineered, not too coupled)?
-->

| Criterion | Met? | Notes |
|------|------|------|
| <!-- Follows existing patterns (or new pattern is justified) --> | <!-- ... --> | <!-- ... --> |
| <!-- Maintains clean module boundaries --> | <!-- ... --> | <!-- ... --> |
| <!-- No code duplication that should be shared --> | <!-- ... --> | <!-- ... --> |
| <!-- Dependencies flow in the right direction (no circular dependencies) --> | <!-- ... --> | <!-- ... --> |
| <!-- Appropriate abstraction level (not over-engineered, not too coupled) --> | <!-- ... --> | <!-- ... --> |

### 4.4 Security

<!--
Does the change introduce vulnerabilities? Review questions:
- Is user input validated and sanitized?
- Are secrets kept out of code, logs, and version control?
- Is authentication/authorization checked where needed?
- Are SQL queries parameterized (no string concatenation)?
- Are outputs encoded to prevent XSS?
- Are dependencies from trusted sources with no known vulnerabilities?
- Is data from external sources (APIs, logs, user content, config files) treated as untrusted?
- Are external data flows validated at system boundaries before use in logic or rendering?

Security-sensitive changes require a security-focused reviewer (Section 3.5).
-->

| Criterion | Met? | Notes |
|------|------|------|
| <!-- User input validated and sanitized --> | <!-- ... --> | <!-- ... --> |
| <!-- No secrets in code, logs, or version control --> | <!-- ... --> | <!-- ... --> |
| <!-- Authentication/authorization checked where needed --> | <!-- ... --> | <!-- ... --> |
| <!-- SQL queries parameterized (no string concatenation) --> | <!-- ... --> | <!-- ... --> |
| <!-- Outputs encoded to prevent XSS --> | <!-- ... --> | <!-- ... --> |
| <!-- Dependencies from trusted sources, no known vulnerabilities --> | <!-- ... --> | <!-- ... --> |
| <!-- External data treated as untrusted and validated at system boundaries --> | <!-- ... --> | <!-- ... --> |

### 4.5 Performance

<!--
Does the change introduce performance problems? Review questions:
- Any N+1 query patterns?
- Any unbounded loops or unconstrained data fetching?
- Any synchronous operations that should be async?
- Any unnecessary re-renders in UI components?
- Any missing pagination on list endpoints?
- Any large objects created in hot paths?
-->

| Criterion | Met? | Notes |
|------|------|------|
| <!-- No N+1 query patterns --> | <!-- ... --> | <!-- ... --> |
| <!-- No unbounded loops or unconstrained data fetching --> | <!-- ... --> | <!-- ... --> |
| <!-- Synchronous operations that should be async (if any) --> | <!-- ... --> | <!-- ... --> |
| <!-- No unnecessary re-renders in UI components --> | <!-- ... --> | <!-- ... --> |
| <!-- Pagination on list endpoints --> | <!-- ... --> | <!-- ... --> |
| <!-- No large objects created in hot paths --> | <!-- ... --> | <!-- ... --> |

### 4.6 Dependency Review

<!--
Fill for every new dependency. Prefer the standard library and existing utilities over new dependencies; every dependency is a liability.
Before adding any dependency: does the existing stack solve this; how large is it (bundle impact); is it actively maintained; known vulnerabilities; compatible license.
-->

| Dependency | Existing Stack Solves It? | Size / Bundle Impact | Actively Maintained? | Known Vulnerabilities? | License Compatible? |
|------|------|------|------|------|------|
| <!-- name --> | <!-- Yes | No | NA --> | <!-- ... --> | <!-- last commit, open issues --> | <!-- npm audit result --> | <!-- Yes | No --> |

### 4.7 Dead Code Hygiene

<!--
After any refactoring or implementation change, list code that is now unreachable or unused.
Ask before deleting: "Should I remove these now-unused elements: [list]?" Do not silently delete what you are unsure about.
Record the inventory and the decision here; items not resolved in this change become findings (Section 5) or follow-up items (Section 8).
-->

| Element | Location | Replaced By | Safe to Remove? | Decision |
|------|------|------|------|------|
| <!-- element name --> | <!-- file --> | <!-- replacement --> | <!-- Yes | No → ask --> | <!-- Removed | FU-XXX | FIND-XXX --> |

---

## 5. Review Findings

<!--
Expected content:
- The findings inventory: every review comment, each labeled with its severity.
- Per finding: ID, severity, axis, location (file/line), description with evidence, required author action, disposition.
- Guidance:
  - Every comment must carry a severity label — unlabeled feedback makes required vs optional unclear.
  - Quantify problems when possible ("this N+1 query adds ~50ms per item in the list" beats "this could be slow").
  - Do not soften real issues and do not rubber-stamp (no "LGTM" without evidence of review).
  - Push back on approaches with clear problems; sycophancy is a failure mode in reviews.
- Finding IDs FIND-XXX. Required findings must be addressed before merge; Critical findings block merge.
-->

### 5.1 Findings Inventory

| Finding ID | Severity | Axis | Location | Description | Required Author Action | Status |
|------|------|------|------|------|------|------|
| <!-- FIND-001 --> | <!-- Critical | (no prefix) required | Nit | Optional/Consider | FYI --> | <!-- correctness | readability | architecture | security | performance --> | <!-- file:line --> | <!-- ... --> | <!-- ... --> | <!-- Open | Addressed | Deferred → FU-XXX --> |

### 5.2 Finding Details

<!--
Repeat this block per finding when detail is needed beyond one inventory row.
-->

**FIND-XXX: <!-- short title -->**

| Field | Value |
|------|-------|
| **Severity** | <!-- Critical | (no prefix) required | Nit | Optional/Consider | FYI --> |
| **Axis** | <!-- correctness | readability | architecture | security | performance --> |
| **Location** | <!-- file:line or review comment link --> |
| **Description** | <!-- what is wrong, with evidence --> |
| **Evidence** | <!-- diff excerpt, benchmark, audit result, spec citation --> |
| **Quantified Impact** | <!-- e.g., ~50ms per item; else NA --> |
| **Required Action** | <!-- what the author must do (empty for Nit/FYI) --> |
| **Disposition** | <!-- Addressed in round N | Deferred → FU-XXX | Ask reviewer --> |

### 5.3 Unlabeled Comments Check

<!--
None — every comment must carry a severity label. If any comment was added without a label during the round, retroactively label it here so required vs optional stays unambiguous.
-->

<!-- Placeholder: none, or list of retroactively labeled comments. -->

---

## 6. Verification Story

<!--
Expected content:
- What the author verified: tests run, build result, manual verification, UI evidence, before/after comparison.
- What the reviewer verified independently.
- UI changes require screenshots; bug fixes require a regression test.
- Do not rubber-stamp: the verification story is part of the merge gate (Section 7).
-->

| Check | Verified By | Result | Evidence |
|------|------|------|------|
| **Tests pass** | <!-- author --> | <!-- ... --> | <!-- CI run link --> |
| **Build succeeds** | <!-- author --> | <!-- ... --> | <!-- CI run link --> |
| **Regression test for bug fix** | <!-- author --> | <!-- ... | NA --> | <!-- test name/ID --> |
| **Manual verification** | <!-- author --> | <!-- ... | NA --> | <!-- steps performed --> |
| **UI evidence (screenshots)** | <!-- author --> | <!-- ... | NA --> | <!-- link --> |
| **Before/after comparison** | <!-- author --> | <!-- ... | NA --> | <!-- benchmark or link --> |
| **Reviewer-verified checks** | <!-- reviewer --> | <!-- ... --> | <!-- what was re-run or checked --> |

---

## 7. Review Outcome and Decisions

<!--
Expected content:
- Verdict: ✅ Approve (ready to merge) / ❌ Request Changes (issues must be addressed) / 🔴 Block (merge gate not passed).
- The approval standard: approve when the change definitely improves overall code health, even if it isn't perfect; do not block because it isn't exactly how you would have written it.
- Per-axis summary with blocking findings per axis.
- Deferrals and overrides: all required findings addressed or explicitly deferred with justification; deferral of cleanup is not accepted without a follow-up item (Section 8).
- Disagreements: where reviewer and author disagreed and how it was resolved (Appendix C hierarchy: technical facts > style guides > design principles > codebase consistency).
- Honesty checks: no rubber-stamp, real issues not softened, author override accepted gracefully where the author has full context; comment on code, not people.
-->

### 7.1 Verdict

| Field | Value |
|------|-------|
| **Final Verdict** | <!-- ✅ Approve | ❌ Request Changes | 🔴 Block --> |
| **Decision Maker** | <!-- name (human) --> |
| **Date** | <!-- date --> |
| **Rationale** | <!-- why this verdict; what improves overall code health --> |

### 7.2 Per-Axis Summary

| Axis | Result | Blocking Findings | Notes |
|------|------|------|------|
| **Correctness** | <!-- Pass | Fail | Pass with findings --> | <!-- FIND-XXX or none --> | <!-- ... --> |
| **Readability & Simplicity** | <!-- ... --> | <!-- ... --> | <!-- ... --> |
| **Architecture** | <!-- ... --> | <!-- ... --> | <!-- ... --> |
| **Security** | <!-- ... --> | <!-- ... --> | <!-- security-focused review required for security-sensitive changes --> |
| **Performance** | <!-- ... --> | <!-- ... --> | <!-- ... --> |

### 7.3 Deferrals and Overrides

<!--
Accept override gracefully: if the author has full context and disagrees, defer to their judgment. Comment on code, not people.
But do not accept "I'll clean it up later" — require cleanup before merge; if it cannot be addressed in this change, file a follow-up item (Section 8) with self-assignment.
-->

| Item | Origin (FIND-XXX) | Author Position | Reviewer Position | Resolution Basis | Follow-up |
|------|------|------|------|------|------|
| <!-- ... --> | <!-- ... --> | <!-- ... --> | <!-- ... --> | <!-- Author override | Technical facts | Style guide | Design principle | Codebase consistency --> | <!-- FU-XXX or none --> |

### 7.4 Merge Gate

<!--
Before merge, confirm:
- All Critical findings resolved.
- All required findings addressed or explicitly deferred with justification (follow-up item filed, Section 8).
- Verification story complete (Section 6).
- Follow-up items tracked (Section 8).
-->

| Gate Check | Done |
|------|------|
| <!-- All Critical findings resolved --> | <!-- ☐ --> |
| <!-- All required findings addressed or explicitly deferred with justification (FU-XXX filed) --> | <!-- ☐ --> |
| <!-- Verification story complete (Section 6) --> | <!-- ☐ --> |
| <!-- Follow-up items tracked (Section 8) --> | <!-- ☐ --> |

---

## 8. Follow-up Management

<!--
Expected content:
- Inventory of follow-up items created by this review (deferrals, won't-fix with justification, dead code cleanup decisions, deferred notes).
- Per item: ID, origin finding, description, self-assigned owner, tracked reference (bug/issue link), status.
- Rules: a deferral is not "I'll clean it up later" — each item needs justification, an owner (self-assignment), and a tracked reference; deferred cleanup never happens without tracking.
- Dead code "safe to remove" items self-assigned per the ask-first decision in 4.7.
-->

| Item ID | Origin (FIND-XXX) | Description | Self-Assigned To | Reference (Issue/Bug) | Status |
|------|------|------|------|------|------|
| <!-- FU-001 --> | <!-- FIND-003 --> | <!-- ... --> | <!-- owner --> | <!-- link --> | <!-- Open | Done --> |

---

## 9. Appendices

<!--
Expected content:
- Reusable references applied in this review: the blank per-change checklist (A), the finding severity reference (B), and the disagreement resolution reference (C).
-->

### Appendix A: Five-Axis Review Checklist (Reusable)

<!--
Blank per-change checklist for any review round.
-->

```markdown
## Review: [PR/Change title]

### Context
- [ ] I understand what this change does and why

### Correctness
- [ ] Change matches spec/task requirements
- [ ] Edge cases handled
- [ ] Error paths handled
- [ ] Tests cover the change adequately

### Readability
- [ ] Names are clear and consistent
- [ ] Logic is straightforward
- [ ] No unnecessary complexity

### Architecture
- [ ] Follows existing patterns
- [ ] No unnecessary coupling or dependencies
- [ ] Appropriate abstraction level

### Security
- [ ] No secrets in code
- [ ] Input validated at boundaries
- [ ] No injection vulnerabilities
- [ ] Auth checks in place
- [ ] External data sources treated as untrusted

### Performance
- [ ] No N+1 patterns
- [ ] No unbounded operations
- [ ] Pagination on list endpoints

### Verification
- [ ] Tests pass
- [ ] Build succeeds
- [ ] Manual verification done (if applicable)

### Verdict
- [ ] Approve — Ready to merge
- [ ] Request changes — Issues must be addressed
```

### Appendix B: Finding Severity Reference

| Label | Meaning | Author Action |
|------|------|------|
| *(no prefix)* | Required change | Must address before merge |
| **Critical:** | Blocks merge | Security vulnerability, data loss, broken functionality |
| **Nit:** | Minor, optional | Author may ignore — formatting, style preferences |
| **Optional:** / **Consider:** | Suggestion | Worth considering but not required |
| **FYI** | Informational only | No action needed — context for future reference |

### Appendix C: Disagreement Resolution Reference

| Priority | Basis | Application |
|------|------|------|
| 1 | **Technical facts and data** | Override opinions and preferences |
| 2 | **Style guides** | Absolute authority on style matters |
| 3 | **Software design** | Evaluated on engineering principles, not personal preference |
| 4 | **Codebase consistency** | Acceptable if it does not degrade overall code health |

---

## Document History

| Version | Date | Author | Changes |
|------|------|------|------|
| 0.1 | <!-- date --> | <!-- name --> | <!-- initial draft --> |
| 1.0 | <!-- date --> | <!-- name --> | <!-- approved/baselined version --> |
