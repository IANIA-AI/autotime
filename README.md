# AutoTime Governed SQL Writer

Este repositório contém o blueprint técnico do **AutoTime Governed SQL Writer**: uma aplicação on-premise, com local LLM, para ajudar report writers do AutoTime a gerar SQL governado a partir de linguagem natural.

O repositório está organizado para onboarding primeiro e referência detalhada depois.

## Comece aqui

Novos integrantes do time devem ler:

1. [ONBOARDING.md](ONBOARDING.md)
2. [Resumo Executivo](docs/00-comece-aqui/resumo-executivo.md)
3. [Trilha de Leitura](docs/00-comece-aqui/trilha-de-leitura.md)
4. [Fronteiras do Produto](docs/01-contexto-produto/fronteiras-produto.md)
5. [Escopo da Fase 1](docs/01-contexto-produto/escopo-fase-1.md)
6. [Visão Geral da Arquitetura](docs/02-arquitetura/visao-geral.md)
7. [Plano de 8 Semanas](docs/03-entrega/plano-8-semanas.md)

## Projeto em um parágrafo

O AutoTime precisa de um assistente governado de natural-language-to-SQL para o seu external Report Writer. O produto roda localmente no ambiente do cliente, usa um local model runtime, mapeia pedidos para um semantic catalog controlado, gera structured intent, compila SQL de forma determinística, aplica scope e policy rules, valida a saída e entrega SQL copiável ao usuário.

## Fronteiras inegociáveis

O produto não:

- executa SQL em produção;
- conecta ao production database em runtime;
- chama cloud LLM APIs;
- substitui autorização ou runtime security do AutoTime;
- confia em free-form SQL gerado diretamente por um LLM.

O caminho preferencial é:

```text
Natural Language
  -> Structured Intent / IR
  -> Semantic Resolution
  -> Deterministic SQL Compiler
  -> Scope Engine
  -> SQL Validators
  -> Governed SQL Output
```

## Organização da documentação

| Área | Propósito |
|---|---|
| [docs/00-comece-aqui](docs/00-comece-aqui/) | Entrada executiva e trilha de leitura. |
| [docs/01-contexto-produto](docs/01-contexto-produto/) | Contexto do produto, fronteiras e escopo da Fase 1. |
| [docs/02-arquitetura](docs/02-arquitetura/) | Arquitetura simplificada, runtime flow e validation flow. |
| [docs/03-entrega](docs/03-entrega/) | Plano de entrega, alocação do time, critérios de release e perguntas abertas. |
| [docs/04-engenharia](docs/04-engenharia/) | Decisões ativas de engenharia e eval strategy. |
| [docs/90-referencia](docs/90-referencia/) | Referência detalhada de arquitetura, deployment e evals. |
| [docs/99-arquivo](docs/99-arquivo/) | Research notes e material histórico. |
| [diagrams](diagrams/) | Arquivos Mermaid brutos. |
| [semantic-catalog](semantic-catalog/) | Futuros assets do semantic catalog. |
| [evals](evals/) | Futuro golden dataset, eval runners e reports. |
| [deployment](deployment/) | Futuros assets de instalação, packaging e smoke tests. |

## Situação atual do projeto

Este é um repositório de blueprint técnico, ainda não um repositório de implementação.

O primeiro alvo de entrega proposto é um **Working Product with engineering evidence**, focado nas famílias Labor Charge e Employee, execução local de modelo, geração governada de SQL, evals, smoke tests e UAT.
