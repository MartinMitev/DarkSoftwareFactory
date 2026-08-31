# Vendor

> **Slug:** `vendor` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** an external supplier — service/product, criticality, lock-in risk, SLA, contract type, and exit strategy.
- **Purpose / when used:** the supplier relationship artefact; referenced by interfaces, costs, and the legacy-decommission plan.

## 2. Semantics (crisp)

`vendor` is an **external supplier relationship**: a vendor name, the service/product provided, criticality, lock-in risk, SLA, contract type (fixed-price / T&M), a single point of contact, and an exit strategy. It is **not** the interface contract (→ [Interface](interface.md)) and **not** a cost (→ [Cost](cost.md)) — it references both. For Modernization, the legacy vendor's support-contract status and exit strategy feed the [Legacy Decommission](legacy-decommission.md) plan.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| name | string | yes | |
| serviceProduct | string | yes | |
| criticality | enum (critical / important / nice-to-have) | yes | |
| lockInRisk | string | yes | |
| sla | string | yes | |
| contractType | string | yes | fixed-price / T&M |
| exitStrategy | string | yes | 🟤🔵 |
| spoc | string | yes | single point of contact |

## 4. State (as-is / target)

Stateless — a supplier relationship.

## 5. Relationships (semantic references)

- **Refers to:** [Interface](interface.md), [Cost](cost.md), [Risk](risk.md), [Legacy Decommission](legacy-decommission.md).
- **Referred by:** [Legacy Decommission](legacy-decommission.md).

## 6. Lifecycle / status

N/A — relationship; contract status tracked over time.

## 7. Template coverage

- `templates/analysis/viability-study.md` §6.4 Contractual Obligations, §8.5 Vendor & Supply Chain Dependencies
- `templates/analysis/project-plan.md` §13 Procurement & Vendor Management (§13.1, §13.2, §13.3)

## 8. Non-overlap note

The interface contract belongs to [Interface](interface.md); the cost belongs to [Cost](cost.md). Vendor owns the supplier relationship.
