# SQL Generation e Validation Flow

Este documento descreve a lógica de decisão para geração segura de SQL, validation, blocking e abstention.

```mermaid
flowchart TD
    START([Usuário faz uma pergunta de relatório])

    START --> AUTH{Usuário autenticado?}
    AUTH -->|Não| DENY_AUTH[Rejeitar: autenticação obrigatória]
    AUTH -->|Sim| FAMILY{Request mapeia para<br/>report family suportada?}

    FAMILY -->|Não| ABSTAIN_FAMILY[Abstain: family não suportada]
    FAMILY -->|Sim| SCOPE_Q{Request exige<br/>managerial scope?}

    SCOPE_Q -->|Sim| SCOPE_KNOWN{Scope rule exigida<br/>é conhecida e suportada?}
    SCOPE_Q -->|Não| CONTEXT[Selecionar semantic context]

    SCOPE_KNOWN -->|Não| ABSTAIN_SCOPE[Abstain: scope rule indisponível]
    SCOPE_KNOWN -->|Sim| CONTEXT

    CONTEXT --> LLM[Local LLM gera structured IR]
    LLM --> IR_VALID{IR válido contra schema?}

    IR_VALID -->|Não| REPAIR_IR{Retry permitido?}
    REPAIR_IR -->|Sim| LLM
    REPAIR_IR -->|Não| ABSTAIN_IR[Abstain: intent inválido]

    IR_VALID -->|Sim| SEMANTIC{Entities, metrics e filters<br/>resolvidos no catalog?}
    SEMANTIC -->|Não| ABSTAIN_SEM[Abstain: semantic mapping não resolvido]
    SEMANTIC -->|Sim| COMPILE[Compilar SQL determinístico]

    COMPILE --> SQL_PARSE{SQL parseia corretamente?}
    SQL_PARSE -->|Não| REPAIR_SQL{Bounded repair permitido?}
    REPAIR_SQL -->|Sim| COMPILE
    REPAIR_SQL -->|Não| ABSTAIN_SQL[Abstain: SQL compilation falhou]

    SQL_PARSE -->|Sim| READONLY{Somente read-only SELECT?}
    READONLY -->|Não| BLOCK_DML[Block: DDL/DML não permitido]
    READONLY -->|Sim| JOINS{Somente tables e joins<br/>permitidos?}

    JOINS -->|Não| BLOCK_JOIN[Block: violação de table/join policy]
    JOINS -->|Sim| SCOPE_CHECK{Mandatory scope filters<br/>presentes quando exigidos?}

    SCOPE_CHECK -->|Não| BLOCK_SCOPE[Block: scope policy ausente]
    SCOPE_CHECK -->|Sim| OUTPUT[Retornar governed SQL<br/>com explicação e confidence]

    OUTPUT --> TRACE[Registrar trace + audit + metrics]
    ABSTAIN_FAMILY --> TRACE
    ABSTAIN_SCOPE --> TRACE
    ABSTAIN_IR --> TRACE
    ABSTAIN_SEM --> TRACE
    ABSTAIN_SQL --> TRACE
    BLOCK_DML --> TRACE
    BLOCK_JOIN --> TRACE
    BLOCK_SCOPE --> TRACE

    TRACE --> END([Fim])
    DENY_AUTH --> END
```

## Regras obrigatórias de validation

O sistema deve bloquear ou abster quando:

- usuário não estiver autenticado;
- report family não for suportada;
- scope rule for exigida, mas estiver indisponível;
- structured intent for inválido;
- semantic mapping não puder ser resolvido;
- SQL compilation falhar;
- SQL não for read-only;
- SQL contiver DDL/DML;
- SQL referenciar tables ou joins fora da allowlist;
- mandatory scope filters estiverem ausentes.

## Princípio de safe failure

Um validator com falha não deve vazar SQL inseguro para o usuário. O comportamento esperado é controlled refusal com um motivo útil, mas sem revelar um unsafe candidate.
