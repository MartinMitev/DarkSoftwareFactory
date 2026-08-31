# Constraint

> **Slug:** `constraint` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a limitation — budget, schedule, technical, resource, regulatory, organizational, backward-compatibility, uptime, vendor, or convention — with an impact and a flexibility level.
- **Purpose / when used:** the single constraint artefact across business case, scope, SRS, and the design-phase architecture constraints (technical, organizational, conventions, legacy).

## 2. Semantics (crisp)

`constraint` is a **hard or soft limit** on the project: a type (budget, schedule, technical, resource, regulatory, organizational, backward-compat, uptime, vendor, **convention**), the statement, the impact, and a flexibility level (fixed / limited / negotiable). The `convention` type covers design-time architectural conventions — programming guidelines, REST API naming rules, versioning strategy, documentation/naming conventions — that constrain architects during design. It is **not** an assumption (a stated belief — → [Assumption](assumption.md)) and **not** a dependency (a relies-on relationship — → [Dependency](dependency.md)). Regulatory constraints are linked to a [Compliance Requirement](compliance-requirement.md).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| type | enum (budget / schedule / technical / resource / regulatory / organizational / backward-compat / uptime / vendor / convention) | yes | convention = design-time architectural conventions | |
| statement | string | yes | |
| impact | string | yes | |
| flexibility | enum (fixed / limited / negotiable) | yes | |

## 4. State (as-is / target)

Stateless — a limitation.

## 5. Relationships (semantic references)

- **Refers to:** [Compliance Requirement](compliance-requirement.md) (for regulatory constraints).
- **Referred by:** [Compliance Requirement](compliance-requirement.md).

## 6. Lifecycle / status

N/A — limitation; revised as conditions change.

## 7. Template coverage

- `templates/analysis/business-case.md` §14.3 Constraints
- `templates/analysis/project-scope.md` §13.2 Scope Constraints
- `templates/analysis/software-requirements-specification.md` §12.1 Technical Constraints, §12.2 Business Constraints
- `templates/design/software-architecture.md` §3 Architecture Constraints (§3.1 Technical, §3.2 Organizational, §3.3 Conventions, §3.4 Legacy System Constraints)

## 8. Non-overlap note

A stated belief belongs to [Assumption](assumption.md); a relies-on relationship belongs to [Dependency](dependency.md).
