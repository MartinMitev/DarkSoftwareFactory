# Current System

> **Slug:** `current-system` | **Layer:** L4 Investment Decision & Viability | **Applicability:** 🟤🔵

## 1. Identity & definition

- **Definition (one sentence):** the as-is system snapshot — architecture, technology stack, hosting, active users, age, and last major update — for Brown Field and Modernization projects.
- **Purpose / when used:** the starting state that constrains and shapes all subsequent analysis; referenced by the roadmap and transition strategy.

## 2. Semantics (crisp)

`current-system` is the **as-is snapshot** of the existing system (system name, primary business function, architecture style, technology stack, hosting environment, active users, system age, last major update). It is `as-is` **only**. It is **not** the target system (→ [Application](application.md) in target state), **not** a technical-debt item (→ [Technical Debt Item](technical-debt-item.md)), and **not** a risk (→ [Risk](risk.md)). For Green Field, mark NOT APPLICABLE and document any existing manual processes/systems the new software replaces (these are noted via references). Knowledge-concentration risk of the current system is captured as a [Risk](risk.md) (category=Knowledge-Concentration).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| systemName | string | yes | |
| businessFunction | string | yes | |
| architectureStyle | string | yes | monolith / microservices / layered / … |
| technologyStack | ref[] → [Technology](technology.md) | yes | |
| hostingEnvironment | string | yes | on-prem / cloud / hybrid |
| activeUsers | string | yes | count and type |
| systemAge | string | yes | years since initial deployment |
| lastMajorUpdate | string | yes | date |

## 4. State (as-is / target)

As-is only. The target counterpart is [Application](application.md).

## 5. Relationships (semantic references)

- **Refers to:** [Application](application.md), [Interface](interface.md), [Data Entity](data-entity.md), [Technical Debt Item](technical-debt-item.md), [Risk](risk.md) (knowledge concentration).
- **Referred by:** [Legacy Decommission](legacy-decommission.md), [Roadmap](roadmap.md), [SWOT Item](swot-item.md), [Technical Debt Item](technical-debt-item.md).

## 6. Lifecycle / status

N/A — as-is snapshot.

## 7. Template coverage

- `templates/analysis/viability-study.md` §3.1 System Overview, §3.5 Existing System for Green Field Context, Appendix F (Current System Documentation)
- `templates/analysis/project-scope.md` §3.3 Current State Summary
- `templates/analysis/business-case.md` §3.2 Current State Assessment

## 8. Non-overlap note

The target system belongs to [Application](application.md); tracked debt belongs to [Technical Debt Item](technical-debt-item.md); potential harm belongs to [Risk](risk.md).
