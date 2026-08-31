# Technology

> **Slug:** `technology` | **Layer:** L4 Investment Decision & Viability | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a technology or component choice evaluated for feasibility — purpose, maturity, license, lock-in risk, and alternative.
- **Purpose / when used:** the atomic unit of technology-stack evaluation and target architecture decisions; used by applications and interfaces.

## 2. Semantics (crisp)

`technology` is a **technology/component under evaluation or selected** (language, framework, library, runtime, platform) with maturity (proven/emerging/experimental), license/cost model, lock-in risk, and an alternative. It is **not** the application that uses it (→ [Application](application.md)), **not** the interface contract (→ [Interface](interface.md)), and **not** an option (investment alternative — → [Option](option.md)). It is referenced by [Application](application.md) and [Interface](interface.md) and evaluated by the viability study.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| name | string | yes | |
| purpose | string | yes | |
| maturity | enum (proven / emerging / experimental) | yes | |
| license | string | yes | open-source / commercial / usage-based |
| lockInRisk | string | yes | |
| alternative | string | yes | |

## 4. State (as-is / target)

Stateful. As-is technologies (current stack) vs target technologies (selected stack).

## 5. Relationships (semantic references)

- **Refers to:** [Application](application.md), [Interface](interface.md), [Option](option.md).
- **Referred by:** [Application](application.md), [Interface](interface.md), [Option](option.md), [Proof of Concept](proof-of-concept.md).

## 6. Lifecycle / status

N/A — evaluation artefact; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/viability-study.md` §5.1 Architecture & Platform Strategy, §5.2 Technology Stack Evaluation
- `templates/analysis/project-plan.md` Appendix E Architecture & Technical Context, §12.4 Technology & Infrastructure Resources
- `templates/analysis/project-scope.md` §4.5 Technical Enablers (enabler technologies)

## 8. Non-overlap note

The system using the technology belongs to [Application](application.md); the contract belongs to [Interface](interface.md); the investment alternative belongs to [Option](option.md).
