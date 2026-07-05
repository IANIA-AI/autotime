# Product Boundaries

These boundaries are non-negotiable unless the project scope is explicitly changed.

## Runtime boundaries

The delivered product runtime:

- does not execute SQL in production;
- does not connect to the production database;
- does not call cloud LLM APIs;
- does not depend on external services for generation;
- does not bypass AutoTime's external Report Writer;
- does not replace AutoTime authorization or runtime security.

## Generation boundaries

The LLM should not produce final trusted SQL directly.

The LLM may help produce structured intent, but governed SQL must be produced through:

- semantic catalog resolution;
- deterministic SQL compilation;
- scope enforcement;
- SQL parsing and validation;
- policy checks;
- controlled refusal when the request is unsupported or unsafe.

## Scope boundaries

The product should not pretend to understand business scope unless it can apply that scope deterministically.

Examples that require explicit rules:

- my employees;
- my facility;
- my department;
- my team;
- employees under my management hierarchy.

Unknown or unsupported scope should produce abstention, not guessed SQL.

## Deployment boundaries

The target deployment model is customer-controlled and on-premise.

Windows support is a tier decision, not a promise of equal capability across all runtime profiles. Linux should remain the recommended production direction for GPU-backed higher-concurrency serving until benchmark evidence says otherwise.
