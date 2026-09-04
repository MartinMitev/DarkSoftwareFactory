# Branch

> **Slug:** `branch` | **View:** Version Control View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a named line of development in version control (feature / release / hotfix / main) composed of a sequence of [Code Commit](code-commit.md)s.
- **Purpose / when used:** the unit of parallel development and integration; sources and targets of [Pull Request](pull-request.md)s; feeds an analysis [Release](../analysis/release.md) / [Phase](../analysis/phase.md).

## 2. Semantics (crisp)

`branch` is a named pointer over the commit graph: a `kind` (feature / release / hotfix / main / develop), its base commit, its head commit, and a lifecycle status (open / merged / abandoned). It targets an analysis [Release](../analysis/release.md) and/or [Phase](../analysis/phase.md) (the increment it feeds). A [Pull Request](pull-request.md) sources from and targets a Branch. The branching *model* (GitFlow / Trunk-based / GitHub Flow) is a convention owned by analysis [Constraint](../analysis/constraint.md), not an attribute. It is **not** a single change (→ [Code Commit](code-commit.md)), **not** the deployment event (→ [Release](../analysis/release.md)), **not** a project phase (→ [Phase](../analysis/phase.md)), and **not** the integration proposal (→ [Pull Request](pull-request.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| name | string | yes | e.g. feature/payments-001 |
| kind | enum (feature / release / hotfix / main / develop) | yes | |
| baseCommit | ref → [Code Commit](code-commit.md) | yes | branch point |
| headCommit | ref → [Code Commit](code-commit.md) | yes | current tip |
| targetsRelease | ref → [Release](../analysis/release.md) | no | the release it feeds |
| targetsPhase | ref → [Phase](../analysis/phase.md) | no | the phase it belongs to |
| status | enum (open / merged / abandoned) | yes | |

## 4. State (as-is / target)

Stateless — a VCS construct; lifecycle is open → merged / abandoned.

## 5. Relationships (semantic references)

- **Refers to:** [Code Commit](code-commit.md) (base, head), [Release](../analysis/release.md), [Phase](../analysis/phase.md).
- **Referred by:** [Pull Request](pull-request.md).

## 6. Lifecycle / status

open → merged (via a [Pull Request](pull-request.md)) / abandoned. Branch-model convention is an analysis [Constraint](../analysis/constraint.md).

## 7. Template coverage

- A future `templates/development/*.md` version-control / branching section.
- Maps to the delivery path of analysis [Release](../analysis/release.md) / [Phase](../analysis/phase.md).

## 8. Non-overlap note

A single change belongs to [Code Commit](code-commit.md); the deployment event belongs to [Release](../analysis/release.md); the project-work span belongs to [Phase](../analysis/phase.md); the integration proposal belongs to [Pull Request](pull-request.md). The branching model is a convention (analysis [Constraint](../analysis/constraint.md)).
