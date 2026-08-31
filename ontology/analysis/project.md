# Project

> **Slug:** `project` | **Layer:** L0 Root | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the root container for one analysis engagement; carries the metadata block and the project-type classification that drives the applicability of every other artefact.
- **Purpose / when used:** every analysis engagement has exactly one `project`; it owns the project type (Green Field / Brown Field / Software Modernization) and the administrative metadata that recurs at the top of each template.

## 2. Semantics (crisp)

`project` is the **root** of the ontology: all other artefacts belong to exactly one project. It owns the **project-type classification** (🟢 / 🟤 / 🔵) which, per the README legend, drives the applicability of downstream artefacts. It is **not** a deliverable and holds **no domain semantics** — all business, requirements, investment, planning, and cross-cutting content lives in lower-layer artefacts. The metadata block at the top of every template (project name, sponsor, product owner, technical lead, classification, baseline version) is an instance of `project`.

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| name | string | yes | project name |
| type | enum (Green Field / Brown Field / Software Modernization) | yes | drives artefact applicability |
| sponsor | ref → [Stakeholder](stakeholder.md) | yes | sponsoring stakeholder/department |
| productOwner | ref → [Stakeholder](stakeholder.md) | yes | |
| technicalLead | ref → [Stakeholder](stakeholder.md) | yes | |
| projectManager | ref → [Stakeholder](stakeholder.md) | no | |
| authors | string[] | no | |
| reviewers | string[] | no | |
| classification | enum (Public / Internal / Confidential) | no | |
| baselineVersion | string | no | set on approval |
| projectId | string | no | unique identifier |
| program | string | no | parent program name |

## 4. State (as-is / target)

Stateless. `project` describes the engagement itself, not a system state.

## 5. Relationships (semantic references)

- **Refers to:** none (it is the root).
- **Referred by:** [Documentation Inventory](documentation-inventory.md), [Project Understanding](project-understanding.md).

## 6. Lifecycle / status

N/A — root artefact. Status follows the hosting document's approval/baseline process.

## 7. Template coverage

Supplies the **Metadata** block and the **Project Type Classification** (§2.2) of every template:

- `templates/analysis/viability-study.md` §0 Metadata, §2.2
- `templates/analysis/business-case.md` §0 Metadata, §2.2
- `templates/analysis/project-scope.md` §0 Metadata, §2.2
- `templates/analysis/software-requirements-specification.md` §0 Metadata, §2.2
- `templates/analysis/user-stories.md` §0 Metadata, §1.2
- `templates/analysis/project-plan.md` §0 Metadata, §2.2

## 8. Non-overlap note

`project` holds **only** metadata and the project-type classification. All domain semantics live in lower-layer artefacts. No other artefact redefines the metadata block or the project-type classification.
