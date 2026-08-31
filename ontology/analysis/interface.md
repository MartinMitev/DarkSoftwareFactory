# Interface

> **Slug:** `interface` | **Layer:** L3 Requirements | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** an interface or integration point — external or internal between components — API, messaging/event, file exchange, UI, or hardware — with direction, protocol, version, security, criticality, and backward-compatibility.
- **Purpose / when used:** the consolidated artefact for every boundary of the system (external integration boundaries and internal component-to-component boundaries); "integration" is an aspect of this artefact, not a separate one. Used in analysis (external interfaces) and design (building-block interfaces, technical context channels).

## 2. Semantics (crisp)

`interface` is the **single artefact** for every boundary of the system: external APIs/integrations (expose/consume), messaging/events (publish/subscribe), file exchanges, user interfaces, hardware/device interfaces, **and internal component-to-component interfaces** (a component exposes/consumes an interface — the design-phase [Component](../design/component.md) links here). It carries direction (inbound/outbound/bidirectional), protocol/format, version, security mechanism (authentication, encryption, mTLS), specification location, criticality, and (for Brown Field / Modernization) backward compatibility and a change type (new/modified/preserved/retired). The term "integration" is a **synonym/aspect** of `interface` — there is no separate integration artefact. It is **not** the data payload structure (→ [Data Entity](data-entity.md)), **not** the technology choice (→ [Technology](technology.md)), and **not** the application/component itself (→ [Application](application.md) / design [Component](../design/component.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. IR-001 |
| name | string | yes | |
| type | enum (api / messaging / file / ui / hardware) | yes | |
| direction | enum (inbound / outbound / bidirectional) | yes | |
| protocol | string | yes | REST / gRPC / Kafka / SFTP / … |
| format | string | yes | JSON / XML / Avro / … |
| version | string | yes | contract version, e.g. v1, v2 |
| securityMechanism | string | no | auth / encryption / mTLS — design §4.2 technical context |
| specificationLocation | string | no | link to OpenAPI/AsyncAPI spec |
| criticality | enum (critical / important / nice-to-have) | yes | |
| backwardCompatibility | string | no | 🟤🔵 |
| changeType | enum (new / modified / preserved / retired) | no | 🟤🔵 |
| consumerProvider | string | yes | who consumes / who provides |

## 4. State (as-is / target)

Stateful. As-is interfaces (current contracts) vs target interfaces. Backward compatibility constraints for Brown Field / Modernization. Internal component-to-component interfaces are target-state by default (Green Field) or modified/preserved (Brown Field / Modernization).

## 5. Relationships (semantic references)

- **Refers to:** [Requirement](requirement.md), [Data Entity](data-entity.md), [Application](application.md), [Technology](technology.md).
- **Referred by:** [Application](application.md), [Current System](current-system.md), [Data Entity](data-entity.md), [Data Migration](data-migration.md), [Requirement](requirement.md), [Technology](technology.md), [Use Case](use-case.md), [Vendor](vendor.md), and (design phase) [Component](../design/component.md), [Execution Flow](../design/execution-flow.md), [Crosscutting Concern](../design/crosscutting-concern.md).

## 6. Lifecycle / status

Status: Draft → Reviewed → Approved. Changes via [Change Request](change-request.md).

## 7. Template coverage

- `templates/analysis/software-requirements-specification.md` §8 Interface Requirements (incl. §8.2 API, §8.3 messaging, §8.4 file, §8.5 UI, §8.6 hardware)
- `templates/analysis/project-scope.md` §7 System Boundaries & Interfaces (incl. §7.2 integrations, §7.3 API contracts, §7.4 migration integration)
- `templates/analysis/viability-study.md` §5.5 Integration & Interoperability
- `templates/analysis/software-requirements-specification.md` Appendix D (API Spec), Appendix E (Message & Event Schema)
- `templates/design/software-architecture.md` §4.2 Technical Context (channels, protocols, security), §4.3 External Interface Specifications, §6.1/6.2 Important Interfaces (internal component interfaces)

## 8. Non-overlap note

Integration is folded here — no separate integration artefact. Data payload structure belongs to [Data Entity](data-entity.md); technology choice belongs to [Technology](technology.md).
