# Verification & Validation

> **Slug:** `verification-validation` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the verification and validation approach — verification methods per requirement category (demo/test/inspection/analysis), test levels, validation (UAT/pilot/parallel), and requirement quality criteria.
- **Purpose / when used:** the V&V strategy; referenced by requirements and quality gates.

## 2. Semantics (crisp)

`verification-validation` is the **V&V strategy**: verification methods per requirement category (demonstration, test, inspection, analysis), test levels (unit/integration/system/acceptance), validation approach (stakeholder review, UAT, pilot, parallel testing for 🟤🔵), responsible parties, and the requirement quality criteria (necessary, unambiguous, testable, traceable, complete, consistent, feasible, singular). It answers "did we build it right" (verification) and "did we build the right thing" (validation). It is **not** the quality-gate checkpoint (→ [Quality Gate](quality-gate.md)) and **not** the detailed testing-phase test concept (downstream elaboration). It also carries the delivery-methodology facet referenced by the project plan.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| verificationMethods | table | yes | per requirement category |
| testLevels | string | yes | unit/integration/system/acceptance |
| validationApproach | string | yes | UAT/pilot/parallel |
| qualityCriteria | table | yes | necessary/unambiguous/testable/… |
| responsible | ref[] → [Stakeholder](stakeholder.md) | yes | |

## 4. State (as-is / target)

Stateless — a strategy.

## 5. Relationships (semantic references)

- **Refers to:** [Requirement](requirement.md), [Use Case](use-case.md), [Quality Gate](quality-gate.md), [Stakeholder](stakeholder.md).
- **Referred by:** none.

## 6. Lifecycle / status

N/A — strategy; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/software-requirements-specification.md` §14 Verification & Validation (§14.1 verification, §14.2 validation, §14.3 acceptance, §14.4 quality criteria)
- `templates/analysis/viability-study.md` §9 Quality & Testing Strategy
- `templates/analysis/project-plan.md` §9 Quality Management (§9.1 strategy, §9.2 testing strategy), §2.3 Delivery Methodology

## 8. Non-overlap note

The checkpoint enforcement belongs to [Quality Gate](quality-gate.md); detailed test cases belong to the testing phase. Verification & Validation owns the strategy.
