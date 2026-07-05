# Evals

This directory will hold the golden dataset, eval runners and generated eval reports.

## Expected future structure

```text
evals/
├── golden-dataset/
├── runners/
├── reports/
└── fixtures/
```

## Evaluation objectives

The eval pipeline should measure:

- IR validity;
- SQL parse success;
- policy pass/fail;
- execution accuracy in engineering lab;
- scope correctness;
- abstention accuracy;
- latency p50/p95;
- failure taxonomy.

## Product/runtime distinction

The engineering lab may execute SQL against the AutoTime demo DB for validation.

The delivered product runtime should not connect to the production database.
