# Acceptance Criterion

> **Slug:** `acceptance-criterion` | **Layer:** L3 Requirements | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a measurable Given/When/Then condition that must be true for a user story or requirement to be considered done.
- **Purpose / when used:** the pass/fail test condition at the story/requirement level; includes parity criteria for migrated features.

## 2. Semantics (crisp)

`acceptance-criterion` is a **single pass/fail test condition** in Given/When/Then form (functional, error, edge, NFR, or parity). It is **not** the quality gate (a checkpoint — → [Quality Gate](quality-gate.md)), **not** the requirement (the contract — → [Requirement](requirement.md)), and **not** the user story (the increment — → [User Story](user-story.md)). For Brown Field / Modernization, parity criteria specify the exact legacy behaviour to preserve and the verification method. Every story must have at least one AC.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. US-001.AC-1 |
| type | enum (functional / error / edge / NFR / parity) | yes | |
| given | string | yes | |
| when | string | yes | |
| then | string | yes | |
| parityLevel | enum (100% / Partial) | no | 🟤🔵 |
| verificationMethod | string | no | 🟤🔵 parallel test / comparison / UAT |

## 4. State (as-is / target)

Journey — a test condition verified during delivery.

## 5. Relationships (semantic references)

- **Refers to:** [User Story](user-story.md), [Requirement](requirement.md).
- **Referred by:** [Deliverable](deliverable.md), [Quality Gate](quality-gate.md), [User Story](user-story.md).

## 6. Lifecycle / status

N/A — test condition; verified at acceptance.

## 7. Template coverage

- `templates/analysis/user-stories.md` §5 Acceptance Criteria (incl. §5.2 by story, §5.3 parity)
- `templates/analysis/software-requirements-specification.md` §14.3 Acceptance Test Requirements
- `templates/analysis/project-scope.md` §11.1 Product Acceptance Criteria

## 8. Non-overlap note

The checkpoint enforcement belongs to [Quality Gate](quality-gate.md); the contract belongs to [Requirement](requirement.md).
