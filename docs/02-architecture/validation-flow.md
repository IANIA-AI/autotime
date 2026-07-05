# SQL Generation and Validation Flow

This document describes the decision logic for safe SQL generation, validation, blocking and abstention.

```mermaid
flowchart TD
    START([User asks a report question])

    START --> AUTH{User authenticated?}
    AUTH -->|No| DENY_AUTH[Reject: authentication required]
    AUTH -->|Yes| FAMILY{Can request be mapped<br/>to supported report family?}

    FAMILY -->|No| ABSTAIN_FAMILY[Abstain: unsupported family]
    FAMILY -->|Yes| SCOPE_Q{Does request require<br/>managerial scope?}

    SCOPE_Q -->|Yes| SCOPE_KNOWN{Is required scope rule<br/>known and supported?}
    SCOPE_Q -->|No| CONTEXT[Select semantic context]

    SCOPE_KNOWN -->|No| ABSTAIN_SCOPE[Abstain: scope rule unavailable]
    SCOPE_KNOWN -->|Yes| CONTEXT

    CONTEXT --> LLM[Local LLM generates structured IR]
    LLM --> IR_VALID{IR valid against schema?}

    IR_VALID -->|No| REPAIR_IR{Retry allowed?}
    REPAIR_IR -->|Yes| LLM
    REPAIR_IR -->|No| ABSTAIN_IR[Abstain: invalid intent]

    IR_VALID -->|Yes| SEMANTIC{Entities, metrics, filters<br/>resolved in catalog?}
    SEMANTIC -->|No| ABSTAIN_SEM[Abstain: unresolved semantic mapping]
    SEMANTIC -->|Yes| COMPILE[Compile deterministic SQL]

    COMPILE --> SQL_PARSE{SQL parses correctly?}
    SQL_PARSE -->|No| REPAIR_SQL{Bounded repair allowed?}
    REPAIR_SQL -->|Yes| COMPILE
    REPAIR_SQL -->|No| ABSTAIN_SQL[Abstain: SQL compilation failed]

    SQL_PARSE -->|Yes| READONLY{Read-only SELECT only?}
    READONLY -->|No| BLOCK_DML[Block: DDL/DML not allowed]
    READONLY -->|Yes| JOINS{Only allowed tables<br/>and joins?}

    JOINS -->|No| BLOCK_JOIN[Block: table/join policy violation]
    JOINS -->|Yes| SCOPE_CHECK{Mandatory scope filters<br/>present when required?}

    SCOPE_CHECK -->|No| BLOCK_SCOPE[Block: missing scope policy]
    SCOPE_CHECK -->|Yes| OUTPUT[Return governed SQL<br/>with explanation and confidence]

    OUTPUT --> TRACE[Log trace + audit + metrics]
    ABSTAIN_FAMILY --> TRACE
    ABSTAIN_SCOPE --> TRACE
    ABSTAIN_IR --> TRACE
    ABSTAIN_SEM --> TRACE
    ABSTAIN_SQL --> TRACE
    BLOCK_DML --> TRACE
    BLOCK_JOIN --> TRACE
    BLOCK_SCOPE --> TRACE

    TRACE --> END([End])
    DENY_AUTH --> END
```

## Mandatory validation rules

The system must block or abstain when:

- user is unauthenticated;
- report family is unsupported;
- scoping rule is required but unavailable;
- structured intent is invalid;
- semantic mapping cannot be resolved;
- SQL compilation fails;
- SQL is not read-only;
- SQL contains DDL/DML;
- SQL references tables or joins outside the allowlist;
- mandatory scope filters are missing.

## Safe failure principle

A failed validator should not leak unsafe SQL to the user. The expected behavior is controlled refusal with a reason that is useful but does not reveal an unsafe candidate.
