# Infrastructure Resource

> **Slug:** `infrastructure-resource` | **View:** Infrastructure View | **Applicability:** ⚪

## 1. Identity & definition

- **Definition (one sentence):** a concrete physical, virtual, or cloud hosting resource — location, computer/processor, container host, network zone, or storage unit — with quality/performance features, that executes deployed software.
- **Purpose / when used:** the atomic unit of the deployment infrastructure; the concrete provisioned environment that [Deployment Node](deployment-node.md)s map [Component](component.md)s onto and that resides in an [Environment](environment.md).

## 2. Semantics (crisp)

`infrastructure-resource` is a **concrete provisioned resource** — a geographical location, a computer/processor, a container host (e.g. a Kubernetes cluster), a network zone/subnet, or a storage unit — with quality/performance features (capacity, throughput, redundancy) and an internal structure (sub-elements at level 2). It is an *instance* of an analysis [Technology](../analysis/technology.md) (e.g. the technology "Kubernetes" vs the resource "prod-k8s-cluster-eu1"). It resides in an [Environment](environment.md) (dev/test/staging/prod/migration-parallel) and is the target of [Deployment Node](deployment-node.md) mappings. It is **not** the technology choice (→ [Technology](../analysis/technology.md)), **not** the software building block (→ [Component](component.md)), **not** the mapping of software to infrastructure (→ [Deployment Node](deployment-node.md)), and **not** the environment (→ [Environment](environment.md)). For Brown Field / Modernization, as-is instances are legacy infrastructure; target instances are new infrastructure; retired instances are decommissioned with the [Legacy Decommission](../analysis/legacy-decommission.md).

## 3. Attributes

| Attribute | Type | Required | Notes |
|---|---|---|---|
| id | string | yes | e.g. IR-001 |
| name | string | yes | e.g. prod-k8s-cluster-eu1 |
| kind | enum (location / computer / processor / container-host / network-zone / storage) | yes | |
| instanceOf | ref → [Technology](../analysis/technology.md) | yes | the technology this is an instance of |
| residesIn | ref → [Environment](environment.md) | yes | |
| qualityPerformance | string | yes | capacity / throughput / redundancy |
| contains | ref[] → [Infrastructure Resource](infrastructure-resource.md) | no | contained sub-resources (level-2 containment hierarchy) |
| subElements | table (subElement / purpose / qualityPerformance) | no | level-2 internal structure |
| changeType | enum (new / modified / preserved / retired) | no | 🟤🔵 |
| retirementTimeline | string | no | 🟤🔵 linked to [Legacy Decommission](../analysis/legacy-decommission.md) |
| justifiedBy | ref → [Decision](../analysis/decision.md) | no | ADR justifying this resource |

## 4. State (as-is / target)

Stateful. As-is infrastructure (legacy, 🟤🔵) vs target infrastructure; transition infrastructure for dual-running.

## 5. Relationships (semantic references)

- **Refers to:** [Technology](../analysis/technology.md) (instance of), [Environment](environment.md) (resides in), [Legacy Decommission](../analysis/legacy-decommission.md) (🟤🔵), [Decision](../analysis/decision.md) (justified by), [Infrastructure Resource](infrastructure-resource.md) (contains).
- **Referred by:** [Deployment Node](deployment-node.md), [Environment](environment.md), [Infrastructure Resource](infrastructure-resource.md) (contains), [Decision](../analysis/decision.md), maintenance [Monitoring Alert](../maintenance/monitoring-alert.md), maintenance [Vulnerability Finding](../maintenance/vulnerability-finding.md).

## 6. Lifecycle / status

N/A — provisioned resource; status follows hosting document approval. Provisioning tracked by [Work Package](../analysis/work-package.md).

## 7. Template coverage

- `templates/design/software-architecture.md` §8.1 Infrastructure Level 1 (top-level infrastructure + quality/performance features), §8.2 Infrastructure Level 2 (internal structure / sub-elements), §8.4 Legacy Deployment 🔵🟤 (current / transition / target / retirement)

## 8. Non-overlap note

The technology choice belongs to [Technology](../analysis/technology.md); the software building block belongs to [Component](component.md); the software-to-infrastructure mapping belongs to [Deployment Node](deployment-node.md); the environment context belongs to [Environment](environment.md).
