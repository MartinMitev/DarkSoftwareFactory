# Execution Flow

> **Slug:** `execution-flow` | **View:** Runtime View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a runtime scenario describing the dynamic sequence of interactions between [Component](component.md) instances — trigger, ordered steps, data exchanged, and error/rollback handling — for a use case, operation, error, or migration situation.
- **Purpose / when used:** the atomic unit of the runtime view; models dynamic behaviour and control flow at design time, complementing the static [Component](component.md) decomposition.

## 2. Semantics (crisp)

`execution-flow` is a **runtime scenario**: what triggers it (user action, external event, scheduled job, system start-up), the ordered steps of interaction between participating [Component](component.md) instances, the [Data Entity](../analysis/data-entity.md) / payload exchanged at each step, and the error handling or rollback at each step. Its `scenarioType` distinguishes use-case scenarios, operation/administration scenarios (launch, start-up, stop), error/exception scenarios, and migration runtime scenarios (requests routing through legacy + new components during transition, with a `rollbackOnFailure` per step). It participates at [Interface](../analysis/interface.md) boundaries and operationalises an analysis [Use Case](../analysis/use-case.md) / [Requirement](../analysis/requirement.md). It is **not** the static structure (→ [Component](component.md)), **not** the interface contract (→ [Interface](../analysis/interface.md)), **not** the data model (→ [Data Entity](../analysis/data-entity.md)), and **not** the use case itself (→ [Use Case](../analysis/use-case.md)). It may be expressed as numbered steps, sequence/activity/state diagrams, BPMN, or flow charts.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. EF-001 |
| name | string | yes | scenario name |
| scenarioType | enum (use-case / operation / error / migration) | yes | |
| trigger | string | yes | user action / event / scheduled job / start-up |
| participants | ref[] → [Component](component.md) | yes | building blocks involved |
| steps | table (step / buildingBlock / action / dataExchanged / errorHandling) | yes | ordered |
| usesInterfaces | ref[] → [Interface](../analysis/interface.md) | no | boundaries exercised |
| exchangesData | ref[] → [Data Entity](../analysis/data-entity.md) | no | payloads |
| realisesUseCase | ref → [Use Case](../analysis/use-case.md) | no | for use-case scenarios |
| realisesRequirement | ref[] → [Requirement](../analysis/requirement.md) | no | |
| rollbackOnFailure | table (step / rollbackAction) | no | 🔵🟤 for migration scenarios |
| performanceConsiderations | string | no | expected response time / throughput |

## 4. State (as-is / target)

Stateful. As-is flows (current runtime behaviour, 🟤🔵) vs target flows. Migration flows exist only during the transition journey.

## 5. Relationships (semantic references)

- **Refers to:** [Component](component.md), [Interface](../analysis/interface.md), [Data Entity](../analysis/data-entity.md), [Use Case](../analysis/use-case.md), [Requirement](../analysis/requirement.md).
- **Referred by:** none.

## 6. Lifecycle / status

Status: Draft → Reviewed → Approved. Changes via [Change Request](../analysis/change-request.md).

## 7. Template coverage

- `templates/design/software-architecture.md` §7 Runtime View (§7.1/7.2 Runtime Scenarios, §7.3 Migration Runtime Scenario 🔵🟤, §7.4 Error and Exception Scenarios)

## 8. Non-overlap note

Static structure belongs to [Component](component.md); the interface contract belongs to [Interface](../analysis/interface.md); the data model belongs to [Data Entity](../analysis/data-entity.md); the use case (analysis-level "what") belongs to [Use Case](../analysis/use-case.md) — execution-flow is the design-level "how it runs".
