# Contexto do Projeto

## Resumo em uma linha

O AutoTime precisa de um assistente governado, on-premise, de natural-language-to-SQL que ajude report writers a gerar SQL válido para o AutoTime external Report Writer sem conectar ao production database e sem usar cloud LLM APIs.

## Conceito do produto

O produto é uma aplicação standalone instalada por cada cliente AutoTime no seu próprio ambiente. Ele recebe uma pergunta de negócio em linguagem natural, interpreta localmente, mapeia para report families suportadas do AutoTime, compila governed SQL e retorna SQL copiável para execução fora do produto.

## Restrições confirmadas

- Cada cliente terá sua própria instalação.
- O cliente instala o produto no seu próprio hardware ou VM.
- O runtime deve ser on-premise / customer-controlled.
- Sem cloud LLM API.
- Sem dependência externa para geração.
- O produto não executa SQL em produção.
- O produto não conecta ao production database em runtime.
- O SQL é copiado e depois executado no AutoTime external Report Writer.
- O suporte inicial deve focar nas report families Labor Charge e Employee.
- O produto deve suportar múltiplos usuários emitindo inference requests.
- Candidate scale tiers: até 10, até 20 e até 30 usuários concorrentes.
- Existem clientes Windows e Linux, mas Linux pode ser justificado como tier de produção recomendado para GPU serving.
- Windows support pode ser oferecido em um CPU-compatible tier se modern GPU serving não se encaixar nativamente em Windows.

## Distinção do engineering lab

Embora o produto não deva conectar ao production database em runtime, o projeto de engenharia precisa de um lab environment com:

- AutoTime demo DB;
- schema metadata;
- example queries;
- report examples;
- golden dataset;
- eval harness;
- execução controlada de expected SQL versus generated SQL.

Essa distinção é crítica:

| Ambiente | Conexão com DB? | Propósito |
|---|---:|---|
| Engineering lab | Sim | Validar SQL, criar evals, comparar result sets |
| Delivered product runtime | Não | Gerar governed SQL offline para copy/paste |

## Principal risco

O principal risco técnico não é apenas sintaxe SQL. É semântica de business scope e authorization, especialmente expressões como:

- my employees;
- my facility;
- my department;
- my team;
- employees under my management hierarchy.

O produto não deve fingir que entende uma scope rule se não consegue aplicá-la de forma determinística.

## Resultado alvo

A Fase 1 deve entregar um Working Product with engineering evidence:

- app standalone;
- local LLM runtime;
- semantic catalog;
- structured IR;
- deterministic SQL compiler;
- scope engine;
- validators;
- eval harness;
- golden dataset;
- deployment kit;
- UAT report;
- release candidate recommendation.
