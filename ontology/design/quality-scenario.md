# Quality Scenario

> **Slug:** `quality-scenario` | **View:** Quality View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a concrete, measurable stimulus-response scenario that operationalises a non-functional [Requirement](../analysis/requirement.md) (quality attribute) — with context, source/stimulus, environment, artifact, response, and response measure — so that fulfillment can be decided.
- **Purpose / when used:** the atomic unit of the quality-requirements view; makes quality goals concrete and testable at design time (SEI ATAM / Q42 scenario form).

## 2. Semantics (crisp)

`quality-scenario` is a **testable quality-attribute scenario**: a quality category (ISO 25010 / Q42 — performance efficiency, compatibility, usability, reliability, security, maintainability, flexibility, safety, plus migration qualities: data integrity, transition availability, feature parity, rollback speed), a context/background, a source/stimulus, an environment, an artifact (the [Component](component.md) / [Crosscutting Concern](crosscutting-concern.md) / [Design Pattern](design-pattern.md) that must respond), the expected response, and a response measure / acceptance criterion. It refines an analysis [Requirement](../analysis/requirement.md) (NFR) — the NFR is the "shall" statement; the scenario is its concrete operationalisation. Its `kind` distinguishes usage scenarios (runtime reaction to a stimulus), change scenarios (effect of a modification/extension), and migration scenarios (data integrity, cutover downtime, feature parity, rollback). It is **not** the NFR statement (→ [Requirement](../analysis/requirement.md)), **not** a story/deliverable pass-fail test (→ [Acceptance Criterion](../analysis/acceptance-criterion.md)), **not** an objective pass/fail (→ [Success Criterion](../analysis/success-criterion.md)), and **not** an ongoing indicator (→ [KPI](../analysis/kpi.md)). The top scenarios are referenced by the design template's Quality Goals (§2.4).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. QS-001 / MQS-001 (migration) |
| kind | enum (usage / change / migration) | yes | |
| qualityCategory | enum (performance-efficiency / compatibility / usability / reliability / security / maintainability / flexibility / safety / data-integrity / transition-availability / feature-parity / rollback) | yes | extendable |
| context | string | yes | system/component + environment |
| source | string | yes | who/what initiates |
| stimulus | string | yes | the action/event |
| environment | string | yes | conditions |
| artifact | ref → [Component](component.md) / [Crosscutting Concern](crosscutting-concern.md) / [Design Pattern](design-pattern.md) | yes | what must respond |
| response | string | yes | expected behaviour |
| responseMeasure | string | yes | metric / acceptance criterion |
| refines | ref → [Requirement](../analysis/requirement.md) | yes | the NFR it operationalises |

## 4. State (as-is / target)

Stateful. As-is scenarios (current quality behaviour, 🟤🔵) vs target scenarios. Migration scenarios exist only during the transition journey.

## 5. Relationships (semantic references)

- **Refers to:** [Requirement](../analysis/requirement.md) (refines), [Component](component.md), [Crosscutting Concern](crosscutting-concern.md), [Design Pattern](design-pattern.md).
- **Referred by:** none.

## 6. Lifecycle / status

N/A — testable scenario; status follows hosting document approval.

## 7. Template coverage

- `templates/design/software-architecture.md` §11.2 Quality Scenarios (usage / change scenarios, short and long SEI form), §11.3 Migration Quality Scenarios 🔵🟤
- `templates/design/software-architecture.md` §2.4 Quality Goals (concrete scenarios + metric/acceptance criteria)

## 8. Non-overlap note

The NFR statement belongs to [Requirement](../analysis/requirement.md); a story/deliverable pass-fail belongs to [Acceptance Criterion](../analysis/acceptance-criterion.md); an objective pass/fail belongs to [Success Criterion](../analysis/success-criterion.md); an ongoing indicator belongs to [KPI](../analysis/kpi.md). Quality-scenario is the design-level stimulus-response operationalisation of an NFR.
