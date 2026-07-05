# AutoTime Governed SQL Writer

Technical blueprint repository for the **AutoTime Governed SQL Writer** initiative.

This repository documents the preliminary engineering architecture for a standalone, on-premise, local-LLM application that generates governed SQL from natural language for use in AutoTime's external Report Writer.

## Purpose

The product is designed to generate SQL locally from:

- AutoTime schema metadata;
- example SQL queries and reports;
- a versioned semantic catalog;
- deterministic scoping rules;
- local open-weight LLMs;
- SQL validators and guardrails;
- golden datasets and evaluation harnesses.

The product **does not**:

- execute SQL in production;
- connect to the production database at runtime;
- call cloud LLM APIs;
- depend on external services;
- replace AutoTime authorization or runtime security;
- generate free-form SQL without validation.

## Core architectural principle

The LLM should not be treated as the SQL author of record.

The recommended design is:

```text
Natural Language
  -> Structured Intent / IR
  -> Semantic Resolution
  -> Deterministic SQL Compiler
  -> Scope Engine
  -> SQL Validators
  -> Governed SQL Output
```

## Documentation map

| Document | Description |
|---|---|
| [Project Context](docs/project/project-context.md) | Consolidated understanding of the AutoTime opportunity, constraints and scope. |
| [Solution Architecture](docs/architecture.md) | Logical architecture and main technical components. |
| [Runtime Request Sequence](docs/runtime-sequence.md) | Sequence from user request to governed SQL output. |
| [SQL Validation Flow](docs/validation-flow.md) | Decision flow for SQL generation, validation and abstention. |
| [Evaluation Pipeline](docs/eval-pipeline.md) | Golden dataset, eval harness and release gates. |
| [Deployment Topologies](docs/deployment-topologies.md) | On-premise deployment tiers for CPU, Linux GPU and higher concurrency. |
| [Delivery Plan](docs/delivery-plan.md) | 8-week working-product plan, team allocation and release criteria. |
| [Team Allocation](docs/project/team-allocation.md) | Person-by-person responsibility and average daily load. |
| [Engineering Decisions](docs/engineering/engineering-decisions.md) | Open and proposed architecture decisions. |
| [Open Questions](docs/project/open-questions.md) | Items to validate with AutoTime, Cole, Harold and SMEs. |
| [Research Notes](docs/research/research-notes.md) | Engineering conclusions from the technical research discussion. |

## Mermaid diagrams

Raw Mermaid files are available in [`diagrams/`](diagrams/):

| Diagram | File |
|---|---|
| Solution Architecture | [`diagrams/solution-architecture.mmd`](diagrams/solution-architecture.mmd) |
| Runtime Request Sequence | [`diagrams/runtime-request-sequence.mmd`](diagrams/runtime-request-sequence.mmd) |
| SQL Validation Flow | [`diagrams/sql-validation-flow.mmd`](diagrams/sql-validation-flow.mmd) |
| Evaluation Pipeline | [`diagrams/eval-pipeline.mmd`](diagrams/eval-pipeline.mmd) |
| Deployment Topologies | [`diagrams/deployment-topologies.mmd`](diagrams/deployment-topologies.mmd) |
| Engineering Workstream Map | [`diagrams/engineering-workstream-map.mmd`](diagrams/engineering-workstream-map.mmd) |

## Suggested 8-week delivery framing

The compressed 8-week plan should be positioned as a **Working Product with engineering evidence**, not as a fully hardened multi-client enterprise platform.

Included in the 8-week version:

- standalone app;
- local model runtime;
- Labor Charge and Employee report families;
- semantic catalog v1;
- structured IR;
- deterministic SQL compiler;
- scope engine;
- SQL guardrails;
- eval harness;
- initial golden dataset;
- local authentication;
- basic audit/history;
- Linux deployment kit;
- Windows feasibility or limited tier;
- UAT and release candidate.

Excluded from the 8-week version:

- all report families;
- direct production SQL execution;
- direct integration with AutoTime runtime;
- complete LDAP/OIDC/SAML implementation;
- high availability;
- multi-node serving;
- full enterprise hardening;
- large 500+ case golden dataset;
- fine-tuning or automatic retraining.

## Proposed team

| Person | Primary role | Secondary role | Allocation |
|---|---|---|---:|
| Erlon Rachi | Project/Delivery Manager | QA, validation, metrics, risk control | ~40% |
| José Marcos Ferreira | Data/SQL/AI Engineer | Semantic catalog, compiler, evals | ~90% |
| Persival Ballesté | AI Architect / Tech Lead | Runtime decision, prompts, guardrails, eval strategy | ~70% |
| Fábio Sarmento | Platform / Fullstack / DevOps / Security | App, packaging, auth, observability | ~90% |

## Key release candidate criteria

A release candidate should not be declared unless:

- the app runs standalone in the supported environment;
- the local model runtime works without cloud dependency;
- Labor Charge and Employee families are supported;
- SQL is generated through the IR + compiler path;
- validators block DDL/DML and unsafe SQL operations;
- scope rules are applied when required;
- the golden dataset runs end-to-end;
- the eval report is generated;
- installation smoke tests pass;
- UAT has been executed with AutoTime SME involvement;
- known limitations are documented.

## Internal note

The core of the project is not the LLM itself. The core is the governed engineering loop:

```text
Semantic Catalog + Golden Dataset + IR + Compiler + Scope Engine + Validators + Evals
```

This is what makes the solution defensible as an enterprise AI system rather than a demo chatbot that happens to output SQL.
