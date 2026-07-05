# Project Context

## One-line summary

AutoTime needs a governed, on-premise natural-language-to-SQL assistant that helps report writers generate valid SQL for AutoTime's external Report Writer without connecting to the production database and without using cloud LLM APIs.

## Product concept

The product is a standalone application installed by each AutoTime customer in its own environment. It receives a business question in natural language, interprets it locally, maps it to supported AutoTime report families, compiles governed SQL and returns copyable SQL for execution outside the product.

## Confirmed constraints

- Each customer will have its own installation.
- The customer installs the product on its own hardware or VM.
- Runtime must be on-premise / customer-controlled.
- No cloud LLM API.
- No external dependency for generation.
- The product does not execute SQL in production.
- The product does not connect to the production database at runtime.
- SQL is copied and later executed in AutoTime's external Report Writer.
- Initial support should focus on Labor Charge and Employee report families.
- The product must support multiple users issuing inference requests.
- Candidate scale tiers: up to 10, up to 20 and up to 30 concurrent users.
- Windows and Linux customers exist, but Linux may be justified as the recommended production tier for GPU serving.
- Windows support may be offered through a CPU-compatible tier if modern GPU serving does not fit Windows natively.

## Engineering-lab distinction

Although the product must not connect to the production database at runtime, the engineering project needs a lab environment with:

- AutoTime demo DB;
- schema metadata;
- example queries;
- report examples;
- golden dataset;
- eval harness;
- controlled execution of expected SQL versus generated SQL.

This distinction is critical:

| Environment | DB connection? | Purpose |
|---|---:|---|
| Engineering lab | Yes | Validate SQL, create evals, compare result sets |
| Delivered product runtime | No | Generate governed SQL offline for copy/paste |

## Primary risk

The primary technical risk is not merely SQL syntax. It is business scope and authorization semantics, especially expressions such as:

- my employees;
- my facility;
- my department;
- my team;
- employees under my management hierarchy.

The product should not pretend to understand a scoping rule unless it can deterministically apply it.

## Target outcome

Phase 1 should deliver a Working Product with engineering evidence:

- standalone app;
- local LLM runtime;
- semantic catalog;
- structured IR;
- deterministic SQL compiler;
- scope engine;
- validators;
- eval harness;
- golden dataset;
- deployment kit;
- UAT report;
- release candidate recommendation.
