# Executive Summary

AutoTime needs a governed, on-premise natural-language-to-SQL assistant for report writers.

The product should help users express report questions in natural language, generate governed SQL locally, and return copyable SQL for use in AutoTime's external Report Writer.

## Core idea

The system should not trust an LLM to generate final SQL directly.

The recommended architecture is:

```text
Natural Language
  -> Structured Intent / IR
  -> Semantic Resolution
  -> Deterministic SQL Compiler
  -> Scope Engine
  -> SQL Validators
  -> Governed SQL Output
```

## Why this matters

Enterprise Text-to-SQL is risky because schemas are large, business terms are ambiguous and authorization scope is domain-specific. The project becomes defensible only if SQL generation is governed by explicit catalog, compiler, scope and eval assets.

## Phase 1 target

Phase 1 should deliver a working product with engineering evidence:

- standalone local application;
- local LLM runtime;
- Labor Charge and Employee report families;
- semantic catalog v1;
- structured IR;
- deterministic SQL compiler;
- scope engine;
- SQL validators;
- golden dataset and eval harness;
- deployment kit and smoke tests;
- UAT report and release recommendation.

## Main risks

- Unsupported business scope such as "my employees" or "my facility".
- Weak golden dataset or low SME validation coverage.
- Overpromising Windows GPU support before benchmark.
- Treating evals as final QA instead of part of the engineering loop.
- Letting the LLM become the SQL author of record.
