# Business Process

> **Slug:** `business-process` | **Layer:** L2 Business Architecture | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** an orchestrated workflow of activities that executes one or more capabilities, with triggers, inputs, outputs, and business rules.
- **Purpose / when used:** describes how capabilities are operationalized end-to-end across roles and applications.

## 2. Semantics (crisp)

`business-process` is the **how** — a sequence of activities (with triggers, inputs, outputs, and governing business rules) that operationalises one or more [Capability](capability.md) artefacts, coordinated across [Role](role.md) artefacts and supported by [Application](application.md) artefacts. It is **not** the value stream (coarser — → [Value Stream](value-stream.md)), **not** a use case (actor↔system interaction — → [Use Case](use-case.md)), and **not** a capability (what — → [Capability](capability.md)). Coordination of people across a process is captured by [RACI Assignment](raci-assignment.md).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| processSteps | string[] | yes | ordered activities |
| triggers | string | yes | what starts the process |
| inputs | string | yes | |
| outputs | string | yes | |
| businessRules | ref[] → [Business Rule](business-rule.md) | yes | rules governing the process |
| realizes | ref[] → [Capability](capability.md) | yes | which capabilities it executes |
| participants | ref[] → [Role](role.md) | yes | roles involved |

## 4. State (as-is / target)

Stateful. As-is process (current workflow) vs target process (improved workflow). Migration projects specify preserved/modified/new processes.

## 5. Relationships (semantic references)

- **Refers to:** [Capability](capability.md), [Role](role.md), [Application](application.md), [Business Rule](business-rule.md).
- **Referred by:** [Application](application.md), [Business Rule](business-rule.md), [Capability](capability.md), [RACI Assignment](raci-assignment.md), [Requirement](requirement.md), [Role](role.md), [Value Stream](value-stream.md).

## 6. Lifecycle / status

N/A — structural artefact; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/software-requirements-specification.md` §4.4 State & Workflow Requirements
- `templates/analysis/project-scope.md` §5.3 Business Rules & Logic (process-level rules)
- `templates/analysis/business-case.md` §11.3 Change Management Plan (process impact)

## 8. Non-overlap note

Actor↔system interaction belongs to [Use Case](use-case.md); people coordination belongs to [RACI Assignment](raci-assignment.md); the ability belongs to [Capability](capability.md).
