# Code Unit

> **Slug:** `code-unit` | **View:** Source View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** the atomic unit of source code — a file, class, module, function, or test source — that realises a design [Component](../design/component.md).
- **Purpose / when used:** the atomic unit of written implementation; the thing that is version-controlled ([Code Commit](code-commit.md)), built ([Build Artifact](build-artifact.md)), and analysed ([Static Analysis Finding](static-analysis-finding.md)).

## 2. Semantics (crisp)

`code-unit` is a piece of written source. It has a `kind` (source / test / config / script), a path/location, a language (analysis [Technology](../analysis/technology.md)), and a `testFacet` (`unitTest` true for co-located unit tests — full test *design/execution/reporting* belongs to the testing phase, not here). It realises one design [Component](../design/component.md), may implement [Design Pattern](../design/design-pattern.md)s, is subject to design [Crosscutting Concern](../design/crosscutting-concern.md)s (e.g. logging calls, security API usage), is authored by an analysis [Role](../analysis/role.md), and is constrained by analysis [Constraint](../analysis/constraint.md)s (the `convention` constraint type already covers coding standards / style guides / naming conventions). It carries two dependency attributes that document the code-unit dependency graph: `dependsOn` (outbound — the [Code Unit](code-unit.md)s this unit imports/uses) and `dependedBy` (inbound — the [Code Unit](code-unit.md)s that import/use this unit). It is **not** the design abstraction (→ [Component](../design/component.md)), **not** the VCS change (→ [Code Commit](code-commit.md)), **not** the build output (→ [Build Artifact](build-artifact.md)), and **not** a test plan/case/result (→ testing phase).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. CU-001 |
| path | string | yes | repository path / location |
| kind | enum (source / test / config / script) | yes | |
| language | ref → [Technology](../analysis/technology.md) | yes | the language/framework |
| realises | ref → [Component](../design/component.md) | yes | the design block it implements |
| implementsPatterns | ref[] → [Design Pattern](../design/design-pattern.md) | no | |
| subjectTo | ref[] → [Crosscutting Concern](../design/crosscutting-concern.md) | no | enforced policies in code |
| conformsTo | ref[] → [Constraint](../analysis/constraint.md) | no | coding standards / conventions (constraint type=convention) |
| authoredBy | ref → [Role](../analysis/role.md) | yes | |
| dependsOn | ref[] → [Code Unit](code-unit.md) | no | the code units this unit depends on (outbound dependencies) |
| dependedBy | ref[] → [Code Unit](code-unit.md) | no | the code units that depend on / reference this unit (inbound dependencies) |
| testFacet | table (unitTest bool / testFramework) | no | true for co-located unit-test sources only |

## 4. State (as-is / target)

Stateful. As-is units (existing source, 🟤🔵 — counterpart of the as-is design) vs target units (new/modified source). A `changeType` (new / modified / preserved / retired) tracks Brown Field / Modernization changes at the file level.

## 5. Relationships (semantic references)

- **Refers to:** [Component](../design/component.md) (realises), [Design Pattern](../design/design-pattern.md), [Crosscutting Concern](../design/crosscutting-concern.md), [Technology](../analysis/technology.md), [Role](../analysis/role.md), [Constraint](../analysis/constraint.md), [Code Unit](code-unit.md) (dependsOn — code-unit dependency graph).
- **Referred by:** [Code Unit](code-unit.md) (dependedBy — code-unit dependency graph), [Code Commit](code-commit.md), [Build Configuration](build-configuration.md), [Build Artifact](build-artifact.md), [Code Review](code-review.md), [Static Analysis Finding](static-analysis-finding.md), [Refactoring](refactoring.md).

## 6. Lifecycle / status

N/A — source artefact; status follows the containing repository's VCS state. New/modified/removed via [Code Commit](code-commit.md).

## 7. Template coverage

- A future `templates/development/*.md` source-structure section (file/module inventory per realised component).
- Maps to the implementation of `templates/design/software-architecture.md` §6 Building Block View (each Component is realised by Code Units).

## 8. Non-overlap note

The design abstraction belongs to [Component](../design/component.md); the VCS change belongs to [Code Commit](code-commit.md); the build output belongs to [Build Artifact](build-artifact.md); the test design/execution belongs to the testing phase. Coding standards are analysis [Constraint](../analysis/constraint.md) (convention type), not a separate dev artefact.
