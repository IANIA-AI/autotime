# Runtime Flow

Este documento descreve o comportamento end-to-end em runtime quando um report writer faz uma pergunta em linguagem natural.

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

    User->>UI: Faz pergunta de relatório em linguagem natural
    UI->>API: Envia request
    API->>Auth: Valida sessão / usuário
    Auth-->>API: Autenticado

    API->>Trace: Cria trace do request
    API->>Queue: Enfileira inference job
    Queue->>Catalog: Seleciona contexto da report family
    Catalog-->>Queue: Schema subset + glossary + allowed joins + rules

    Queue->>LLM: Prompt com contexto restrito
    LLM-->>Queue: Structured intent candidate

    Queue->>IR: Valida JSON schema e intent suportado
    alt Intent inválido ou não suportado
        IR-->>API: Rejeita com motivo
        API->>Trace: Registra abstention
        API-->>UI: Retorna controlled refusal
        UI-->>User: Explica pedido não suportado
    else Intent válido
        IR-->>Compiler: IR válido
        Compiler->>Catalog: Resolve entidades, metrics e dimensions
        Catalog-->>Compiler: Semantic bindings resolvidos

        Compiler->>Scope: Gera SQL draft
        Scope->>Scope: Injeta scoping filters obrigatórios
        Scope-->>Validator: Scoped SQL candidate

        Validator->>Validator: Parse SQL / AST / read-only / policy / scope
        alt SQL passa em todos os validators
            Validator-->>API: Governed SQL aprovado
            API->>Trace: Armazena SQL, model version, catalog version e validation result
            API-->>UI: Retorna SQL + explicação + confidence
            UI-->>User: Mostra SQL copiável
        else SQL falha na validation
            Validator-->>API: Validation failure
            API->>Trace: Registra falha e motivo
            API-->>UI: Retorna controlled refusal ou repair request
            UI-->>User: Explica por que o SQL não foi gerado
        end
    end
```

## Comportamento em runtime

1. O usuário envia um request em linguagem natural.
2. O backend autentica a sessão.
3. O request recebe trace.
4. O inference job entra na queue.
5. O context selector identifica a report family e o semantic subset relevantes.
6. O local LLM gera structured intent candidate.
7. O IR validator verifica JSON schema e intent suportado.
8. O SQL compiler gera SQL a partir de IR válido.
9. O scope engine injeta filters obrigatórios.
10. Validators checam SQL safety, policy e scope.
11. O app retorna governed SQL ou controlled refusal.
12. Trace/audit information é armazenada.

## Non-goals em runtime

- O produto não executa SQL.
- O produto não conecta ao production DB.
- O produto não chama cloud LLM APIs.
- O produto não contorna o AutoTime external Report Writer.
