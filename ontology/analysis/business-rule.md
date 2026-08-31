# Business Rule

> **Slug:** `business-rule` | **Layer:** L3 Requirements | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a statement that defines or constrains business behaviour — decision, calculation, validation, constraint, derivation, or workflow rule — sourced from regulation, policy, or a business process.
- **Purpose / when used:** captures the business logic that governs system behaviour; drives requirements; may be expressed as a decision table.

## 2. Semantics (crisp)

`business-rule` is a **business-logic statement** (categorised decision / calculation / validation / constraint / derivation / workflow), attributed to a source (regulation, policy, business process, existing system). It is **not** a system design decision, **not** a requirement ("system shall" — → [Requirement](requirement.md)), and **not** a regulatory obligation (→ [Compliance Requirement](compliance-requirement.md)) — a compliance requirement *drives* business rules. Complex conditional logic is expressed as a decision table. For Brown Field / Modernization, rules carry a `changeType` (new / preserved / modified / retired) and tribal-knowledge rules are captured.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. BR-001 |
| category | enum (decision / calculation / validation / constraint / derivation / workflow) | yes | |
| statement | string | yes | |
| source | string | yes | regulation / policy / business process / existing system |
| changeType | enum (new / preserved / modified / retired) | no | 🟤🔵 |
| decisionTable | table | no | for complex conditional logic |

## 4. State (as-is / target)

Stateful. As-is rules (current logic) vs target rules. Change type marks preserved/modified/retired.

## 5. Relationships (semantic references)

- **Refers to:** [Requirement](requirement.md), [Business Process](business-process.md), [Compliance Requirement](compliance-requirement.md).
- **Referred by:** [Business Process](business-process.md), [Requirement](requirement.md), [Use Case](use-case.md).

## 6. Lifecycle / status

Status: Draft → Reviewed → Approved. Changes via [Change Request](change-request.md).

## 7. Template coverage

- `templates/analysis/software-requirements-specification.md` §6 Business Rules & Decision Logic
- `templates/analysis/project-scope.md` §5.3 Business Rules & Logic
- `templates/analysis/software-requirements-specification.md` Appendix F (Business Rule Catalog)

## 8. Non-overlap note

The regulatory obligation belongs to [Compliance Requirement](compliance-requirement.md); the "system shall" belongs to [Requirement](requirement.md). Business rules drive both.
