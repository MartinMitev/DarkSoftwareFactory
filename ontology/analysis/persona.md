# Persona

> **Slug:** `persona` | **Layer:** L2 Business Architecture | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a user type with goals, pain points, and usage patterns — a human-centred archetype.
- **Purpose / when used:** drives use cases, user stories, and UI/UX scope; referenced by roles and use cases.

## 2. Semantics (crisp)

`persona` is a **human-centred archetype** — a distinct type of user with role, technical proficiency, key goals, pain points, and usage frequency. It is **not** a permission set (→ [Role](role.md)) and **not** a use-case actor binding (→ [Use Case](use-case.md) participants). A persona maps to a [Role](role.md); one persona may hold several roles and vice versa. Brown Field / Modernization include existing personas and any new ones introduced.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| name | string | yes | |
| role | ref → [Role](role.md) | yes | mapped role |
| proficiency | enum (low / medium / high) | yes | technical proficiency |
| goals | string | yes | key goals |
| painPoints | string | yes | |
| frequency | string | yes | usage frequency |

## 4. State (as-is / target)

Stateful. As-is personas (current users) vs target personas (new user types introduced). Change type marks new/preserved.

## 5. Relationships (semantic references)

- **Refers to:** [Role](role.md), [User Story](user-story.md), [Use Case](use-case.md).
- **Referred by:** [Role](role.md), [Stakeholder](stakeholder.md), [Use Case](use-case.md), [User Story](user-story.md).

## 6. Lifecycle / status

N/A — definition; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/software-requirements-specification.md` §3.1 User Personas
- `templates/analysis/user-stories.md` §4 User Stories (persona per story)
- `templates/analysis/project-scope.md` §5.2 User Stories / Epics (persona)

## 8. Non-overlap note

Permissions belong to [Role](role.md). Use-case participant binding belongs to [Use Case](use-case.md).
