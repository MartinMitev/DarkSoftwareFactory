# Work Package

> **Slug:** `work-package` | **Layer:** L5 Scope & Planning | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a WBS node — description, scope items covered, deliverables, acceptance criteria, dependencies, and effort.
- **Purpose / when used:** the work decomposition unit; collectively covers 100% of in-scope items.

## 2. Semantics (crisp)

`work-package` is the **work decomposition** node of the WBS: a description, the scope items it covers, the deliverables it produces, its acceptance criteria, dependencies on other work packages, and effort. It is **not** the deliverable (→ [Deliverable](deliverable.md)), **not** the scope item (→ [Scope Item](scope-item.md)), and **not** a phase (→ [Phase](phase.md)). Migration-specific work packages (data migration, transition, dual-running, decommission, legacy support) are work-package instances.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. WP1, WP1.1 |
| description | string | yes | |
| parentWorkPackage | ref → [Work Package](work-package.md) | no | parent WBS node (containment hierarchy) |
| scopeItemsCovered | ref[] → [Scope Item](scope-item.md) | yes | |
| deliverables | ref[] → [Deliverable](deliverable.md) | yes | |
| acceptanceCriteria | string | yes | |
| dependencies | ref[] → [Dependency](dependency.md) | no | |
| effort | string | yes | traces to [Estimate](estimate.md) |

## 4. State (as-is / target)

Stateful. As-is work packages (current work) vs target work packages.

## 5. Relationships (semantic references)

- **Refers to:** [Scope Item](scope-item.md), [Deliverable](deliverable.md), [Dependency](dependency.md), [Estimate](estimate.md), [Work Package](work-package.md) (parentWorkPackage).
- **Referred by:** [Change Request](change-request.md), [Dependency](dependency.md), [Estimate](estimate.md), [Scope Item](scope-item.md), [Work Package](work-package.md) (parentWorkPackage).

## 6. Lifecycle / status

N/A — decomposition node; status follows hosting document approval.

## 7. Template coverage

- `templates/analysis/project-scope.md` §10 Work Breakdown Structure (§10.1 high-level, §10.2 dictionary)

## 8. Non-overlap note

The produced artifact belongs to [Deliverable](deliverable.md); the unit of scope belongs to [Scope Item](scope-item.md); the time span belongs to [Phase](phase.md).
