# Requirement

> **Slug:** `requirement` | **Layer:** L3 Requirements | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a testable statement of what the system must do (functional) or how well it must perform (non-functional), prioritised and traced to a capability or business process.
- **Purpose / when used:** the authoritative contract for system behaviour; every functional requirement traces to a capability/process, every non-functional requirement states a measurable quality target.

## 2. Semantics (crisp)

`requirement` has two variants: **functional** ("The system shall X", category=`functional`) and **non-functional** (a quality attribute with a measurable target, category=`non-functional`, with an `nfrCategory`: performance, availability, security, scalability, maintainability, operability, compatibility, accessibility). It is written as WHAT, not HOW (design belongs to the design phase). It is prioritised MoSCoW and traced to a [Capability](capability.md) or [Business Process](business-process.md), to a [Scope Item](scope-item.md), and forward to [Use Case](use-case.md) / [User Story](user-story.md) / test. It is **not** a regulatory obligation (→ [Compliance Requirement](compliance-requirement.md)), **not** a deliverable increment (→ [User Story](user-story.md)), and **not** design. A security NFR (nfrCategory=security) **realises** a [Compliance Requirement](compliance-requirement.md); the obligation lives there.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. FR-001, NFR-001 |
| category | enum (functional / non-functional) | yes | |
| nfrCategory | enum (performance / availability / security / scalability / maintainability / operability / compatibility / accessibility) | conditional | required for NFR |
| statement | string | yes | "The system shall…" or measurable target |
| MoSCoW | enum (Must / Should / Could / Won't) | yes | |
| verificationMethod | enum (demo / test / inspection / analysis) | yes | |
| status | enum (Draft / Approved / Implemented / Verified) | yes | |
| tracesTo | ref[] | yes | → [Capability](capability.md) / [Business Process](business-process.md) / [Scope Item](scope-item.md) / [Objective](objective.md) / [Compliance Requirement](compliance-requirement.md) |

## 4. State (as-is / target)

Stateful. As-is requirements (existing behaviour) vs target requirements. Brown Field marks preserved/modified; Modernization marks parity requirements.

## 5. Relationships (semantic references)

- **Refers to:** [Capability](capability.md), [Business Process](business-process.md), [Scope Item](scope-item.md), [Objective](objective.md), [Compliance Requirement](compliance-requirement.md), [Use Case](use-case.md), [Business Rule](business-rule.md), [Data Entity](data-entity.md), [Interface](interface.md), [User Story](user-story.md).
- **Referred by:** [Acceptance Criterion](acceptance-criterion.md), [Business Rule](business-rule.md), [Capability](capability.md), [Change Request](change-request.md), [Compliance Requirement](compliance-requirement.md), [Data Entity](data-entity.md), [Epic](epic.md), [Interface](interface.md), [Objective](objective.md), [Proof of Concept](proof-of-concept.md), [Quality Gate](quality-gate.md), [Scope Item](scope-item.md), [Use Case](use-case.md), [User Story](user-story.md), [Verification & Validation](verification-validation.md).

## 6. Lifecycle / status

Status: Draft → Approved → Implemented → Verified. Changes go through [Change Request](change-request.md).

## 7. Template coverage

- `templates/analysis/software-requirements-specification.md` §4 Functional Requirements, §9 Non-Functional Requirements, §13 Requirement Traceability (§13.1 forward, §13.2 backward, §13.3 coverage report)
- `templates/analysis/project-scope.md` §5 Functional Requirements, §6 Non-Functional Requirements
- `templates/analysis/user-stories.md` §6 Non-Functional Story Attributes (NFR mapping)
- `templates/analysis/business-case.md` §2.3 Scope, §11 Implementation Plan (requirement refs)
- `templates/analysis/project-plan.md` §4 Project Scope Summary (requirement refs)

## 8. Non-overlap note

Regulatory obligation belongs to [Compliance Requirement](compliance-requirement.md). The deliverable increment belongs to [User Story](user-story.md). Design belongs to the design phase, not here.
