# Runtime Request Sequence

This document describes the end-to-end runtime behavior when a report writer asks a question in natural language.

```mermaid
sequenceDiagram
    autonumber

    actor User as Report Writer
    participant UI as Web UI
    participant API as Backend API
    participant Auth as Auth Module
    participant Queue as Inference Queue
    participant Catalog as Semantic Catalog
    participant LLM as Local LLM Runtime
    participant IR as IR Validator
    participant Compiler as SQL Compiler
    participant Scope as Scope Engine
    participant Validator as SQL Validators
    participant Trace as Trace/Audit Store

    User->>UI: Ask report question in natural language
    UI->>API: Submit request
    API->>Auth: Validate session / user
    Auth-->>API: Authenticated

    API->>Trace: Create request trace
    API->>Queue: Enqueue inference job
    Queue->>Catalog: Select report family context
    Catalog-->>Queue: Schema subset + glossary + allowed joins + rules

    Queue->>LLM: Prompt with constrained context
    LLM-->>Queue: Structured intent candidate

    Queue->>IR: Validate JSON schema and supported intent
    alt Invalid or unsupported intent
        IR-->>API: Reject with reason
        API->>Trace: Log abstention
        API-->>UI: Return controlled refusal
        UI-->>User: Explain unsupported request
    else Valid intent
        IR-->>Compiler: Valid IR
        Compiler->>Catalog: Resolve entities, metrics, dimensions
        Catalog-->>Compiler: Resolved semantic bindings

        Compiler->>Scope: Generate SQL draft
        Scope->>Scope: Inject mandatory scoping filters
        Scope-->>Validator: Scoped SQL candidate

        Validator->>Validator: Parse SQL / check AST / read-only / policy / scope
        alt SQL passes all validators
            Validator-->>API: Approved governed SQL
            API->>Trace: Store SQL, model version, catalog version, validation result
            API-->>UI: Return SQL + explanation + confidence
            UI-->>User: Show copyable SQL
        else SQL fails validation
            Validator-->>API: Validation failure
            API->>Trace: Log failure and reason
            API-->>UI: Return controlled refusal or repair request
            UI-->>User: Explain why SQL was not generated
        end
    end
```

## Runtime behavior

1. User submits a natural language request.
2. Backend authenticates session.
3. Request is traced.
4. Inference job enters queue.
5. Context selector identifies relevant report family and semantic subset.
6. Local LLM generates a structured intent candidate.
7. IR validator checks JSON schema and supported intent.
8. SQL compiler generates SQL from valid IR.
9. Scope engine injects required filters.
10. Validators check SQL safety, policy and scope.
11. The app returns either governed SQL or controlled refusal.
12. Trace/audit information is stored.

## Non-goals at runtime

- The product does not execute SQL.
- The product does not connect to production DB.
- The product does not call cloud LLM APIs.
- The product does not bypass AutoTime's external Report Writer.
