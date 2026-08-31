# Refined Project Concept

> **Slug:** `refined-project-concept` | **Layer:** L1 Intake & Understanding | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the stress-tested, validated project concept produced by idea refinement, with validated key assumptions and explicitly rejected alternatives.
- **Purpose / when used:** produced in Stage 5 of the analysis phase; the pre-investment concept that feeds viability assessment.

## 2. Semantics (crisp)

`refined-project-concept` is the **sharpened concept** that results from divergent/convergent thinking applied to the confirmed [Project Understanding](project-understanding.md). It captures the core value proposition, key assumptions with confidence levels, edge cases and second-order effects, alternative approaches, and the refinement decision. It is **not** the investment case (→ [Option](option.md) / [Cost](cost.md) / [Benefit](benefit.md) in L4), **not** a [Business Model](business-model.md) yet (that formalises value proposition/capture once viability is confirmed), and **not** the original understanding (→ [Project Understanding](project-understanding.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| refinedSummary | string | yes | updated concept statement |
| keyAssumptions | ref[] → [Assumption](assumption.md) | yes | with confidence levels |
| rejectedAlternatives | string[] | yes | with reasons |
| refinedScope | string | yes | refined in/out boundaries |
| edgeCases | string | no | second-order effects |

## 4. State (as-is / target)

Stateless — a pre-investment concept.

## 5. Relationships (semantic references)

- **Refers to:** [Project Understanding](project-understanding.md), [Gap & Contradiction](gap-and-contradiction.md), [Assumption](assumption.md).
- **Referred by:** none.

## 6. Lifecycle / status

N/A — a concept. Refinement may loop back to [Project Understanding](project-understanding.md) when new constraints surface.

## 7. Template coverage

- No template (analysis-phase only). Produced by `skills/analysis/execute-analysis-phase/SKILL.md` Stage 5: Idea Refinement (via the `idea-refine` skill).

## 8. Non-overlap note

Pre-investment. The investment case lives in L4 ([Option](option.md), [Cost](cost.md), [Benefit](benefit.md), [Financial Metric](financial-metric.md)); the formalised value model lives in [Business Model](business-model.md).
