# Evaluation Pipeline

This document describes the evaluation architecture for golden dataset, SQL correctness, policy validation and release gates.

```mermaid
flowchart LR
    subgraph INPUTS["Evaluation Inputs"]
        Q[User Questions]
        EXPECTED_SQL[Expected SQL]
        EXPECTED_RESULT[Expected Result Sets]
        NEG[Negative / Ambiguous Cases]
        SEC[Security Cases]
        SME[SME Labels]
    end

    subgraph GOLD["Golden Dataset"]
        CASES[Test Cases]
        META[Metadata<br/>family / complexity / scope / expected behavior]
        THRESH[Acceptance Thresholds]
    end

    subgraph SUT["System Under Test"]
        APP[Standalone App]
        LLM[Local LLM Runtime]
        COMP[SQL Compiler]
        VAL[Validators]
    end

    subgraph LAB["Engineering Lab Only"]
        DEMODB[AutoTime Demo DB]
        RUNNER[Eval Runner]
        COMPARE[Result Comparator]
    end

    subgraph METRICS["Metrics and Reports"]
        IR_ACC[IR Validity]
        SQL_PARSE[SQL Parse Pass]
        POLICY[Policy Pass Rate]
        EXEC_ACC[Execution Accuracy]
        SCOPE_ACC[Scope Correctness]
        ABSTAIN[Abstention Accuracy]
        LAT[Latency p50/p95]
        FAIL[Failure Taxonomy]
        REPORT[Eval Report]
    end

    Q --> CASES
    EXPECTED_SQL --> CASES
    EXPECTED_RESULT --> CASES
    NEG --> CASES
    SEC --> CASES
    SME --> CASES
    META --> CASES
    THRESH --> CASES

    CASES --> RUNNER
    RUNNER --> APP
    APP --> LLM
    APP --> COMP
    APP --> VAL
    APP --> RUNNER

    RUNNER --> DEMODB
    RUNNER --> COMPARE
    DEMODB --> COMPARE
    EXPECTED_RESULT --> COMPARE

    COMPARE --> IR_ACC
    COMPARE --> SQL_PARSE
    COMPARE --> POLICY
    COMPARE --> EXEC_ACC
    COMPARE --> SCOPE_ACC
    COMPARE --> ABSTAIN
    COMPARE --> LAT
    COMPARE --> FAIL

    IR_ACC --> REPORT
    SQL_PARSE --> REPORT
    POLICY --> REPORT
    EXEC_ACC --> REPORT
    SCOPE_ACC --> REPORT
    ABSTAIN --> REPORT
    LAT --> REPORT
    FAIL --> REPORT

    REPORT --> GATE{Release Gate}
    GATE -->|Pass| RC[Release Candidate]
    GATE -->|Fail| FIX[Fix / Improve / Re-run]
    FIX --> RUNNER
```

## Why evals are central

Evals should not be treated as final QA. They are part of the engineering system.

The project should use evaluation to measure:

- whether the LLM generated a valid structured intent;
- whether the compiler generated valid SQL;
- whether the SQL respected scope and policy rules;
- whether expected and generated SQL return equivalent results in the engineering lab;
- whether the system abstains when it should;
- whether performance remains acceptable under concurrent use.

## Initial golden dataset size

For the 8-week version, target 120 to 180 high-quality cases.

Suggested distribution:

| Case type | Suggested count |
|---|---:|
| Labor Charge simple/medium | 35 |
| Labor Charge complex | 15 |
| Employee simple/medium | 35 |
| Employee complex | 15 |
| Scoping / my X cases | 25 |
| Negative / ambiguous cases | 20 |
| Security / blocking cases | 15 |
| Regression cases from existing reports | 20 |

Approximate total: 160 cases.

## Initial metrics

| Metric | Initial target |
|---|---:|
| IR JSON validity | >= 98% |
| SQL parse pass | >= 95% |
| Policy pass correctness | >= 98% |
| DDL/DML blocking | 100% |
| Abstention accuracy | >= 90% |
| Execution accuracy | 80-85% initial; target 90%+ |
| Scope correctness | >= 90% initial; target 95%+ |
| Install smoke test | 100% on supported tier |

## Lab-only DB execution

The engineering lab may execute SQL against the AutoTime demo DB to compare expected and generated result sets. This is different from product runtime, where the application should not connect to the database.
