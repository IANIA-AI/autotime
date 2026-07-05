# Semantic Catalog

Este diretório irá conter o semantic catalog versionado usado pelo governed SQL generation core.

## Arquivos futuros esperados

```text
semantic-catalog/
├── catalog.yaml
├── glossary.yaml
├── joins.yaml
├── scope-rules.yaml
├── report-families.yaml
└── versions/
```

## Propósito

O semantic catalog mapeia AutoTime schema metadata, report families, business terms, allowed joins, filters, metrics, dimensions e scope rules para uma representação controlada consumida pelo compiler.

## Foco da Fase 1

- Labor Charge.
- Employee.
- Scoping rules iniciais.
- Supported metrics.
- Supported dimensions.
- Allowed joins.
- Known abstention conditions.
