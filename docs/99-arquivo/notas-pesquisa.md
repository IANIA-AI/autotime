# Notas de Pesquisa e Engenharia

## Conclusão principal

O projeto não deve ser desenhado como "colocar um local LLM na frente do schema". Ele deve ser desenhado como um governed engineering system:

```text
Lab + Golden Dataset + Semantic Catalog + IR + Compiler + Guardrails + Local Runtime + Packaging + UAT
```

## Realidade de enterprise Text-to-SQL

Enterprise Text-to-SQL continua difícil porque schemas reais são grandes, irregulares, versionados e semanticamente ambíguos. Acurácia depende fortemente de:

- schema representation;
- business glossary;
- join constraints;
- examples;
- scoping rules;
- evals;
- failure handling.

O produto deve, portanto, otimizar para controlled generation, não para autonomia irrestrita do modelo.

## Estratégia de evals

Evals devem ser uma disciplina, não uma única biblioteca.

O evaluation stack deve incluir:

1. Static SQL eval.
2. IR schema eval.
3. Execution eval no lab demo DB.
4. SME semantic eval.
5. Safety e abstention eval.

LLM-as-judge pode ajudar em classificação auxiliar, mas não deve ser a métrica primária de correctness para SQL.

## Estratégia de runtime

Shortlist para Fase 1:

- llama.cpp para perfil CPU/cross-platform.
- vLLM para perfil Linux GPU.

Outros runtimes como SGLang, TensorRT-LLM e TGI podem ser acompanhados, mas um benchmark amplo não deve fazer parte do critical path de 10 semanas.

## Estratégia Windows/Linux

O produto não deve prometer capacidade igual entre Windows e Linux antes do benchmark.

Posicionamento recomendado:

- Tier A: Windows/Linux CPU-compatible usando llama.cpp ou equivalente.
- Tier B/C: Linux GPU recomendado para maior concurrency.

## O que não cortar no plano de 10 semanas

Não cortar:

- engineering lab;
- golden dataset;
- semantic catalog;
- IR;
- SQL compiler;
- scope engine;
- validators;
- eval harness.

Cortes devem acontecer em:

- project ceremony;
- amplitude do benchmark;
- UX refinement;
- profundidade de enterprise auth;
- Windows hardening;
- polish de documentação;
- large-scale golden dataset.
