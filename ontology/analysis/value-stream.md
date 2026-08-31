# Value Stream

> **Slug:** `value-stream` | **Layer:** L2 Business Architecture | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the end-to-end delivery of the value proposition to the customer/user, expressed as a sequence of value-adding stages.
- **Purpose / when used:** describes how value flows from trigger to outcome; referenced by the capability map and used as the backbone of the user-story map.

## 2. Semantics (crisp)

`value-stream` is the **coarsest value-delivery flow** — the stages a customer/user passes through to receive value, each with an entry/exit and a value contribution. It is **not** a single orchestrated workflow (→ [Business Process](business-process.md)), **not** a capability (what we must be able to do — → [Capability](capability.md)), and **not** a use case (system interaction — → [Use Case](use-case.md)). A value stream is realized by capabilities and operationalized by business processes.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| stages | string[] | yes | ordered value-adding stages |
| entry | string | yes | trigger of the stream |
| exit | string | yes | value realized |
| valuePerStage | string | yes | contribution of each stage |
| supportsValueProposition | ref → [Business Model](business-model.md) | yes | |

## 4. State (as-is / target)

Stateful. Modernization projects define an as-is value stream (current stages, bottlenecks) and a target value stream (streamlined stages). Green Field defines the target.

## 5. Relationships (semantic references)

- **Refers to:** [Business Model](business-model.md), [Capability](capability.md), [Business Process](business-process.md).
- **Referred by:** [Business Model](business-model.md), [Capability Map](capability-map.md).

## 6. Lifecycle / status

N/A — structural artefact; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/user-stories.md` §2 User Story Map (backbone of user activities)
- `templates/analysis/project-scope.md` §3.4 Target State Vision (value delivery)

## 8. Non-overlap note

Finer-grained workflows belong to [Business Process](business-process.md); the abilities needed belong to [Capability](capability.md).
