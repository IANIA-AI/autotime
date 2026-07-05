# Eval Strategy

Evals are part of the engineering system, not final QA.

## What to evaluate

The project should measure:

- IR schema validity;
- semantic resolution success;
- SQL parse success;
- policy pass/fail correctness;
- DDL/DML blocking;
- allowed table and join enforcement;
- scope correctness;
- execution accuracy in the engineering lab;
- abstention accuracy;
- latency p50/p95;
- failure taxonomy.

## Golden dataset

The first delivery should target 120 to 180 high-quality cases across:

- Labor Charge simple and medium questions;
- Labor Charge complex questions;
- Employee simple and medium questions;
- Employee complex questions;
- scope-heavy cases;
- negative and ambiguous cases;
- security and blocking cases;
- regression cases from existing reports.

## Engineering lab versus runtime

The engineering lab may execute SQL against an AutoTime demo DB to compare expected and generated result sets.

The delivered product runtime should not connect to the production database.

## Reference

See [../90-reference/eval-pipeline.md](../90-reference/eval-pipeline.md) for the detailed eval architecture.
