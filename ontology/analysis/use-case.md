# Use Case

> **Slug:** `use-case` | **Layer:** L3 Requirements | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** an interaction between actors and the system to achieve a goal, with main/alternative/exception flows, preconditions, and postconditions.
- **Purpose / when used:** captures actor↔system behaviour; traces to functional requirements; the "actor" notion (human or system) is folded into this artefact's participants.

## 2. Semantics (crisp)

`use-case` is an **interaction specification** between actors and the system: a primary actor (and secondary actors) trigger a main success scenario with alternative and exception flows, preconditions and postconditions. Human actors reference a [Persona](persona.md) and/or [Role](role.md); system actors reference an [Interface](interface.md) — the separate "actor" concept is **folded into** the use case's `participants`, not a standalone artefact. It is **not** a user story (deliverable increment — → [User Story](user-story.md)), **not** a business process (orchestrated workflow — → [Business Process](business-process.md)), and **not** a requirement (the contract — → [Requirement](requirement.md)); it traces to one or more requirements.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. UC-001 |
| name | string | yes | |
| primaryActor | ref → [Persona](persona.md) / [Role](role.md) / [Interface](interface.md) | yes | the "actor" folded here |
| secondaryActors | ref[] → [Persona](persona.md) / [Role](role.md) / [Interface](interface.md) | no | |
| trigger | string | yes | |
| preconditions | string | yes | |
| mainFlow | string[] | yes | numbered actor↔system steps |
| altFlows | table[] | no | |
| exceptionFlows | table[] | no | |
| postconditions | string | yes | |
| frequency | string | yes | |
| MoSCoW | enum (Must / Should / Could) | yes | |
| tracesTo | ref[] → [Requirement](requirement.md) | yes | |

## 4. State (as-is / target)

Stateful. As-is use cases (existing interactions) vs target use cases. Brown Field marks preserved use cases to avoid duplication; Modernization focuses on behavioural differences from legacy.

## 5. Relationships (semantic references)

- **Refers to:** [Persona](persona.md), [Role](role.md), [Interface](interface.md), [Requirement](requirement.md), [Business Rule](business-rule.md).
- **Referred by:** [Persona](persona.md), [Requirement](requirement.md), [Verification & Validation](verification-validation.md).

## 6. Lifecycle / status

Status: Draft → Reviewed → Approved. Changes via [Change Request](change-request.md).

## 7. Template coverage

- `templates/analysis/software-requirements-specification.md` §3.2 Actor Definitions, §5 Use Cases (incl. §5.3 Use Case Diagrams)

## 8. Non-overlap note

The deliverable increment belongs to [User Story](user-story.md); the orchestrated business workflow belongs to [Business Process](business-process.md); the contract belongs to [Requirement](requirement.md).
