# Architecture Overview

The product should behave like a governed compiler-backed assistant, not a free-form SQL chatbot.

## Main flow

```text
Natural Language
  -> Structured Intent / IR
  -> Semantic Resolution
  -> Deterministic SQL Compiler
  -> Scope Engine
  -> SQL Validators
  -> Governed SQL Output
```

## Main components

| Layer | Components | Responsibility |
|---|---|---|
| Application | Web UI, Backend API, Auth, History, Queue | User workflow, access, request tracking and concurrency. |
| Generation Core | Context selector, local LLM, IR validator, compiler, scope engine, validators | Converts supported requests into governed SQL or controlled refusal. |
| Knowledge Layer | Schema metadata, examples, glossary, allowed joins, scope rules, semantic catalog | Provides controlled meaning for business terms and SQL generation. |
| Observability and Evals | Trace store, audit log, feedback, eval harness, golden dataset, metrics | Makes quality measurable and regressions visible. |
| Deployment Kit | Local model weights, config, smoke tests, install/admin docs | Enables customer-controlled on-prem installation. |

## Simplified request behavior

1. User asks a report question.
2. Backend authenticates and traces the request.
3. Context selector chooses the report family and semantic subset.
4. Local LLM generates structured intent.
5. IR validator accepts or rejects the intent.
6. Compiler produces SQL from resolved semantic bindings.
7. Scope engine injects mandatory filters.
8. Validators check safety, policy and scope.
9. Product returns governed SQL or controlled refusal.

## Detailed references

- [Runtime Flow](runtime-flow.md)
- [Validation Flow](validation-flow.md)
- [Detailed Solution Architecture](../90-reference/detailed-architecture.md)
- Raw Mermaid: [../../diagrams/solution-architecture.mmd](../../diagrams/solution-architecture.mmd)
