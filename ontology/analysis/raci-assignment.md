# RACI Assignment

> **Slug:** `raci-assignment` | **Layer:** L2 Business Architecture | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** per-activity Responsible / Accountable / Consulted / Informed assignments of roles within a business process.
- **Purpose / when used:** describes how different roles interact within a process — who does the work, who is answerable, who is consulted, who is informed.

## 2. Semantics (crisp)

`raci-assignment` is a **coordination matrix** for one activity of a [Business Process](business-process.md): each role is assigned exactly one of R/A/C/I, with **exactly one Accountable** per activity (the single answerable party). It is **not** the role definition itself (→ [Role](role.md)), **not** the process (→ [Business Process](business-process.md)), and **not** a governance decision-rights matrix (→ [Governance](governance.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| activity | string | yes | the process activity |
| role | ref → [Role](role.md) | yes | the assigned role |
| raci | enum (R / A / C / I) | yes | exactly one A per activity |

## 4. State (as-is / target)

Stateful. As-is RACI (current coordination) vs target RACI (improved coordination).

## 5. Relationships (semantic references)

- **Refers to:** [Business Process](business-process.md), [Role](role.md).
- **Referred by:** none.

## 6. Lifecycle / status

N/A — matrix; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/project-plan.md` §6.2 RACI Matrix

## 8. Non-overlap note

Role identity and permissions belong to [Role](role.md). Project-level decision rights belong to [Governance](governance.md).
