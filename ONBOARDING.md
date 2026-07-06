# Onboarding do AutoTime Governed SQL Writer

Este documento é a trilha de onboarding para sponsors, delivery leads e engenheiros que entrarem no projeto AutoTime Governed SQL Writer.

> Nome externo (client-facing): **AutoTime Governed AI Report Writer**. Ver
> [Mapeamento Interno ↔ Cliente](docs/01-contexto-produto/mapeamento-cliente.md)
> antes de qualquer call, e-mail ou documento enviado ao AutoTime.

## Orientação de 10 minutos

O AutoTime quer um assistente local, customer-controlled, que transforme perguntas de report writers em SQL governado para o AutoTime external Report Writer.

O produto não é um chatbot que emite SQL. Ele é um sistema de geração governada:

```text
Natural Language -> IR -> Semantic Catalog -> SQL Compiler -> Scope Engine -> Validators -> Governed SQL
```

O LLM ajuda a interpretar o pedido, mas o SQL final precisa vir de semantic resolution controlada, compilação determinística, scope enforcement e validation.

## O que o produto faz

- Aceita perguntas de relatório em linguagem natural.
- Usa local model inference dentro do ambiente do cliente.
- Mapeia o pedido para report families suportadas do AutoTime.
- Gera structured intent.
- Resolve campos, joins, metrics e filters por meio de um semantic catalog.
- Produz SQL copiável para o AutoTime external Report Writer.
- Registra trace, audit e validation information.

## O que o produto não faz

- Não executa SQL em produção.
- Não conecta ao production database em runtime.
- Não chama cloud LLM APIs.
- Não contorna permissões do AutoTime nem controles do Report Writer.
- Não promete SQL válido para report families não suportadas ou scope rules desconhecidas.

## Leia nesta ordem

| Passo | Documento | Por que importa |
|---:|---|---|
| 1 | [Resumo Executivo](docs/00-comece-aqui/resumo-executivo.md) | Alinha o entendimento do projeto. |
| 2 | [Fronteiras do Produto](docs/01-contexto-produto/fronteiras-produto.md) | Define regras que a implementação não pode violar. |
| 3 | [Escopo da Fase 1](docs/01-contexto-produto/escopo-fase-1.md) | Mostra o que entra e o que fica fora da primeira entrega. |
| 4 | [Visão Geral da Arquitetura](docs/02-arquitetura/visao-geral.md) | Explica o modelo simplificado do sistema. |
| 5 | [Runtime Flow](docs/02-arquitetura/fluxo-runtime.md) | Mostra o que acontece quando o usuário faz uma pergunta. |
| 6 | [Validation Flow](docs/02-arquitetura/fluxo-validacao.md) | Explica como o sistema bloqueia, abstém ou retorna SQL. |
| 7 | [Plano de 10 Semanas](docs/03-entrega/plano-10-semanas.md) | Mostra a sequência de trabalho, milestones, paralelização e release path. |
| 8 | [Perguntas Abertas](docs/03-entrega/perguntas-abertas.md) | Lista decisões que dependem do AutoTime ou de SMEs. |
| 9 | [Mapeamento Interno ↔ Cliente](docs/01-contexto-produto/mapeamento-cliente.md) | Vocabulário a usar (e a evitar) com o AutoTime. |

## Foco da primeira semana

A primeira semana deve produzir clareza e fundações operacionais, não UX polida.

Resultados esperados da primeira semana:

- engineering lab definido;
- AutoTime demo DB e schema artifacts identificados;
- report examples coletados;
- Phase 1 report families confirmadas;
- formato do semantic catalog rascunhado;
- formato dos casos do golden dataset rascunhado;
- runtime benchmark plan acordado;
- principais perguntas abertas atribuídas a owners.

## Responsabilidades do time

| Papel | Foco principal |
|---|---|
| Erlon — Client Delivery / QA / UAT / Evidence | Insumos, validações, riscos, aceite, evidence pack e UAT. |
| Marcos — Data / SQL / Catalog / Compiler | Schema, SQL esperado, semantic catalog técnico, compiler e scoping SQL. |
| Persival — AI Architecture / IR / Runtime / Guardrails | Arquitetura, governança do LLM, eval strategy e quality gates. |
| Fábio — Platform / App / Deployment / Observability | Produto executável, instalável, observável e testável. |

Veja [Alocação do Time](docs/03-entrega/alocacao-time.md) para a proposta de alocação nominal.

## Riscos críticos

- Semânticas de business scope como "my employees" ou "my facility" podem ser mais difíceis que a sintaxe SQL.
- O semantic catalog e o golden dataset são engineering assets de primeira classe, não extras de documentação.
- Windows support é uma decisão de product tier e não deve ser prometido como equivalente a Linux GPU serving antes do benchmark.
- Um release candidate sem eval evidence não deve ser considerado pronto.

## Referência detalhada

Depois da trilha de onboarding, use:

- [Arquitetura Detalhada](docs/90-referencia/arquitetura-detalhada.md)
- [Pipeline de Evals](docs/90-referencia/pipeline-evals.md)
- [Topologias de Deployment](docs/90-referencia/topologias-deployment.md)
- [Notas de Pesquisa](docs/99-arquivo/notas-pesquisa.md)
