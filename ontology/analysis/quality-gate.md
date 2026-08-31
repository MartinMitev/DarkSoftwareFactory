# Quality Gate

> **Slug:** `quality-gate` | **Layer:** L6 Cross-cutting Concerns | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a work-item or release pass/fail checkpoint — Definition of Ready, Definition of Done, Release-Readiness, or Migration-Readiness — with criterion, measured-by, and enforced-at.
- **Purpose / when used:** the single artefact for DoR/DoD/release-readiness/migration-readiness across scope, SRS, user stories, and project plan.

## 2. Semantics (crisp)

`quality-gate` is a **work-item or release pass/fail checkpoint**: a `gateType` (DoR / DoD / release-readiness / migration-readiness), a criterion (e.g. code reviewed, tests passing, coverage threshold, security scan clean, parity verified, data migration validated), a `measuredBy` (PR approval, CI pipeline, PO sign-off), and an `enforcedAt` (merge gate, release gate, sprint review). It folds DoR, DoD, release-readiness, and migration-readiness into one artefact. It is **not** the phase-level governance review (→ [Stage Gate](stage-gate.md)) and **not** a single acceptance criterion (→ [Acceptance Criterion](acceptance-criterion.md)) — it aggregates criteria.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| gateType | enum (DoR / DoD / release-readiness / migration-readiness) | yes | |
| criterion | string | yes | e.g. coverage ≥ 80% |
| measuredBy | string | yes | CI / PR / PO |
| enforcedAt | string | yes | merge gate / release gate / sprint review |

## 4. State (as-is / target)

Journey — a checkpoint on the delivery path.

## 5. Relationships (semantic references)

- **Refers to:** [User Story](user-story.md), [Requirement](requirement.md), [Release](release.md), [Cutover](cutover.md), [Acceptance Criterion](acceptance-criterion.md).
- **Referred by:** [Release](release.md), [Verification & Validation](verification-validation.md).

## 6. Lifecycle / status

N/A — checkpoint; pass/fail per work item or release.

## 7. Template coverage

- `templates/analysis/project-scope.md` §11 Acceptance Criteria & Definition of Done (§11.1, §11.2 DoD, §11.3 release readiness)
- `templates/analysis/software-requirements-specification.md` §14.2 Validation Approach (acceptance gates)
- `templates/analysis/user-stories.md` §9 Definition of Ready & Definition of Done
- `templates/analysis/project-plan.md` §9.3 Definition of Done, §18.2 Release Readiness Checklist

## 8. Non-overlap note

The phase-level review belongs to [Stage Gate](stage-gate.md); a single AC belongs to [Acceptance Criterion](acceptance-criterion.md). Quality Gate aggregates work-item/release criteria.
