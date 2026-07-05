# Smoke Tests

Smoke tests should validate that an installed package works in a clean environment.

## Minimum smoke tests

- app starts;
- local model runtime starts;
- semantic catalog loads;
- health endpoint returns OK;
- sample prompt generates valid IR;
- compiler generates SQL;
- validators pass safe SQL;
- validators block DDL/DML;
- audit log is written;
- package version is visible.
