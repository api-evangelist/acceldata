# Acceldata (acceldata)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Acceldata is an agentic data management platform that helps enterprises monitor, govern, and optimize data across cloud, lakehouse, and hybrid environments. The platform combines AI-powered agents with data observability to proactively detect issues, trace root causes, and automate remediation workflows. Key products include ADM (Agentic Data Management), ADOC (Acceldata Data Observability Cloud), Pulse for Hadoop environments, and Agent Studio for building custom AI agents. It supports integrations with Snowflake, Databricks, AWS, GCP, Azure, and Hadoop.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/acceldata/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - AI Agents, Data Management, Data Observability, Data Pipeline, Data Quality, Intelligence, Observability

## Timestamps

- **Created:** 2025-02-24
- **Modified:** 2026-04-19

## APIs

### Acceldata Data Observability Cloud API
The ADOC API provides programmatic access to data observability features including alerts, data quality rules, pipeline monitoring, data lineage, users, groups, roles, and permissions within the Acceldata Data Observability Cloud platform.

**Human URL:** [https://docs.acceldata.io/api/introduction](https://docs.acceldata.io/api/introduction)

#### Tags:

 - Data Observability, Data Quality, Alerts, Data Pipeline

#### Properties

- [Documentation](https://docs.acceldata.io/api/introduction)
- [Authentication](https://docs.acceldata.io/api/authentication)
- [OpenAPI](openapi/acceldata-adoc-api.yaml)
- [JSONSchema](json-schema/adoc-api-alert-schema.json)
- [JSONSchema](json-schema/adoc-api-alert-list-schema.json)
- [JSONSchema](json-schema/adoc-api-data-quality-rule-schema.json)
- [JSONSchema](json-schema/adoc-api-data-quality-rule-list-schema.json)
- [JSONSchema](json-schema/adoc-api-dataset-schema.json)
- [JSONSchema](json-schema/adoc-api-dataset-list-schema.json)
- [JSONSchema](json-schema/adoc-api-lineage-node-schema.json)
- [JSONSchema](json-schema/adoc-api-lineage-graph-schema.json)
- [JSONSchema](json-schema/adoc-api-pipeline-job-schema.json)
- [JSONSchema](json-schema/adoc-api-pipeline-job-list-schema.json)
- [JSONSchema](json-schema/adoc-api-user-schema.json)
- [JSONSchema](json-schema/adoc-api-user-list-schema.json)
- [JSONSchema](json-schema/adoc-api-role-schema.json)
- [JSONSchema](json-schema/adoc-api-role-list-schema.json)
- [JSONStructure](json-structure/adoc-api-alert-structure.json)
- [JSONStructure](json-structure/adoc-api-alert-list-structure.json)
- [JSONStructure](json-structure/adoc-api-data-quality-rule-structure.json)
- [JSONStructure](json-structure/adoc-api-data-quality-rule-list-structure.json)
- [JSONStructure](json-structure/adoc-api-dataset-structure.json)
- [JSONStructure](json-structure/adoc-api-dataset-list-structure.json)
- [JSONStructure](json-structure/adoc-api-lineage-node-structure.json)
- [JSONStructure](json-structure/adoc-api-lineage-graph-structure.json)
- [JSONStructure](json-structure/adoc-api-pipeline-job-structure.json)
- [JSONStructure](json-structure/adoc-api-pipeline-job-list-structure.json)
- [JSONStructure](json-structure/adoc-api-user-structure.json)
- [JSONStructure](json-structure/adoc-api-user-list-structure.json)
- [JSONStructure](json-structure/adoc-api-role-structure.json)
- [JSONStructure](json-structure/adoc-api-role-list-structure.json)
- [Example](examples/adoc-api-alert-example.json)
- [Example](examples/adoc-api-alert-list-example.json)
- [Example](examples/adoc-api-data-quality-rule-example.json)
- [Example](examples/adoc-api-dataset-example.json)
- [Example](examples/adoc-api-lineage-graph-example.json)
- [Example](examples/adoc-api-pipeline-job-example.json)
- [Example](examples/adoc-api-user-example.json)
- [Example](examples/adoc-api-role-example.json)

## Common Properties

- [Website](https://www.acceldata.io/)
- [Portal](https://accounts.acceldata.app/login)
- [Documentation](https://docs.acceldata.io/)
- [GettingStarted](https://docs.acceldata.io/api/introduction)
- [Pricing](https://www.acceldata.io/pricing)
- [Blog](https://www.acceldata.io/blog)
- [PrivacyPolicy](https://www.acceldata.io/privacy-policy)
- [TermsOfService](https://www.acceldata.io/terms-of-use)
- [SpectralRules](rules/acceldata-spectral-rules.yml)
- [NaftikoCapability](capabilities/data-observability.yaml)
- [Vocabulary](vocabulary/acceldata-vocabulary.yaml)
- [JSON-LD](json-ld/acceldata-adoc-api-context.jsonld)

## Features

| Name | Description |
|------|-------------|
| Agentic Data Management | AI-powered agents that proactively detect issues, trace root causes, and automate data quality remediation workflows |
| Data Quality Monitoring | Multi-variate anomaly detection, column-level profiling, and proactive monitoring across all data platforms |
| Data Lineage | End-to-end data lineage visualization with schema change management and column-level impact analysis |
| Pipeline Health Monitoring | Real-time SLA monitoring, bottleneck identification, and root cause analysis for data pipelines |
| Data Cost Management | Visibility into data spending, budget optimization, chargebacks, and cost forecasting across cloud environments |
| Business Notebook | Natural language interface with contextual memory for querying data quality and observability insights |
| Agent Studio | Low-code environment for building and deploying custom AI agents for data management workflows |
| BYOLLM Support | Bring Your Own Large Language Model for enterprise-controlled AI inference within data operations |
| xLake Reasoning Engine | Exabyte-scale, AI-aware processing engine supporting cloud hyperscalers and on-premises deployments |

## Use Cases

| Name | Description |
|------|-------------|
| Data Quality Assurance | Continuously monitor and automatically remediate data quality issues across cloud and hybrid environments |
| Cloud Migration Validation | Validate data completeness, consistency, and accuracy during cloud migration projects |
| AI and LLM Data Readiness | Ensure data pipelines produce clean, reliable, and AI-ready datasets for training and inference |
| Cost Optimization and FinOps | Identify and reduce wasteful data pipeline and infrastructure costs with granular usage analytics |
| Data Reconciliation | Automatically detect and resolve discrepancies between source and target systems across platforms |
| Compliance and Data Governance | Track data lineage and access patterns to support regulatory compliance and data governance programs |

## Integrations

| Name | Description |
|------|-------------|
| Snowflake | Native integration for monitoring Snowflake data quality, query performance, and cost optimization |
| Databricks | Integration for observing Databricks lakehouse pipelines, job health, and data quality |
| AWS | Support for AWS data services including S3, Redshift, Glue, EMR, and Athena |
| Google Cloud Platform | Integration with GCP data services including BigQuery, Dataflow, and Cloud Storage |
| Microsoft Azure | Integration with Azure Synapse, Azure Data Factory, and Azure Data Lake Storage |
| Hadoop / Apache | Dedicated Pulse product for Hadoop ecosystem monitoring including HDFS, YARN, Hive, and Spark |

## Artifacts

Machine-readable API specifications organized by format.

### OpenAPI

- [Acceldata Adoc Api](openapi/acceldata-adoc-api.yaml)

### JSON Schema

- [Adoc Api Acknowledge Alert Request](json-schema/adoc-api-acknowledge-alert-request-schema.json)
- [Adoc Api Alert List](json-schema/adoc-api-alert-list-schema.json)
- [Adoc Api Alert](json-schema/adoc-api-alert-schema.json)
- [Adoc Api Create Data Quality Rule Request](json-schema/adoc-api-create-data-quality-rule-request-schema.json)
- [Adoc Api Data Quality Rule List](json-schema/adoc-api-data-quality-rule-list-schema.json)
- [Adoc Api Data Quality Rule](json-schema/adoc-api-data-quality-rule-schema.json)
- [Adoc Api Dataset List](json-schema/adoc-api-dataset-list-schema.json)
- [Adoc Api Dataset](json-schema/adoc-api-dataset-schema.json)
- [Adoc Api Error Response](json-schema/adoc-api-error-response-schema.json)
- [Adoc Api Lineage Graph](json-schema/adoc-api-lineage-graph-schema.json)
- [Adoc Api Lineage Node](json-schema/adoc-api-lineage-node-schema.json)
- [Adoc Api Pipeline Job List](json-schema/adoc-api-pipeline-job-list-schema.json)
- [Adoc Api Pipeline Job](json-schema/adoc-api-pipeline-job-schema.json)
- [Adoc Api Role List](json-schema/adoc-api-role-list-schema.json)
- [Adoc Api Role](json-schema/adoc-api-role-schema.json)
- [Adoc Api User List](json-schema/adoc-api-user-list-schema.json)
- [Adoc Api User](json-schema/adoc-api-user-schema.json)

### JSON Structure

- [Adoc Api Acknowledge Alert Request](json-structure/adoc-api-acknowledge-alert-request-structure.json)
- [Adoc Api Alert List](json-structure/adoc-api-alert-list-structure.json)
- [Adoc Api Alert](json-structure/adoc-api-alert-structure.json)
- [Adoc Api Create Data Quality Rule Request](json-structure/adoc-api-create-data-quality-rule-request-structure.json)
- [Adoc Api Data Quality Rule List](json-structure/adoc-api-data-quality-rule-list-structure.json)
- [Adoc Api Data Quality Rule](json-structure/adoc-api-data-quality-rule-structure.json)
- [Adoc Api Dataset List](json-structure/adoc-api-dataset-list-structure.json)
- [Adoc Api Dataset](json-structure/adoc-api-dataset-structure.json)
- [Adoc Api Error Response](json-structure/adoc-api-error-response-structure.json)
- [Adoc Api Lineage Graph](json-structure/adoc-api-lineage-graph-structure.json)
- [Adoc Api Lineage Node](json-structure/adoc-api-lineage-node-structure.json)
- [Adoc Api Pipeline Job List](json-structure/adoc-api-pipeline-job-list-structure.json)
- [Adoc Api Pipeline Job](json-structure/adoc-api-pipeline-job-structure.json)
- [Adoc Api Role List](json-structure/adoc-api-role-list-structure.json)
- [Adoc Api Role](json-structure/adoc-api-role-structure.json)
- [Adoc Api User List](json-structure/adoc-api-user-list-structure.json)
- [Adoc Api User](json-structure/adoc-api-user-structure.json)

### JSON-LD

- [Acceldata Adoc Api Context](json-ld/acceldata-adoc-api-context.jsonld)

## Capabilities

Naftiko capabilities organized as shared per-API definitions composed into customer-facing workflows.

### Shared Per-API Definitions

- [acceldata-adoc-api](capabilities/shared/acceldata-adoc-api.yaml) — 9 operations for Acceldata Data Observability Cloud API shared capability for

### Workflow Capabilities

| Workflow | APIs Combined | Tools | Persona |
|----------|--------------|-------|---------|
| [data-observability](capabilities/data-observability.yaml) | acceldata-adoc-api | 6 | Data Engineer, Data Analyst |

## Vocabulary

- [Acceldata Vocabulary](vocabulary/acceldata-vocabulary.yaml) — Unified taxonomy mapping 7 resources, 5 actions, 1 workflows, and 4 personas across operational (OpenAPI) and capability (Naftiko) dimensions

## Rules

- [Acceldata Spectral Rules](rules/acceldata-spectral-rules.yml) — 25 rules enforcing Acceldata API conventions

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
