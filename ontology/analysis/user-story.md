# User Story

> **Slug:** `user-story` | **Layer:** L3 Requirements | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a deliverable increment for a persona ("As a … I want … so that …"), estimated, prioritised, and assigned to a release.
- **Purpose / when used:** the backlog unit the delivery team plans, estimates, and ships sprint by sprint; translates requirements into delivery-sized units.

## 2. Semantics (crisp)

`user-story` is a **deliverable increment** with a story statement, persona, epic, MoSCoW priority, story points, sprint/release assignment, status, SRS trace, and dependencies. It is **not** a requirement (the formal contract — → [Requirement](requirement.md)), **not** a use case (the interaction spec — → [Use Case](use-case.md)), and **not** an epic (the grouping — → [Epic](epic.md)). For Brown Field / Modernization, stories that modify existing behaviour reference the existing behaviour, and parity stories replicate legacy behaviour. It is a *journey* artefact — inherently about incremental delivery.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. US-001 |
| statement | string | yes | "As a … I want … so that …" |
| epic | ref → [Epic](epic.md) | yes | |
| persona | ref → [Persona](persona.md) | yes | |
| MoSCoW | enum (Must / Should / Could) | yes | |
| points | int | yes | Fibonacci |
| sprintRelease | ref → [Release](release.md) | no | |
| status | enum (Backlog / Ready / In Progress / In Review / Done / Blocked / Removed) | yes | |
| srsTrace | ref[] → [Requirement](requirement.md) | yes | |
| dependencies | ref[] → [Dependency](dependency.md) | no | |
| existingBehavior | string | no | 🟤🔵 |

## 4. State (as-is / target)

Journey — a delivery increment; state follows its lifecycle below.

## 5. Relationships (semantic references)

- **Refers to:** [Persona](persona.md), [Role](role.md), [Epic](epic.md), [Requirement](requirement.md), [Acceptance Criterion](acceptance-criterion.md), [Scope Item](scope-item.md).
- **Referred by:** [Acceptance Criterion](acceptance-criterion.md), [Epic](epic.md), [Estimate](estimate.md), [Persona](persona.md), [Quality Gate](quality-gate.md), [Release](release.md), [Requirement](requirement.md).

## 6. Lifecycle / status

Draft → Backlog → Ready → In Progress → In Review → Done; Blocked / Removed as side states. Minor changes by [Product Owner](role.md); major changes via [Change Request](change-request.md).

## 7. Template coverage

- `templates/analysis/user-stories.md` §4 User Stories (incl. §4.1 registry, §4.2 detailed specs), §10 Story Splitting Guide (§10.1 when to split, §10.2 patterns), §11.1 Feature Parity Stories, §11.3 Transition Stories
- `templates/analysis/project-scope.md` §5.2 User Stories / Epics
- `templates/analysis/software-requirements-specification.md` §5 Use Cases (story trace)

## 8. Non-overlap note

The formal contract belongs to [Requirement](requirement.md); the interaction detail belongs to [Use Case](use-case.md); the grouping belongs to [Epic](epic.md).
