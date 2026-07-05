# Alocação do Time

## Alocação conceitual

O plano de 10 semanas adota uma distribuição simétrica por ownership, com quatro trilhas de responsabilidade equivalentes.

A simetria está no ownership e na responsabilidade de entrega, não necessariamente na natureza das tarefas ou em uma divisão rígida de horas.

| Pessoa | Trilha | Papel |
|---|---|---|
| Erlon Rachi | Client, QA, UAT, Evidence | Garante insumos, validações, riscos, aceite e evidências |
| José Marcos Ferreira | Data, SQL, Catalog, Compiler | Garante correção técnica do schema, SQL, catalog e scoping |
| Persival Ballesté | AI Architecture, IR, Runtime, Guardrails | Garante arquitetura, governança do LLM, eval strategy e quality gates |
| Fábio Sarmento | Platform, App, Deployment, Observability | Garante produto executável, instalável, observável e testável |

## Distribuição por ownership

| Bloco | Owner | Peso conceitual |
|---|---|---:|
| Client, QA, UAT, Evidence | Erlon | 25% |
| Data, SQL, Catalog, Compiler | Marcos | 25% |
| AI Architecture, IR, Runtime, Guardrails | Persival | 25% |
| Platform, App, Deployment, Observability | Fábio | 25% |

## Responsabilidades por pessoa

### Erlon Rachi

Erlon lidera client delivery, relacionamento com AutoTime, agenda com Cole, Harold e SMEs, controle de insumos, source inventory, matriz de rastreabilidade, decision log, risk log, operação do golden dataset, UAT script, QA funcional, issue triage, evidence pack, release notes e handover.

### José Marcos Ferreira

Marcos lidera data/SQL engineering, apoio no restore e inspeção do demo DB, schema analysis, table/field mapping, join mapping, SQL esperado, semantic catalog técnico, SQL compiler, scope SQL logic, validators SQL junto com Persival e execução técnica dos evals.

### Persival Ballesté

Persival lidera AI architecture e technical quality, incluindo arquitetura da solução, IR schema, intent taxonomy, eval strategy, model/runtime benchmark, prompt/structured output, guardrails, abstention logic, quality gates, architecture decision records e technical go/no-go.

### Fábio Sarmento

Fábio lidera platform, fullstack e deployment, incluindo engineering lab, ambientes, backend API, frontend/UI, auth local, fila de inferência, integração com runtime LLM, observability, packaging, smoke tests técnicos e deployment kit.

## Estimativa a detalhar

O plano atual evita cravar carga horária rígida como premissa central. A estimativa de horas deve ser detalhada depois que o source inventory, o runtime decision e a disponibilidade de SMEs estiverem mais claros.
