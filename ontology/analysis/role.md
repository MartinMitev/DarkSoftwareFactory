# Role

> **Slug:** `role` | **Layer:** L2 Business Architecture | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a responsibility and permission set that a person or system can hold within processes and the system.
- **Purpose / when used:** defines access/permission bundles and accountability; referenced by processes, RACI, applications, use cases, governance, and stakeholder mapping.

## 2. Semantics (crisp)

`role` is an **access/permission bundle with accountability** — a defined set of permissions and access levels, optionally with a `parentRole` (hierarchy / inheritance) and a persona mapping. It is **not** a user persona (a user with goals — → [Persona](persona.md)) and **not** a use-case actor binding (→ [Use Case](use-case.md) participants). A role may be mapped to a persona; many people can hold one role. For Brown Field / Modernization, a role carries a `changeType` (new / preserved / modified).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| name | string | yes | |
| permissions | string | yes | access levels |
| parentRole | ref → [Role](role.md) | no | parent role in the hierarchy (inheritance) |
| personaMapping | ref → [Persona](persona.md) | no | which persona this role serves |
| changeType | enum (new / preserved / modified) | no | 🟤🔵 |

## 4. State (as-is / target)

Stateful. As-is roles (current permission model) vs target roles. Change type marks preserved/modified/new.

## 5. Relationships (semantic references)

- **Refers to:** [Persona](persona.md), [Business Process](business-process.md), [Role](role.md) (parentRole).
- **Referred by:** [Application](application.md), [Business Process](business-process.md), [Cutover](cutover.md), [Governance](governance.md), [Persona](persona.md), [RACI Assignment](raci-assignment.md), [Role](role.md) (parentRole), [Stakeholder](stakeholder.md), [Use Case](use-case.md), [User Story](user-story.md).

## 6. Lifecycle / status

N/A — definition; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/software-requirements-specification.md` §3.3 User Roles & Permissions
- `templates/analysis/project-plan.md` §6 Roles & Responsibilities, §12.1 Team Composition, §12.2 Resource Calendar, §12.3 Skill Development Plan
- `templates/analysis/business-case.md` §12.1 Team & Staffing (role definitions)
- `templates/analysis/viability-study.md` §8.2 Team & Capability Assessment

## 8. Non-overlap note

A user with goals belongs to [Persona](persona.md). Use-case participant binding belongs to [Use Case](use-case.md).
