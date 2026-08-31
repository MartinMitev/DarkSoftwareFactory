# Stakeholder

> **Slug:** `stakeholder` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a party that influences, approves, or is affected by the project — with role/interest, influence level, attitude, and engagement approach.
- **Purpose / when used:** the single stakeholder identity artefact; referenced by communication plans, governance, and engagement.

## 2. Semantics (crisp)

`stakeholder` is a **person or group with a stake** — internal (executive sponsors, budget holders, development teams, operations, support, end-user departments) or external (customers, partners, regulators, vendors, auditors) — with a role/interest, an influence level (High/Medium/Low), an attitude (champion/neutral/resistant), and an engagement approach. It references (it does not redefine) a [Role](role.md) and/or [Persona](persona.md), and is engaged via a [Communication Plan](communication-plan.md). It is **not** the role definition (→ [Role](role.md)) and **not** the engagement plan (→ [Communication Plan](communication-plan.md)). For Brown Field / Modernization it includes stakeholders affected by the transition (current users, legacy support, vendor contacts).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| name | string | yes | |
| roleOrInterest | string | yes | |
| influence | enum (High / Medium / Low) | yes | |
| attitude | enum (champion / neutral / resistant) | yes | |
| engagementApproach | string | yes | |
| internalExternal | enum (internal / external) | yes | |

## 4. State (as-is / target)

Stateless — a stakeholder identity.

## 5. Relationships (semantic references)

- **Refers to:** [Role](role.md), [Persona](persona.md), [Communication Plan](communication-plan.md).
- **Referred by:** [Assumption](assumption.md), [Communication Plan](communication-plan.md), [Dependency](dependency.md), [Governance](governance.md), [Issue](issue.md), [Lesson Learned](lesson-learned.md), [Milestone](milestone.md), [Project Understanding](project-understanding.md), [Risk](risk.md), [Verification & Validation](verification-validation.md).

## 6. Lifecycle / status

N/A — identity; attitudes may shift over time.

## 7. Template coverage

- `templates/analysis/viability-study.md` §10 Stakeholder Analysis
- `templates/analysis/business-case.md` §13.1 Stakeholder Register
- `templates/analysis/project-scope.md` §15.1 Scope Approval (sign-off stakeholders)
- `templates/analysis/project-plan.md` §16.1 Stakeholder Register
- `templates/analysis/software-requirements-specification.md` §3.4 Stakeholder Requirements Priorities

## 8. Non-overlap note

Permissions belong to [Role](role.md); engagement belongs to [Communication Plan](communication-plan.md). Stakeholder references both.
