# Lesson Learned

> **Slug:** `lesson-learned` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a captured, actionable lesson — category (process/technical/people/governance/vendors/migration), context, action, owner, and status.
- **Purpose / when used:** the atomic insight collected during and after the project; referenced by the post-implementation review.

## 2. Semantics (crisp)

`lesson-learned` is a **single actionable insight**: a lesson, a category (process, technical, people, governance, vendors, migration), a context, an action, an owner, and a status. It is **not** the review event (→ [Post-Implementation Review](post-implementation-review.md)) — the review collects many lessons. It is the unit that gets disseminated to other projects/teams.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| lesson | string | yes | |
| category | enum (process / technical / people / governance / vendors / migration) | yes | |
| context | string | yes | |
| action | string | yes | |
| owner | ref → [Stakeholder](stakeholder.md) | yes | |
| status | enum (open / actioned / closed) | yes | |

## 4. State (as-is / target)

Stateless — an insight.

## 5. Relationships (semantic references)

- **Refers to:** [Post-Implementation Review](post-implementation-review.md), [Stakeholder](stakeholder.md) (owner).
- **Referred by:** [Post-Implementation Review](post-implementation-review.md).

## 6. Lifecycle / status

Status: open → actioned → closed.

## 7. Template coverage

- `templates/analysis/business-case.md` §16.3 Lessons Learned Capture
- `templates/analysis/project-plan.md` §19.4 Lessons Learned

## 8. Non-overlap note

The review event belongs to [Post-Implementation Review](post-implementation-review.md). Lesson Learned owns the single insight.
