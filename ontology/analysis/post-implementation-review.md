# Post-Implementation Review

> **Slug:** `post-implementation-review` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a scheduled post-go-live review — timing, scope, reviewers, deliverable, and benefit-realization tracking.
- **Purpose / when used:** hindsight value check; references benefits, KPIs, and objectives; collects lessons.

## 2. Semantics (crisp)

`post-implementation-review` is the **review event** after go-live: a timing (3 / 6 / 12 / 24 / 36 months post-go-live), a scope (benefit realization, technical performance, user satisfaction), reviewers, a deliverable, and benefit-realization tracking (which benefits, KPI, method, frequency, owner, review milestone). It references [Benefit](benefit.md), [KPI](kpi.md), [Objective](objective.md), and [Milestone](milestone.md), and it collects [Lesson Learned](lesson-learned.md) entries. It is **not** a single lesson (→ [Lesson Learned](lesson-learned.md)) and **not** a success criterion (→ [Success Criterion](success-criterion.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| review | string | yes | review name |
| timing | string | yes | when post-go-live |
| scope | string | yes | what is assessed |
| reviewers | ref[] → [Stakeholder](stakeholder.md) | yes | |
| deliverable | string | yes | PIR report |
| benefitTracking | table | yes | benefit / KPI / method / frequency / owner |

## 4. State (as-is / target)

Stateless — a review event.

## 5. Relationships (semantic references)

- **Refers to:** [Benefit](benefit.md), [KPI](kpi.md), [Objective](objective.md), [Milestone](milestone.md), [Lesson Learned](lesson-learned.md).
- **Referred by:** [Lesson Learned](lesson-learned.md).

## 6. Lifecycle / status

N/A — event; scheduled and conducted.

## 7. Template coverage

- `templates/analysis/business-case.md` §16 Post-Implementation Review Plan (§16.1 benefit tracking, §16.2 schedule)
- `templates/analysis/project-plan.md` §19.3 Post-Implementation Review Plan

## 8. Non-overlap note

A single actionable insight belongs to [Lesson Learned](lesson-learned.md). Post-Implementation Review owns the review event.
