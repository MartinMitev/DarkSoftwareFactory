# Code Commit

> **Slug:** `code-commit` | **View:** Version Control View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** an atomic change recorded in version control — hash, author, message, parent commit(s), and the set of modified code units.
- **Purpose / when used:** the atomic unit of version-controlled change; composed into [Branch](branch.md)es and integrated via [Pull Request](pull-request.md)s.

## 2. Semantics (crisp)

`code-commit` is a single VCS change: a hash, an author (analysis [Role](../analysis/role.md) / [Stakeholder](../analysis/stakeholder.md)), a message, parent commit(s), and the set of modified [Code Unit](code-unit.md)s. It realises an analysis [Work Package](../analysis/work-package.md) or [User Story](../analysis/user-story.md) (the increment it delivers) and may reference an analysis [Change Request](../analysis/change-request.md) that motivated it. Commit-message format (Conventional Commits etc.) is a convention owned by analysis [Constraint](../analysis/constraint.md), not an attribute here. It is **not** the source file (→ [Code Unit](code-unit.md)), **not** the line of development (→ [Branch](branch.md)), **not** the review (→ [Pull Request](pull-request.md) / [Code Review](code-review.md)), and **not** the build execution (→ [Build Run](build-run.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| hash | string | yes | VCS commit hash |
| author | ref → [Role](../analysis/role.md) / [Stakeholder](../analysis/stakeholder.md) | yes | |
| message | string | yes | follows a commit-message convention (→ Constraint) |
| parentHashes | string[] | yes | one for normal commits, 2+ for merges |
| modifies | ref[] → [Code Unit](code-unit.md) | yes | added / modified / deleted files |
| realises | ref → [Work Package](../analysis/work-package.md) / [User Story](../analysis/user-story.md) | no | the increment delivered |
| references | ref → [Change Request](../analysis/change-request.md) | no | if change-driven |
| timestamp | datetime | yes | |

## 4. State (as-is / target)

Stateless — a recorded change. History is immutable; later corrections are new commits.

## 5. Relationships (semantic references)

- **Refers to:** [Code Unit](code-unit.md) (modifies), [Role](../analysis/role.md), [Stakeholder](../analysis/stakeholder.md), [Work Package](../analysis/work-package.md), [User Story](../analysis/user-story.md), [Change Request](../analysis/change-request.md).
- **Referred by:** [Branch](branch.md), [Pull Request](pull-request.md), [Build Run](build-run.md).

## 6. Lifecycle / status

Immutable once recorded. Status is implicit in branch/PR state (merged via a PR, abandoned on a deleted branch).

## 7. Template coverage

- A future `templates/development/*.md` version-control / commit-history section.
- Maps to the delivery of analysis [Work Package](../analysis/work-package.md) / [User Story](../analysis/user-story.md) increments.

## 8. Non-overlap note

The source file belongs to [Code Unit](code-unit.md); the line of development belongs to [Branch](branch.md); the review belongs to [Pull Request](pull-request.md) / [Code Review](code-review.md); the build execution belongs to [Build Run](build-run.md). Commit-message format is a convention (analysis [Constraint](../analysis/constraint.md)).
