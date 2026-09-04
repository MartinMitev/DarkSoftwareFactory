# Code Review

> **Slug:** `code-review` | **View:** Version Control View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the peer review record of a [Pull Request](pull-request.md) — reviewer, findings, verdict — distinct from the gate that requires it.
- **Purpose / when used:** the human-judgement control on code changes; complements automated [Static Analysis Finding](static-analysis-finding.md)s and analysis [Quality Gate](../analysis/quality-gate.md)s.

## 2. Semantics (crisp)

`code-review` is the review record: a reviewer (analysis [Role](../analysis/role.md)), findings (comments / issues / suggestions linked to [Code Unit](code-unit.md) locations), a verdict (approve / request-changes / reject), and a date. It may surface or reference [Static Analysis Finding](static-analysis-finding.md)s that the reviewer used as evidence. It is **not** the pull request (it reviews one), **not** a quality gate (a gate may *require* a review; the review is the human verdict), **not** an analysis [Issue](../analysis/issue.md) (a review finding that is triaged becomes an Issue), and **not** a tool finding (→ [Static Analysis Finding](static-analysis-finding.md) — tool-reported, not human).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. CR-001 |
| reviewer | ref → [Role](../analysis/role.md) | yes | |
| reviewsPR | ref → [Pull Request](pull-request.md) | yes | |
| findings | table (location → [Code Unit](code-unit.md):line / type / comment) | yes | human findings |
| verdict | enum (approve / request-changes / reject) | yes | |
| referencesFindings | ref[] → [Static Analysis Finding](static-analysis-finding.md) | no | tool findings cited |
| date | date | yes | |

## 4. State (as-is / target)

Stateless — a review record; superseded by a new review on re-review.

## 5. Relationships (semantic references)

- **Refers to:** [Pull Request](pull-request.md) (reviews), [Role](../analysis/role.md), [Code Unit](code-unit.md) (finding locations), [Static Analysis Finding](static-analysis-finding.md) (cited).
- **Referred by:** [Pull Request](pull-request.md).

## 6. Lifecycle / status

N/A — a recorded verdict. A re-review after request-changes is a new Code Review on the same PR.

## 7. Template coverage

- A future `templates/development/*.md` code-review / peer-review section.
- Complements analysis [Quality Gate](../analysis/quality-gate.md) (a gate may require N approvals).

## 8. Non-overlap note

The pull request belongs to [Pull Request](pull-request.md); the gate belongs to analysis [Quality Gate](../analysis/quality-gate.md); the tracked problem belongs to analysis [Issue](../analysis/issue.md); the tool finding belongs to [Static Analysis Finding](static-analysis-finding.md). The review is the human verdict.
