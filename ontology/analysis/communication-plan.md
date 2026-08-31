# Communication Plan

> **Slug:** `communication-plan` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** how stakeholders are informed and engaged — stakeholder group, channel, frequency, key messages, owner, feedback — plus the reporting schedule and escalation protocol.
- **Purpose / when used:** the single communication artefact across business case, scope, and project plan.

## 2. Semantics (crisp)

`communication-plan` is the **stakeholder engagement mechanism**: per stakeholder group, a channel, frequency, key messages, owner, and feedback mechanism — plus a reporting schedule (sprint report, monthly status, steering committee deck, gate report, release notes) and an escalation protocol (levels, triggers, response times). It is **not** the stakeholder identity (→ [Stakeholder](stakeholder.md)) and **not** the governance framework (→ [Governance](governance.md)) — it references both.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| stakeholderGroup | ref → [Stakeholder](stakeholder.md) | yes | |
| channel | string | yes | meeting / newsletter / dashboard |
| frequency | string | yes | |
| keyMessages | string | yes | |
| owner | ref → [Stakeholder](stakeholder.md) | yes | |
| feedbackMechanism | string | yes | |
| reportingSchedule | table | yes | report type / frequency / audience |
| escalationProtocol | table | yes | level / trigger / response time |

## 4. State (as-is / target)

Stateless — an engagement plan.

## 5. Relationships (semantic references)

- **Refers to:** [Stakeholder](stakeholder.md), [Governance](governance.md).
- **Referred by:** [Stakeholder](stakeholder.md).

## 6. Lifecycle / status

N/A — plan; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/business-case.md` §13.2 Communication Plan
- `templates/analysis/project-plan.md` §11 Communication Management (§11.1 plan, §11.2 reporting, §11.3 escalation)
- `templates/analysis/project-scope.md` §15.2 Scope Communication
- `templates/analysis/software-requirements-specification.md` §16.2 Requirements Communication

## 8. Non-overlap note

The stakeholder identity belongs to [Stakeholder](stakeholder.md); the decision framework belongs to [Governance](governance.md). Communication Plan owns the engagement mechanism.
