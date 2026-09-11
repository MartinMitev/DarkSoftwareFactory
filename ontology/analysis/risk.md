# Risk

> **Slug:** `risk` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a potential future harm with category, likelihood, impact, score, mitigation, owner, residual, and status — folding knowledge-concentration risk.
- **Purpose / when used:** the single risk artefact across viability, business case, and project plan; distinct from an issue (an occurred problem).

## 2. Semantics (crisp)

`risk` is a **potential future harm**: a category (technical, financial, operational, schedule, resource, compliance, vendor, organizational, migration, **knowledge-concentration**), a likelihood (Very Low → Very High), an impact (Negligible → Catastrophic), a score (likelihood × impact), a mitigation strategy (avoid/reduce/transfer/accept), an owner, a residual risk after mitigation, a financial-impact estimate, and a status (open/mitigated/occurred/closed). **Knowledge-concentration risk** (bus factor, sole experts, undocumented logic) is a risk with `category=knowledge`, plus `busFactor` and `experts` facets — folded here, not a separate artefact. It is **not** an issue (→ [Issue](issue.md)), **not** a technical-debt item (→ [Technical Debt Item](technical-debt-item.md)), and **not** a gap (→ [Gap & Contradiction](gap-and-contradiction.md)).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | |
| category | enum (technical / financial / operational / schedule / resource / compliance / vendor / organizational / migration / knowledge) | yes | knowledge = concentration risk |
| likelihood | enum (Very Low → Very High) | yes | |
| impact | enum (Negligible → Catastrophic) | yes | |
| score | int | yes | likelihood × impact |
| mitigationStrategy | enum (avoid / reduce / transfer / accept) | yes | |
| owner | ref → [Stakeholder](stakeholder.md) | yes | |
| residual | string | yes | residual risk after mitigation |
| financialImpact | string | no | if it materializes |
| status | enum (open / mitigated / occurred / closed) | yes | |
| busFactor | int | no | for knowledge-concentration risk |
| experts | string[] | no | for knowledge-concentration risk |

## 4. State (as-is / target)

Stateless — a potential harm.

## 5. Relationships (semantic references)

- **Refers to:** [Stakeholder](stakeholder.md) (owner).
- **Referred by:** [Current System](current-system.md), [Gap & Contradiction](gap-and-contradiction.md), [Option](option.md), [SWOT Item](swot-item.md), [Vendor](vendor.md), maintenance [Vulnerability Finding](../maintenance/vulnerability-finding.md) (linkedRisk), maintenance [Ticket](../maintenance/ticket.md) (linkedRisk).

## 6. Lifecycle / status

Status: open → mitigated → (occurred → becomes [Issue](issue.md)) → closed. Reviewed at gates and sprints.

## 7. Template coverage

- `templates/analysis/viability-study.md` §11 Risk Assessment, §3.4 Knowledge Concentration Risk, §5.8 Technical Risks, Appendix E
- `templates/analysis/business-case.md` §10 Risk Assessment, §5.4 Risk Comparison
- `templates/analysis/project-plan.md` §10 Risk Management, Appendix C

## 8. Non-overlap note

An occurred problem belongs to [Issue](issue.md); tracked debt belongs to [Technical Debt Item](technical-debt-item.md); a missing piece of info belongs to [Gap & Contradiction](gap-and-contradiction.md). Knowledge-concentration risk is folded via `category=knowledge`.
