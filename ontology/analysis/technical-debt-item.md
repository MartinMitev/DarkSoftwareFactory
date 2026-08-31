# Technical Debt Item

> **Slug:** `technical-debt-item` | **Layer:** L4 Investment Decision & Viability | **Applicability:** 🟤🔵

## 1. Identity & definition

- **Definition (one sentence):** a categorized technical-debt item — of the current system or newly created by the target design/migration — with category, severity, business impact, origin, remediation plan, and target date.
- **Purpose / when used:** quantifies and prioritizes debt that affects modernization and design decisions; used in analysis (current-system debt) and design (debt carried forward or introduced by the architecture).

## 2. Semantics (crisp)

`technical-debt-item` is a **tracked debt entry** — of the [Current System](current-system.md) (as-is) or newly created by the target architecture/migration (target) — categorised (deliberate speed-shortcut, accidental poor-practice, bit-rot environment drift, dependency debt), with an `origin` (deliberate / inadvertent / legacy), severity (Critical/Significant/Manageable), business impact (velocity, defect rate, onboarding), remediation effort, a `remediationPlan`, a `priority`, and a `targetDate`. It is **not** a generic risk (a potential future harm — → [Risk](risk.md)) and **not** the current system snapshot (→ [Current System](current-system.md)). It feeds the modernization business case (cost of carrying debt vs cost of remediation) and the design-phase risks-and-debts section.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| item | string | yes | debt description |
| category | enum (deliberate / accidental / bit-rot / dependency) | yes | |
| origin | enum (deliberate / inadvertent / legacy) | yes | deliberate shortcut / inadvertent poor-practice / legacy carried forward |
| severity | enum (Critical / Significant / Manageable) | yes | |
| businessImpact | string | yes | velocity / defect rate / onboarding |
| remediationEffort | string | yes | |
| remediationPlan | string | no | how the debt will be paid down |
| priority | enum (Must / Should / Could) | no | |
| targetDate | date | no | remediation target | |

## 4. State (as-is / target)

Stateful. As-is items are debt of the current system; target items are debt newly created or carried forward by the target architecture/migration. Change type marks new/modified/preserved/retired.

## 5. Relationships (semantic references)

- **Refers to:** [Current System](current-system.md).
- **Referred by:** [Current System](current-system.md).

## 6. Lifecycle / status

N/A — inventory; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/viability-study.md` §3.3 Technical Debt Assessment
- `templates/design/software-architecture.md` §12.2 Technical Debts, §12.3 Legacy System Risks and Debts

## 8. Non-overlap note

Potential future harm belongs to [Risk](risk.md); the system snapshot belongs to [Current System](current-system.md).
