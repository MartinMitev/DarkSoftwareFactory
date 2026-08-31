# Business Model

> **Slug:** `business-model` | **Layer:** L2 Business Architecture | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the "why" of the initiative — the problem or opportunity, the value proposition, how value is captured, and the strategic alignment.
- **Purpose / when used:** the foundational business artefact that explains why the initiative exists and how it creates and captures value; referenced by the capability map, value streams, and objectives.

## 2. Semantics (crisp)

`business-model` (aka Business Concept) captures the problem/opportunity, the value proposition, the value-capture mechanism, strategic alignment, the affected parties, and the urgency. It is **not** the market sizing or competitive landscape (→ [Market & Demand](market-and-demand.md)), **not** what the organization must be able to do (→ [Capability](capability.md)), and **not** the end-to-end value delivery flow (→ [Value Stream](value-stream.md)). It answers "why and what value", leaving "what we must be able to do" to capabilities.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| problem | string | yes | the pain point / opportunity |
| valueProposition | string | yes | unique value delivered |
| valueCapture | string | yes | how value is monetised/realised |
| strategicAlignment | string | yes | link to organisational objectives |
| affectedParties | string | yes | customers/employees/partners |
| urgency | string | yes | "why now" + cost of inaction |

## 4. State (as-is / target)

Stateful. Brown Field / Modernization projects define an as-is business model (current value proposition and gaps) and a target business model (improved proposition). Green Field defines a target model only.

## 5. Relationships (semantic references)

- **Refers to:** [Objective](objective.md), [Market & Demand](market-and-demand.md), [Value Stream](value-stream.md).
- **Referred by:** [Capability Map](capability-map.md), [Market & Demand](market-and-demand.md), [Objective](objective.md), [Value Stream](value-stream.md).

## 6. Lifecycle / status

N/A — stateless concept; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/viability-study.md` §4.1 Problem Statement & Value Proposition
- `templates/analysis/business-case.md` §3.1 Problem Statement, §3.3 Strategic Alignment, §7 Benefits & Value Proposition

## 8. Non-overlap note

Market, competitors, and demand evidence belong to [Market & Demand](market-and-demand.md). What the organization must be able to do belongs to [Capability](capability.md).
