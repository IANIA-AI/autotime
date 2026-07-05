# Semantic Catalog

This directory will hold the versioned semantic catalog used by the governed SQL generation core.

## Expected future files

```text
semantic-catalog/
├── catalog.yaml
├── glossary.yaml
├── joins.yaml
├── scope-rules.yaml
├── report-families.yaml
└── versions/
```

## Purpose

The semantic catalog maps AutoTime schema metadata, report families, business terms, allowed joins, filters, metrics, dimensions and scope rules into a controlled representation consumable by the compiler.

## Phase 1 focus

- Labor Charge.
- Employee.
- Initial scoping rules.
- Supported metrics.
- Supported dimensions.
- Allowed joins.
- Known abstention conditions.
