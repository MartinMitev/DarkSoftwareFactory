# Gap & Contradiction

> **Slug:** `gap-and-contradiction` | **Layer:** L1 Intake & Understanding | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a register of missing information (gaps) and conflicting information (contradictions) discovered in the source material, with dimension/sources, severity, and resolution.
- **Purpose / when used:** produced in Stage 3 of the analysis phase to identify every information gap and contradiction before they propagate into downstream deliverables.

## 2. Semantics (crisp)

`gap-and-contradiction` is the **defect register of the source material itself**. A *gap* is a missing piece of information across dimensions (problem/goals, users, scope, constraints, dependencies, risks/NFRs, existing system); a *contradiction* is disagreement between sources. It is **not** a [Risk](risk.md) (a potential future harm), **not** an [Assumption](assumption.md) (a stated belief taken as true), and **not** an [Issue](issue.md) (an occurred problem). Critical gaps feed assumptions or interview questions; contradictions are resolved into [Decision](decision.md) records (which source takes precedence).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| kind | enum (gap / contradiction) | yes | |
| dimensionOrSources | string | yes | gap: dimension; contradiction: the disagreeing sources |
| description | string | yes | |
| severity | enum (Critical / Important / Optional) | yes | |
| resolution | string | no | resolved / partially resolved / deferred assumption |
| status | enum (open / resolved / deferred) | yes | |

## 4. State (as-is / target)

Stateless — a register of source-material defects.

## 5. Relationships (semantic references)

- **Refers to:** [Project Understanding](project-understanding.md), [Documentation Inventory](documentation-inventory.md), [Assumption](assumption.md), [Risk](risk.md), [Decision](decision.md).
- **Referred by:** [Assumption](assumption.md), [Refined Project Concept](refined-project-concept.md).

## 6. Lifecycle / status

Status transitions: open → resolved / deferred. Critical gaps must reach a resolution path (interview or deferred assumption with user acknowledgment) before the analysis phase proceeds.

## 7. Template coverage

- No template (analysis-phase only). Produced by `skills/analysis/execute-analysis-phase/SKILL.md` Stage 3: Gap & Contradiction Analysis.

## 8. Non-overlap note

Distinct from [Risk](risk.md) (future harm), [Assumption](assumption.md) (a stated belief), and [Issue](issue.md) (an occurred problem). A gap *may become* an assumption when deferred.
