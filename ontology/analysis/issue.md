# Issue

> **Slug:** `issue` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** an occurred problem with category, priority, owner, status, resolution, and impact.
- **Purpose / when used:** the present-tense realised problem/blocker; distinct from a risk (a potential future harm).

## 2. Semantics (crisp)

`issue` is an **occurred present problem**: a description, a category (technical, process, resource, dependency, vendor, organizational, migration), a priority (critical/high/medium/low), an owner, a status (open/in-progress/resolved/closed), a resolution, and an impact (budget/schedule/scope/quality). It is **not** a risk (a potential future harm — → [Risk](risk.md)), **not** a defect (testing-phase artefact), and **not** a gap (→ [Gap & Contradiction](gap-and-contradiction.md)). For Brown Field / Modernization it includes migration issues (data inconsistency, feature gap, cutover blockers). A risk that materialises becomes an issue.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| description | string | yes | |
| category | string | yes | |
| priority | enum (critical / high / medium / low) | yes | |
| owner | ref → [Stakeholder](stakeholder.md) | yes | |
| status | enum (open / in-progress / resolved / closed) | yes | |
| resolution | string | no | |
| impact | string | yes | budget/schedule/scope/quality |

## 4. State (as-is / target)

Stateless — a present problem.

## 5. Relationships (semantic references)

- **Refers to:** [Stakeholder](stakeholder.md) (owner).
- **Referred by:** none.

## 6. Lifecycle / status

Status: open → in-progress → resolved → closed. Critical issues escalate immediately.

## 7. Template coverage

- `templates/analysis/project-plan.md` §15 Issue Management (incl. §15.1 process, §15.2 priorities, §15.3 log)

## 8. Non-overlap note

A potential future harm belongs to [Risk](risk.md); a missing piece of info belongs to [Gap & Contradiction](gap-and-contradiction.md).
