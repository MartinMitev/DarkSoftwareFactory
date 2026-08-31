# Compliance Requirement

> **Slug:** `compliance-requirement` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a regulatory or legal obligation — regulation, article, system requirement, evidence, gap — including data-protection and audit/forensic obligations.
- **Purpose / when used:** the external rule that drives requirements, data handling, and constraints; distinct from the requirement itself.

## 2. Semantics (crisp)

`compliance-requirement` is a **regulatory/legal obligation**: a regulation (GDPR, HIPAA, PCI-DSS, SOX, DORA, EU AI Act), the specific article/section, the system requirement it drives, the compliance evidence required, and (for Brown Field / Modernization) the gap in the current system. It also covers **data-protection** obligations (consent, data-subject rights, breach notification, cross-border transfer, PIA) and **audit/forensic** obligations (audit trail, log immutability, retention, access control, compliance reporting). It is **not** the requirement ("system shall" — → [Requirement](requirement.md)) and **not** a constraint (→ [Constraint](constraint.md)). A security NFR (nfrCategory=security) *realises* a compliance-requirement; the obligation lives here.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| regulation | string | yes | e.g. GDPR, HIPAA |
| article | string | yes | specific section |
| systemRequirement | string | yes | what the system must satisfy |
| evidence | string | yes | compliance evidence required |
| gap | string | no | 🟤🔵 current-system gap |
| dataProtection | string | no | consent, DSR, breach, cross-border |
| auditForensic | string | no | audit trail, retention, access control |

## 4. State (as-is / target)

Stateless — an external obligation.

## 5. Relationships (semantic references)

- **Refers to:** [Requirement](requirement.md), [Data Entity](data-entity.md), [Constraint](constraint.md).
- **Referred by:** [Business Rule](business-rule.md), [Constraint](constraint.md), [Data Entity](data-entity.md), [Requirement](requirement.md).

## 6. Lifecycle / status

N/A — obligation; compliance status tracked over time.

## 7. Template coverage

- `templates/analysis/viability-study.md` §6 Security & Compliance (§6.1 posture, §6.2 regulatory, §6.3 IP, §6.4 contractual)
- `templates/analysis/software-requirements-specification.md` §10 Security & Compliance Requirements (§10.1 regulatory matrix, §10.2 data protection, §10.3 audit/forensic)
- `templates/analysis/project-plan.md` Appendix G Compliance & Regulatory Requirements
- `templates/analysis/project-scope.md` §8.4 Data Security & Privacy (compliance drivers)

## 8. Non-overlap note

The "system shall" belongs to [Requirement](requirement.md) (a security NFR realises the obligation). The limitation belongs to [Constraint](constraint.md). The compliance-requirement owns the external rule.
