# Component

> **Slug:** `component` | **View:** Building Block View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a modular software building block — module, microservice, package, subsystem, layer, class, library, or framework — with a single responsibility, exposed/consumed interfaces, quality/performance characteristics, and a hierarchical level.
- **Purpose / when used:** the atomic unit of the static decomposition of the system; the design-phase counterpart of the analysis [Application](../analysis/application.md) (a component is *part of* an application). Hierarchical whitebox levels 1 → 2 → 3 zoom into contained building blocks.

## 2. Semantics (crisp)

`component` is a **building block** in the static decomposition of an [Application](../analysis/application.md). It owns a single responsibility, exposes and consumes [Interface](../analysis/interface.md)s (internal boundaries) and may persist/query [Data Entity](../analysis/data-entity.md) instances. It carries a `kind` (module / microservice / package / subsystem / layer / class / library / framework), a `level` (1 top-level whitebox, 2 / 3 deeper whiteboxes), quality/performance characteristics, and a directory/location. It implements [Design Pattern](design-pattern.md)s, is constrained by [Crosscutting Concern](crosscutting-concern.md)s, is mapped to infrastructure by [Deployment Node](deployment-node.md)s, realises analysis [Requirement](../analysis/requirement.md)s (especially NFRs), and is built with analysis [Technology](../analysis/technology.md). It is **not** the whole system (→ [Application](../analysis/application.md)), **not** the interface contract (→ [Interface](../analysis/interface.md)), **not** the technology choice (→ [Technology](../analysis/technology.md)), **not** the runtime behaviour (→ [Execution Flow](execution-flow.md)), and **not** the physical host (→ [Infrastructure Resource](infrastructure-resource.md)). For Brown Field / Modernization, as-is instances are existing building blocks of the [Current System](../analysis/current-system.md); transition instances (sync services, routing gateways, feature-flag services) carry a `transition` facet with a lifetime and a decommission trigger.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. C-001 |
| name | string | yes | |
| kind | enum (module / microservice / package / subsystem / layer / class / library / framework) | yes | |
| level | int (1 / 2 / 3) | yes | whitebox hierarchy |
| parentComponent | ref → [Component](component.md) | no | parent whitebox block (containment hierarchy) |
| contains | ref[] → [Component](component.md) | no | contained whitebox sub-blocks (hierarchical decomposition) |
| responsibility | string | yes | single responsibility |
| exposes | ref[] → [Interface](../analysis/interface.md) | yes | internal + external boundaries |
| consumes | ref[] → [Interface](../analysis/interface.md) | yes | |
| persistsQueries | ref[] → [Data Entity](../analysis/data-entity.md) | no | data ownership / access flows |
| implementsPatterns | ref[] → [Design Pattern](design-pattern.md) | no | |
| subjectTo | ref[] → [Crosscutting Concern](crosscutting-concern.md) | no | enforced policies |
| realises | ref[] → [Requirement](../analysis/requirement.md) | no | NFRs / FRs the block satisfies |
| builtWith | ref[] → [Technology](../analysis/technology.md) | yes | |
| qualityPerformance | string | yes | perf / quality characteristics |
| directoryLocation | string | no | source location |
| changeType | enum (new / modified / preserved / retired) | no | 🟤🔵 |
| transition | bool | no | 🟤🔵 true = temporary transition building block |
| lifetime | string | no | 🟤🔵 required when transition=true |
| decommissionTrigger | string | no | 🟤🔵 required when transition=true |
| justifiedBy | ref → [Decision](../analysis/decision.md) | no | the ADR justifying this block |

## 4. State (as-is / target)

Stateful. As-is components (existing building blocks, 🟤🔵 — counterpart of [Current System](../analysis/current-system.md)) vs target components (new/enhanced). Attribute-level change type for Brown Field / Modernization. Transition components exist only during the journey.

## 5. Relationships (semantic references)

- **Refers to:** [Application](../analysis/application.md) (part of), [Interface](../analysis/interface.md), [Data Entity](../analysis/data-entity.md), [Design Pattern](design-pattern.md), [Crosscutting Concern](crosscutting-concern.md), [Requirement](../analysis/requirement.md), [Technology](../analysis/technology.md), [Current System](../analysis/current-system.md) (as-is counterpart, 🟤🔵), [Decision](../analysis/decision.md) (justified by), [Component](component.md) (parentComponent / contains — whitebox hierarchy).
- **Referred by:** [Component](component.md) (parentComponent / contains), [Execution Flow](execution-flow.md), [Design Pattern](design-pattern.md), [Deployment Node](deployment-node.md), [Crosscutting Concern](crosscutting-concern.md), [Quality Scenario](quality-scenario.md), [Decision](../analysis/decision.md), maintenance [Ticket](../maintenance/ticket.md), maintenance [Maintenance Log](../maintenance/maintenance-log.md).

## 6. Lifecycle / status

Status: Draft → Reviewed → Approved. Changes via [Change Request](../analysis/change-request.md). Transition components are removed once their decommission trigger fires.

## 7. Template coverage

- `templates/design/software-architecture.md` §6 Building Block View (§6.1 Whitebox Overall System, §6.2 Level 2, §6.3 Level 3 Deep Dive, §6.4 Existing System Structure 🟤🔵, §6.5 Transition Building Blocks 🔵)
- `templates/design/software-architecture.md` §5.2 Top-Level Decomposition (level-1 components)
- `templates/design/software-architecture.md` §1 Executive Summary (key decomposition)

## 8. Non-overlap note

The whole system belongs to analysis [Application](../analysis/application.md); the interface contract belongs to [Interface](../analysis/interface.md); the technology choice belongs to [Technology](../analysis/technology.md); runtime behaviour belongs to [Execution Flow](execution-flow.md); the physical host belongs to [Infrastructure Resource](infrastructure-resource.md); the static mapping to a host belongs to [Deployment Node](deployment-node.md).
