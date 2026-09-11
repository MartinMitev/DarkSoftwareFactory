# Decision

> **Slug:** `decision` | **Layer:** L4 Investment Decision & Viability | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a recorded decision — viability go/no-go, recommended option, stage-gate outcome, change approval, cutover/rollback, architecture decision (ADR), or organizational decision — with authority, outcome, rationale, and (for ADRs) alternatives and compliance.
- **Purpose / when used:** the single artefact for every recorded decision across analysis and design; folds the Architecture Decision Record (ADR) as a fully-fleshed variant, including the design-phase ADR format (title, context, decision, alternatives table, consequences, compliance).

## 2. Semantics (crisp)

`decision` is the **recorded outcome** of a decision: type, authority, outcome, rationale, date, status. It covers viability go/no-go, business-case recommended option, stage-gate outcomes, change approvals, cutover/rollback decisions, organizational decisions (team topology, build-vs-buy execution), and **architecture decisions** — the ADR variant. The ADR variant carries the full Nygard/arc42 structure: `adrTitle`, `adrContext`, `adrDecision`, an `alternativesConsidered` table (alternative / pros / cons / reason for rejection), `adrConsequences` (what becomes easier / more difficult), a `compliance` field (how compliance with the decision is enforced), a `sectionReference` back into the hosting document, and ADR-style status (proposed / accepted / deprecated / superseded). ADR instances are written during the design phase and are *justified-by* references from design artefacts (component, infrastructure-resource, design-pattern) — those design artefacts link back here; `decision` itself does not link forward into the design phase, keeping analysis self-contained. It is **not** the request (→ [Change Request](change-request.md)), **not** the gate review (→ [Stage Gate](stage-gate.md)), and **not** the option (→ [Option](option.md)) — a decision *selects* an option. A change-request approval is recorded as a decision.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| type | enum (viability / option / stage-gate / change / cutover / rollback / architecture / organizational) | yes | ADR = architecture; organizational = team topology / execution model |
| authority | ref → [Governance](governance.md) | yes | |
| outcome | string | yes | |
| rationale | string | yes | |
| date | date | yes | |
| status | enum (proposed / accepted / deprecated / superseded) | yes | ADR-style statuses |
| adrTitle | string | no | short noun phrase; required for architecture decisions |
| adrContext | string | no | issue motivating the decision; for architecture decisions |
| adrDecision | string | no | the change/approach chosen; for architecture decisions |
| alternativesConsidered | table (alternative / pros / cons / rejection) | no | for architecture decisions |
| adrConsequences | table (easier / moreDifficult) | no | for architecture decisions |
| compliance | string | no | how compliance with the decision is ensured; for architecture decisions |
| sectionReference | string | no | back-reference into the hosting document section |
| supersedes | ref → [Decision](decision.md) | no | the prior decision this one replaces (ADR supersession chain) |

## 4. State (as-is / target)

Stateless — a recorded decision.

## 5. Relationships (semantic references)

- **Refers to:** [Option](option.md), [Stage Gate](stage-gate.md), [Change Request](change-request.md), [Milestone](milestone.md), [Cutover](cutover.md), [Decision](decision.md) (supersedes).
- **Referred by:** [Change Request](change-request.md), [Cutover](cutover.md), [Decision](decision.md) (supersedes), [Gap & Contradiction](gap-and-contradiction.md), [Governance](governance.md), [Milestone](milestone.md), [Stage Gate](stage-gate.md), rollout [Deployment Runbook](../rollout/deployment-runbook.md) (justifiedBy), rollout [Deployment Execution](../rollout/deployment-execution.md) (approvedBy), maintenance [Maintenance Log](../maintenance/maintenance-log.md) (approvedBy).

## 6. Lifecycle / status

Status: proposed → accepted → (deprecated / superseded). ADRs follow the same lifecycle.

## 7. Template coverage

- `templates/analysis/viability-study.md` §14 Recommendations & Conclusion, Appendix D (ADRs)
- `templates/analysis/business-case.md` §6 Recommended Option, §15 Governance & Approval (decision authority)
- `templates/analysis/project-scope.md` Appendix G (ADRs)
- `templates/analysis/project-plan.md` §5.2 Decision Framework, §17 cutover decisions, Appendix E (ADRs)
- `templates/design/software-architecture.md` §5.5 Organizational Decisions, §10 Architecture Decisions (§10.1 ADR list, §10.2/10.3 ADR detail, §10.4 Migration Decision Records) — ADR instances are written during design and are referenced (justified-by) from design artefacts.

## 8. Non-overlap note

The request belongs to [Change Request](change-request.md); the phase review belongs to [Stage Gate](stage-gate.md); the alternative belongs to [Option](option.md). Architecture decisions (ADRs) and organizational decisions are owned here as variants — there is no separate design-phase `architecture-decision` artefact, to avoid overlap with the design ontology.
