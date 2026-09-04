# Pull Request

> **Slug:** `pull-request` | **View:** Version Control View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a proposal to merge a source [Branch](branch.md) into a target branch, gated by review and CI, that integrates a set of [Code Commit](code-commit.md)s.
- **Purpose / when used:** the integration and review unit; the gate that controls what enters main/release branches.

## 2. Semantics (crisp)

`pull-request` is the integration/review unit: a source and target [Branch](branch.md), the contained [Code Commit](code-commit.md)s, a status (open / approved / merged / rejected / closed), the [Code Review](code-review.md)s it carries, and the analysis [Quality Gate](../analysis/quality-gate.md)s it must pass (definition-of-done / merge-readiness). It realises an analysis [User Story](../analysis/user-story.md) / [Scope Item](../analysis/scope-item.md). It is **not** the review itself (→ [Code Review](code-review.md)), **not** a commit, **not** a branch, and **not** a quality gate (it is *gated by* one — a gate decides readiness, the PR is the proposal). A [Build Run](build-run.md) may be triggered by a PR.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. PR-001 |
| sourceBranch | ref → [Branch](branch.md) | yes | |
| targetBranch | ref → [Branch](branch.md) | yes | |
| containsCommits | ref[] → [Code Commit](code-commit.md) | yes | |
| reviews | ref[] → [Code Review](code-review.md) | yes | |
| gatedBy | ref[] → [Quality Gate](../analysis/quality-gate.md) | yes | DoD / merge-readiness gates |
| realises | ref → [User Story](../analysis/user-story.md) / [Scope Item](../analysis/scope-item.md) | no | the increment integrated |
| status | enum (open / approved / merged / rejected / closed) | yes | |

## 4. State (as-is / target)

Stateless — a VCS/forge construct; lifecycle open → approved → merged / rejected / closed.

## 5. Relationships (semantic references)

- **Refers to:** [Branch](branch.md), [Code Commit](code-commit.md), [Code Review](code-review.md), [Quality Gate](../analysis/quality-gate.md), [User Story](../analysis/user-story.md), [Scope Item](../analysis/scope-item.md).
- **Referred by:** [Code Review](code-review.md), [Build Run](build-run.md).

## 6. Lifecycle / status

open → approved → merged (the source branch becomes `merged`) / rejected / closed. Re-opened on request-changes.

## 7. Template coverage

- A future `templates/development/*.md` integration / pull-request section.
- Maps to the integration of analysis [User Story](../analysis/user-story.md) / [Scope Item](../analysis/scope-item.md) increments; gated by [Quality Gate](../analysis/quality-gate.md).

## 8. Non-overlap note

The review belongs to [Code Review](code-review.md); the commit belongs to [Code Commit](code-commit.md); the branch belongs to [Branch](branch.md); the gate belongs to analysis [Quality Gate](../analysis/quality-gate.md). The PR is the proposal that ties them together.
