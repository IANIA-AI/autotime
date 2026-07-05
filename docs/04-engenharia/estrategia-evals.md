# Estratégia de Evals

Evals fazem parte do engineering system, não são apenas QA final.

## O que avaliar

O projeto deve medir:

- IR schema validity;
- semantic resolution success;
- SQL parse success;
- policy pass/fail correctness;
- DDL/DML blocking;
- allowed table e join enforcement;
- scope correctness;
- execution accuracy no engineering lab;
- abstention accuracy;
- latency p50/p95;
- failure taxonomy.

## Golden dataset

A primeira entrega deve mirar 120 a 180 casos de alta qualidade cobrindo:

- perguntas Labor Charge simples e médias;
- perguntas Labor Charge complexas;
- perguntas Employee simples e médias;
- perguntas Employee complexas;
- casos intensivos em scope;
- negative e ambiguous cases;
- security e blocking cases;
- regression cases de existing reports.

## Engineering lab versus runtime

O engineering lab pode executar SQL contra um AutoTime demo DB para comparar expected result sets e generated result sets.

O delivered product runtime não deve conectar ao production database.

## Referência

Veja [../90-referencia/pipeline-evals.md](../90-referencia/pipeline-evals.md) para a arquitetura detalhada de evals.
