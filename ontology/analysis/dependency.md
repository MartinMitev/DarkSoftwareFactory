# Dependency

> **Slug:** `dependency` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a relies-on relationship — internal, external, technical, data, or infrastructure — with owner, due date, impact-if-not-met, and mitigation.
- **Purpose / when used:** the single dependency artefact across business case, scope, SRS, user stories, and project plan.

## 2. Semantics (crisp)

`dependency` is a **relies-on relationship**: the project needs X (another project, a shared service, a vendor delivery, a regulatory approval, a framework release, a cloud feature, source data quality) — typed (internal / external / technical / data / infrastructure) with an owner, a due date, the impact if not met, and a mitigation. It is **not** a constraint (a limitation — → [Constraint](constraint.md)) and **not** an assumption (a stated belief — → [Assumption](assumption.md)). For Brown Field / Modernization it includes legacy-system dependencies and data-migration dependencies.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| type | enum (internal / external / technical / data / infrastructure) | yes | |
| statement | string | yes | what is relied on |
| owner | ref → [Stakeholder](stakeholder.md) | yes | |
| dueDate | date | yes | |
| impactIfNotMet | string | yes | |
| mitigation | string | yes | |

## 4. State (as-is / target)

Stateless — a relationship.

## 5. Relationships (semantic references)

- **Refers to:** [Stakeholder](stakeholder.md) (owner), [Work Package](work-package.md), [Data Migration](data-migration.md).
- **Referred by:** [Work Package](work-package.md).

## 6. Lifecycle / status

N/A — relationship; resolved or managed.

## 7. Template coverage

- `templates/analysis/business-case.md` §14.1 Dependencies
- `templates/analysis/project-scope.md` §13.3 Scope Dependencies
- `templates/analysis/software-requirements-specification.md` §12.4 Requirements Dependencies
- `templates/analysis/user-stories.md` §7 Story Dependencies & Sequencing
- `templates/analysis/project-plan.md` §7.5 Critical Path Analysis

## 8. Non-overlap note

A limitation belongs to [Constraint](constraint.md); a stated belief belongs to [Assumption](assumption.md).
