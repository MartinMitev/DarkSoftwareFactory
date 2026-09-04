# Static Analysis Finding

> **Slug:** `static-analysis-finding` | **View:** Code Quality View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a code-quality or security issue reported by a static analysis tool — rule, severity, location (file:line) — that may be triaged into a tracked issue or debt item.
- **Purpose / when used:** the raw tool output of automated code analysis; complements the human [Code Review](code-review.md) and feeds analysis [Issue](../analysis/issue.md) / [Technical Debt Item](../analysis/technical-debt-item.md) tracking.

## 2. Semantics (crisp)

`static-analysis-finding` is the raw tool output: a tool, a rule id, a severity (critical / major / minor / info), a category (bug / vulnerability / code-smell / security-hotspot), a location ([Code Unit](code-unit.md):line), and a status (open / triaged / false-positive / fixed). When triaged it *becomes* an analysis [Issue](../analysis/issue.md) or [Technical Debt Item](../analysis/technical-debt-item.md) — it is **not** the tracked problem itself (→ Issue / Technical Debt Item). It is **not** a [Code Review](code-review.md) finding (a review finding is human; this is tool-reported), and **not** a test failure (→ testing phase). It may be resolved by a [Refactoring](refactoring.md) and is often surfaced inside a [Pull Request](pull-request.md) (via a [Build Run](build-run.md) that runs the analyser).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. SAF-001 |
| tool | string | yes | SonarQube / Semgrep / CodeQL / … |
| ruleId | string | yes | the violated rule |
| severity | enum (critical / major / minor / info) | yes | |
| category | enum (bug / vulnerability / code-smell / security-hotspot) | yes | |
| location | ref → [Code Unit](code-unit.md) + line | yes | |
| status | enum (open / triaged / false-positive / fixed) | yes | |
| triagesTo | ref → [Issue](../analysis/issue.md) / [Technical Debt Item](../analysis/technical-debt-item.md) | no | set on triage |
| resolvedBy | ref → [Refactoring](refactoring.md) | no | the refactoring that fixes it |

## 4. State (as-is / target)

Stateless — a tool report; lifecycle open → triaged → fixed / false-positive.

## 5. Relationships (semantic references)

- **Refers to:** [Code Unit](code-unit.md) (location), [Issue](../analysis/issue.md), [Technical Debt Item](../analysis/technical-debt-item.md) (triages to), [Refactoring](refactoring.md) (resolved by).
- **Referred by:** [Code Review](code-review.md) (cited), [Refactoring](refactoring.md) (resolves), [Pull Request](pull-request.md) (surfaced via a [Build Run](build-run.md)).

## 6. Lifecycle / status

open → triaged (→ becomes [Issue](../analysis/issue.md) / [Technical Debt Item](../analysis/technical-debt-item.md)) → fixed (via [Refactoring](refactoring.md)) / false-positive. Suppressed findings retain a record with `status=false-positive` + rationale.

## 7. Template coverage

- A future `templates/development/*.md` code-quality / static-analysis section.
- Feeds analysis [Issue](../analysis/issue.md) / [Technical Debt Item](../analysis/technical-debt-item.md) tracking for `templates/design/software-architecture.md` §12 Risks and Technical Debts.

## 8. Non-overlap note

The tracked problem belongs to analysis [Issue](../analysis/issue.md) / [Technical Debt Item](../analysis/technical-debt-item.md); the human review finding belongs to [Code Review](code-review.md); the test failure belongs to the testing phase. The finding is the raw tool report — it *becomes* a tracked problem on triage.
