# Visão Geral da Arquitetura

O produto deve se comportar como um assistente governado, apoiado por compiler, e não como um chatbot de free-form SQL.

## Fluxo principal

```text
Natural Language
  -> Structured Intent / IR
  -> Semantic Resolution
  -> Deterministic SQL Compiler
  -> Scope Engine
  -> SQL Validators
  -> Governed SQL Output
```

## Componentes principais

| Camada | Componentes | Responsabilidade |
|---|---|---|
| Application | Web UI, Backend API, Auth, History, Queue | Workflow do usuário, acesso, request tracking e concurrency. |
| Generation Core | Context selector, local LLM, IR validator, compiler, scope engine, validators | Converte pedidos suportados em governed SQL ou controlled refusal. |
| Knowledge Layer | Schema metadata, examples, glossary, allowed joins, scope rules, semantic catalog | Dá significado controlado a business terms e à geração de SQL. |
| Observability and Evals | Trace store, audit log, feedback, eval harness, golden dataset, metrics | Torna qualidade mensurável e regressões visíveis. |
| Deployment Kit | Local model weights, config, smoke tests, install/admin docs | Viabiliza instalação on-premise customer-controlled. |

## Comportamento simplificado de request

1. O usuário faz uma pergunta de relatório.
2. O backend autentica e registra trace do request.
3. O context selector escolhe a report family e o semantic subset.
4. O local LLM gera structured intent.
5. O IR validator aceita ou rejeita o intent.
6. O compiler produz SQL a partir de semantic bindings resolvidos.
7. O scope engine injeta filters obrigatórios.
8. Validators checam safety, policy e scope.
9. O produto retorna governed SQL ou controlled refusal.

## Referências detalhadas

- [Runtime Flow](fluxo-runtime.md)
- [Validation Flow](fluxo-validacao.md)
- [Arquitetura Detalhada](../90-referencia/arquitetura-detalhada.md)
- Mermaid bruto: [../../diagrams/solution-architecture.mmd](../../diagrams/solution-architecture.mmd)
