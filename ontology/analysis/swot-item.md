# SWOT Item

> **Slug:** `swot-item` | **Layer:** L4 Investment Decision & Viability | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a strength, weakness, opportunity, or threat with a source — a synthesis entry for the SWOT view.
- **Purpose / when used:** provides the structured SWOT synthesis for the viability study.

## 2. Semantics (crisp)

`swot-item` is a **single SWOT entry** (strength/weakness = internal; opportunity/threat = external) with a source. It is a *synthesis view* — it **references, it does not redefine**, the underlying [Risk](risk.md), [Benefit](benefit.md), [Market & Demand](market-and-demand.md), and [Current System](current-system.md) artefacts. It is **not** a risk (→ [Risk](risk.md)), **not** a benefit (→ [Benefit](benefit.md)), and **not** a market fact (→ [Market & Demand](market-and-demand.md)); it only re-frames them for the SWOT lens.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| kind | enum (strength / weakness / opportunity / threat) | yes | |
| statement | string | yes | |
| source | string | yes | evidence/reference |
| references | ref[] | yes | → [Risk](risk.md) / [Benefit](benefit.md) / [Market & Demand](market-and-demand.md) / [Current System](current-system.md) |

## 4. State (as-is / target)

Stateless — a synthesis view.

## 5. Relationships (semantic references)

- **Refers to:** [Risk](risk.md), [Benefit](benefit.md), [Market & Demand](market-and-demand.md), [Current System](current-system.md).
- **Referred by:** none.

## 6. Lifecycle / status

N/A — synthesis entry.

## 7. Template coverage

- `templates/analysis/viability-study.md` §12 SWOT Analysis

## 8. Non-overlap note

References rather than redefines risk, benefit, market, and current system. The underlying artefacts own the detailed semantics.
