# Application

> **Slug:** `application` | **Layer:** L2 Business Architecture | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a business application (system) that supports capabilities, processes, and roles, with boundaries and technologies.
- **Purpose / when used:** the system under analysis or a related system; references the capabilities it supports, the processes it participates in, and the technologies it uses.

## 2. Semantics (crisp)

`application` is the **system** — the software under analysis or a related/adjacent system. It defines its purpose, boundaries (what is inside vs external), the capabilities and processes it supports, the roles it serves, and its technologies. It is **not** an interface contract (→ [Interface](interface.md)), **not** a technology choice (→ [Technology](technology.md)), and **not** the as-is legacy snapshot (→ [Current System](current-system.md)). For Modernization, the target application replaces the [Current System](current-system.md).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| name | string | yes | |
| purpose | string | yes | business function |
| boundaries | string | yes | inside vs external |
| supportsCapabilities | ref[] → [Capability](capability.md) | yes | |
| supportsProcesses | ref[] → [Business Process](business-process.md) | yes | |
| servesRoles | ref[] → [Role](role.md) | yes | |
| technologies | ref[] → [Technology](technology.md) | yes | |

## 4. State (as-is / target)

Stateful. As-is application (current system) vs target application (new/enhanced system). The as-is snapshot is also captured as [Current System](current-system.md).

## 5. Relationships (semantic references)

- **Refers to:** [Capability](capability.md), [Business Process](business-process.md), [Role](role.md), [Interface](interface.md), [Technology](technology.md).
- **Referred by:** [Business Process](business-process.md), [Capability](capability.md), [Current System](current-system.md), [Interface](interface.md), [Technology](technology.md).

## 6. Lifecycle / status

N/A — definition; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/software-requirements-specification.md` §7 System Boundaries & Interfaces (system context)
- `templates/analysis/project-plan.md` Appendix E Architecture & Technical Context
- `templates/analysis/viability-study.md` §3.1 System Overview (existing system)

## 8. Non-overlap note

Technology choices belong to [Technology](technology.md); interface contracts belong to [Interface](interface.md); the legacy as-is snapshot belongs to [Current System](current-system.md).
