# Assumption

> **Slug:** `assumption` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a stated belief taken as true that underpins the analysis, with category, impact-if-wrong, validation method, and owner.
- **Purpose / when used:** the single assumption artefact across business case, scope, SRS, and project plan.

## 2. Semantics (crisp)

`assumption` is a **stated belief taken as true** — categorised (business, technical, financial, organizational, regulatory) with an impact-if-wrong, a validation method, and an owner. It is **not** a constraint (a hard/soft limit — → [Constraint](constraint.md)) and **not** a dependency (a relies-on relationship — → [Dependency](dependency.md)). A gap may become an assumption when deferred with user acknowledgment. For Brown Field / Modernization it includes assumptions about the existing system (stability, documentation accuracy, data quality).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| category | enum (business / technical / financial / organizational / regulatory) | yes | |
| statement | string | yes | |
| impactIfWrong | string | yes | |
| validationMethod | string | yes | |
| owner | ref → [Stakeholder](stakeholder.md) | yes | |

## 4. State (as-is / target)

Stateless — a stated belief.

## 5. Relationships (semantic references)

- **Refers to:** [Stakeholder](stakeholder.md) (owner), [Gap & Contradiction](gap-and-contradiction.md) (origin).
- **Referred by:** [Gap & Contradiction](gap-and-contradiction.md), [Refined Project Concept](refined-project-concept.md).

## 6. Lifecycle / status

N/A — belief; validated or revised over time.

## 7. Template coverage

- `templates/analysis/business-case.md` §14.2 Assumptions
- `templates/analysis/project-scope.md` §13.1 Scope Assumptions
- `templates/analysis/software-requirements-specification.md` §12.3 Requirements Assumptions
- `templates/analysis/project-plan.md` §8.4 Financial Assumptions
- `templates/analysis/viability-study.md` (assumptions across sections)

## 8. Non-overlap note

A limitation belongs to [Constraint](constraint.md); a relies-on relationship belongs to [Dependency](dependency.md); a missing piece of info belongs to [Gap & Contradiction](gap-and-contradiction.md).
