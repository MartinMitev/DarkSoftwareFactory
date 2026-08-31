# Capability

> **Slug:** `capability` | **Layer:** L2 Business Architecture | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a single business ability described in detail — what the organization must be able to do.
- **Purpose / when used:** the atomic unit of the [Capability Map](capability-map.md); a stable, organization-level ability realized by processes, supported by applications, and elaborated by requirements.

## 2. Semantics (crisp)

`capability` is a **business ability** (stable, organization-level), e.g. "Order Management", "Customer Onboarding". It states what we can do and its outcomes/hotspots. It is **not** how the capability is executed (→ [Business Process](business-process.md)), **not** a system function (→ [Requirement](requirement.md)), and **not** a system that supports it (→ [Application](application.md)). Capabilities are realized by requirements and operationalized by processes.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| name | string | yes | |
| description | string | yes | |
| level | int | yes | level 1 / 2 in the map |
| owner | ref → [Stakeholder](stakeholder.md) | yes | accountable for the capability |
| outcomes | string | yes | what it produces |
| hotspots | string | no | known weaknesses / gaps |

## 4. State (as-is / target)

Stateful. As-is capability (current ability, gaps) vs target capability (required ability). Brown Field marks changes to existing capabilities.

## 5. Relationships (semantic references)

- **Refers to:** [Capability Map](capability-map.md), [Business Process](business-process.md), [Application](application.md), [Requirement](requirement.md).
- **Referred by:** [Application](application.md), [Business Process](business-process.md), [Capability Map](capability-map.md), [Epic](epic.md), [Requirement](requirement.md), [Roadmap](roadmap.md), [Value Stream](value-stream.md).

## 6. Lifecycle / status

N/A — structural artefact; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/software-requirements-specification.md` §4.1, §4.2 (feature area / business capability grouping)
- `templates/analysis/project-scope.md` §5.1 Functional Requirements Overview (capability grouping)
- `templates/analysis/user-stories.md` §3 Epics (an epic delivers a capability)

## 8. Non-overlap note

Realisation (system behaviour) belongs to [Requirement](requirement.md); orchestration belongs to [Business Process](business-process.md); the supporting system belongs to [Application](application.md).
