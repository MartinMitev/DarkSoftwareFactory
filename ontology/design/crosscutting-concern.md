# Crosscutting Concern

> **Slug:** `crosscutting-concern` | **View:** Concepts View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a system-wide architectural policy or concept — security, observability, error handling & resilience, data access & persistence, integration & communication, testing, or migration-specific concepts (data sync, feature flags, dual-running monitoring, cutover, rollback) — applied consistently across multiple [Component](component.md)s and [Interface](../analysis/interface.md)s.
- **Purpose / when used:** the atomic unit of the cross-cutting concepts view; ensures conceptual integrity (consistency, homogeneity) of the architecture.

## 2. Semantics (crisp)

`crosscutting-concern` is a **system-wide architectural policy** applied across multiple building blocks: what the concept is, why it is architecturally important, how it is implemented consistently, the [Design Pattern](design-pattern.md)s and tooling/frameworks used to enforce it, and which [Component](component.md)s / [Interface](../analysis/interface.md)s it applies to. It realises analysis [Requirement](../analysis/requirement.md)s (especially NFRs — e.g. a security concept realises security NFRs) and satisfies analysis [Compliance Requirement](../analysis/compliance-requirement.md)s (e.g. a data-protection concept satisfies a GDPR obligation). It is **not** a tactical pattern (→ [Design Pattern](design-pattern.md) — a concern may *mandate* patterns but is the policy, not the solution), **not** a regulatory obligation (→ [Compliance Requirement](../analysis/compliance-requirement.md) — the concern *satisfies* the obligation), **not** a single component (→ [Component](component.md)), **not** a single interface (→ [Interface](../analysis/interface.md)), and **not** an NFR statement (→ [Requirement](../analysis/requirement.md)). Migration-specific concerns (data synchronization, feature-flag management, dual-running monitoring, cutover, rollback) carry a `migrationFacet` with a transition duration and a decommission trigger.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. CCC-001 |
| name | enum (security / observability / error-handling-resilience / data-access-persistence / integration-communication / testing / migration-sync / feature-flag / dual-running-monitoring / cutover / rollback) | yes | extendable |
| description | string | yes | what it is and why architecturally important |
| consistencyMechanism | string | yes | how implemented consistently across the system |
| mandatesPatterns | ref[] → [Design Pattern](design-pattern.md) | no | patterns enforcing the concept |
| toolingFrameworks | string | no | tools/frameworks enforcing the concept |
| appliesToComponents | ref[] → [Component](component.md) | yes | |
| appliesToInterfaces | ref[] → [Interface](../analysis/interface.md) | no | |
| realises | ref[] → [Requirement](../analysis/requirement.md) | yes | NFRs/FRs this concept realises |
| satisfies | ref[] → [Compliance Requirement](../analysis/compliance-requirement.md) | no | regulatory obligations satisfied |
| migrationFacet | bool | no | 🔵🟤 true for migration-specific concepts |
| transitionDuration | string | no | 🔵🟤 required when migrationFacet=true |
| decommissionTrigger | string | no | 🔵🟤 required when migrationFacet=true |

## 4. State (as-is / target)

Stateful. As-is concerns (existing policies, 🟤🔵 — must be consistent between legacy and new during transition) vs target concerns. Migration concerns exist only during the transition journey.

## 5. Relationships (semantic references)

- **Refers to:** [Component](component.md), [Interface](../analysis/interface.md), [Design Pattern](design-pattern.md), [Requirement](../analysis/requirement.md), [Compliance Requirement](../analysis/compliance-requirement.md).
- **Referred by:** [Component](component.md), [Quality Scenario](quality-scenario.md).

## 6. Lifecycle / status

N/A — architectural policy; status follows hosting document approval.

## 7. Template coverage

- `templates/design/software-architecture.md` §9 Cross-cutting Concepts (§9.1–9.6 general concepts: security, observability, error handling, data access, integration, testing; §9.7 Migration-Specific Concepts 🔵🟤)

## 8. Non-overlap note

A tactical pattern belongs to [Design Pattern](design-pattern.md); a regulatory obligation belongs to [Compliance Requirement](../analysis/compliance-requirement.md); an NFR statement belongs to [Requirement](../analysis/requirement.md); a single building block belongs to [Component](component.md); a single contract belongs to [Interface](../analysis/interface.md).
