# Resumo Executivo

O AutoTime precisa de um assistente governado, on-premise, de natural-language-to-SQL para report writers.

O produto deve ajudar usuários a expressar perguntas de relatório em linguagem natural, gerar SQL governado localmente e retornar SQL copiável para uso no AutoTime external Report Writer.

## Ideia central

O sistema não deve confiar em um LLM para gerar o SQL final diretamente.

A arquitetura recomendada é:

```text
Natural Language
  -> Structured Intent / IR
  -> Semantic Resolution
  -> Deterministic SQL Compiler
  -> Scope Engine
  -> SQL Validators
  -> Governed SQL Output
```

## Por que isso importa

Enterprise Text-to-SQL é arriscado porque schemas são grandes, termos de negócio são ambíguos e authorization scope é específico do domínio. O projeto só fica defensável se a geração de SQL for governada por catalog, compiler, scope e eval assets explícitos.

## Alvo da Fase 1

A Fase 1 deve entregar um working product com engineering evidence:

- aplicação local standalone;
- local LLM runtime;
- report families Labor Charge e Employee;
- semantic catalog v1;
- structured IR;
- deterministic SQL compiler;
- scope engine;
- SQL validators;
- golden dataset e eval harness;
- deployment kit e smoke tests;
- UAT report e release recommendation.

## Principais riscos

- Business scope não suportado, como "my employees" ou "my facility".
- Golden dataset fraco ou baixa cobertura de validação por SME.
- Prometer Windows GPU support antes de benchmark.
- Tratar evals como QA final, e não como parte do engineering loop.
- Deixar o LLM virar o SQL author of record.
