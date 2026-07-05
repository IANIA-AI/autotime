# Arquitetura Detalhada da Solução

Este documento de referência descreve a arquitetura lógica do produto standalone on-premise de governed SQL generation.

Para onboarding, comece por [../02-arquitetura/visao-geral.md](../02-arquitetura/visao-geral.md).

```mermaid
flowchart TB
    U[Report Writer / Business User]

    subgraph APP["Aplicação Standalone On-Prem"]
        UI[Web UI]
        API[Backend API]
        AUTH[Auth Module<br/>Usuários Locais<br/>LDAP/OIDC Stub]
        SESSION[Session Manager]
        QUEUE[Inference Queue<br/>Concurrency Control]
        HISTORY[Request History]
    end

    subgraph CORE["Governed SQL Generation Core"]
        CTX[Context Selector<br/>Report Family + Semantic Context]
        LLM[Local LLM Runtime<br/>llama.cpp / vLLM]
        IR[Structured IR Generator<br/>NL to JSON Intent]
        SEM[Semantic Catalog Resolver]
        COMP[Deterministic SQL Compiler<br/>IR to T-SQL]
        SCOPE[Scope Engine<br/>my employees / my facility / etc.]
        VAL[SQL Validators<br/>Read-only / AST / Policy / Scope]
        ABSTAIN[Abstention Engine]
    end

    subgraph KNOW["Knowledge Layer Versionado"]
        SCHEMA[Schema Metadata<br/>schema.xml / table ref]
        EXAMPLES[Example Queries + Reports]
        GLOSSARY[Business Glossary]
        JOINS[Allowed Joins]
        RULES[Scope + Policy Rules]
        CATALOG[Semantic Catalog Pack]
    end

    subgraph OBS["Observability, Audit e Evals"]
        TRACE[Trace Store]
        AUDIT[Audit Log]
        FEEDBACK[User Feedback<br/>Accepted / Rejected / Edited]
        EVALS[Eval Harness]
        GOLDEN[Golden Dataset]
        METRICS[Metrics Dashboard]
    end

    subgraph DEPLOY["Offline Deployment Kit"]
        BUNDLE[Air-Gapped Bundle]
        MODEL[Local Model Weights]
        CONFIG[Config Files]
        SMOKE[Smoke Tests]
        DOCS[Install + Admin Docs]
    end

    U --> UI
    UI --> API
    API --> AUTH
    API --> SESSION
    API --> HISTORY
    API --> QUEUE
    QUEUE --> CTX

    CTX --> CATALOG
    CATALOG --> SCHEMA
    CATALOG --> EXAMPLES
    CATALOG --> GLOSSARY
    CATALOG --> JOINS
    CATALOG --> RULES

    CTX --> LLM
    LLM --> IR
    IR --> SEM
    SEM --> COMP
    COMP --> SCOPE
    SCOPE --> VAL

    VAL -->|Pass| API
    VAL -->|Fail| ABSTAIN
    ABSTAIN --> API

    API --> UI
    UI --> U

    API --> TRACE
    API --> AUDIT
    UI --> FEEDBACK
    FEEDBACK --> EVALS
    GOLDEN --> EVALS
    TRACE --> EVALS
    EVALS --> METRICS

    BUNDLE --> APP
    MODEL --> LLM
    CONFIG --> APP
    SMOKE --> APP
    DOCS --> APP
```

## Camadas arquiteturais

### 1. User/Application Layer

- Web UI
- Backend API
- Auth module
- Session manager
- Request history
- Inference queue

### 2. Governed SQL Generation Core

- Context selector
- Local LLM runtime
- Structured IR generator
- Semantic catalog resolver
- Deterministic SQL compiler
- Scope engine
- SQL validators
- Abstention engine

### 3. Versioned Knowledge Layer

- AutoTime schema metadata
- Example queries e reports
- Business glossary
- Allowed joins
- Scope e policy rules
- Semantic catalog pack

### 4. Observability e Evals

- Trace store
- Audit log
- User feedback
- Eval harness
- Golden dataset
- Metrics dashboard

### 5. Offline Deployment Kit

- Air-gapped bundle
- Local model weights
- Config files
- Smoke tests
- Install e admin docs

## Princípio de design

O LLM não deve produzir diretamente o SQL final como trusted output. O LLM deve produzir um structured intent candidate, e o SQL final deve ser gerado por um deterministic compiler após semantic resolution e scope enforcement.

## Por que isso importa

Essa arquitetura evita o failure mode de um chatbot que por acaso retorna SQL. O produto deve se comportar como um assistente governado, compiler-backed, com explicit refusal sempre que o pedido estiver fora do supported semantic envelope.
