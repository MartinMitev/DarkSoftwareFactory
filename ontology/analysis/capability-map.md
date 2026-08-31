# Capability Map

> **Slug:** `capability-map` | **Layer:** L2 Business Architecture | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the set of business capabilities the organization must be able to do, organized into levels, mapped to the business model and to all value streams.
- **Purpose / when used:** the aggregate view of capabilities that links "what we must be able to do" to the value proposition and the value-delivery flow.

## 2. Semantics (crisp)

`capability-map` is the **aggregate** of capabilities — the structured inventory of what the organization must be able to do, with level/level-2 decomposition, and explicit mapping to the [Business Model](business-model.md) and to **every** [Value Stream](value-stream.md). It is **not** a single capability (→ [Capability](capability.md)), **not** a process (how — → [Business Process](business-process.md)), and **not** a requirements list (→ [Requirement](requirement.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| capabilityList | ref[] → [Capability](capability.md) | yes | the capabilities |
| levels | string | yes | level/level-2 decomposition |
| mappingToValueStreams | table | yes | each capability → value stream stage(s) |
| mappingToBusinessModel | table | yes | each capability → value proposition element |

## 4. State (as-is / target)

Stateful. As-is capability map (current abilities and gaps) vs target capability map (required abilities). The delta drives the roadmap.

## 5. Relationships (semantic references)

- **Refers to:** [Business Model](business-model.md), [Value Stream](value-stream.md), [Capability](capability.md).
- **Referred by:** [Capability](capability.md).

## 6. Lifecycle / status

N/A — structural artefact; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/software-requirements-specification.md` §4.1 Functional Requirements Overview (grouping by capability / feature area)
- `templates/analysis/project-scope.md` §5.1 Functional Requirements Overview (capability grouping)
- `templates/analysis/project-scope.md` §4.4 Feature Parity Scope (capability-level parity)

## 8. Non-overlap note

Single-capability detail belongs to [Capability](capability.md); orchestration belongs to [Business Process](business-process.md); system behaviour belongs to [Requirement](requirement.md).
