# Evals

Este diretório irá conter o golden dataset, eval runners e generated eval reports.

## Estrutura futura esperada

```text
evals/
├── golden-dataset/
├── runners/
├── reports/
└── fixtures/
```

## Objetivos de evaluation

O eval pipeline deve medir:

- IR validity;
- SQL parse success;
- policy pass/fail;
- execution accuracy no engineering lab;
- scope correctness;
- abstention accuracy;
- latency p50/p95;
- failure taxonomy.

## Distinção produto/runtime

O engineering lab pode executar SQL contra o AutoTime demo DB para validation.

O delivered product runtime não deve conectar ao production database.
