# Decisões de Engenharia

Este documento acompanha decisões propostas e decisões abertas de engenharia.

## Decisões propostas

| Decisão | Direção recomendada | Racional |
|---|---|---|
| Estratégia de SQL generation | IR + deterministic compiler | Reduz risco de free-form SQL vindo do LLM |
| Runtime DB connection | Sem runtime DB connection | Produto apenas gera SQL para copy/paste |
| Engineering lab DB | Sim, apenas demo DB | Necessário para evals e execution accuracy |
| Report families iniciais | Labor Charge e Employee | Escopo controlado para Fase 1 |
| Eval strategy | Golden dataset + execution comparison + safety cases | Torna qualidade mensurável |
| Auth na primeira entrega | Local auth + enterprise auth abstraction | Evita overbuild de LDAP/OIDC/SAML na Fase 1 |
| Windows support | Tiered support | Windows pode funcionar melhor com CPU/llama.cpp; Linux é melhor para GPU |
| Shortlist de model runtime | llama.cpp e vLLM primeiro | Cobre cross-platform CPU e Linux GPU |
| Packaging | Linux package primeiro, Windows best effort/limited tier | Protege o timeline de 10 semanas |

## Decisões confirmadas (Annex v1.2)

| Decisão | Direção | Racional |
|---|---|---|
| Dialeto SQL alvo | T-SQL primeiro (SQL Server 2022 / Express 2022) | Baseline confirmado pelo AutoTime no Annex v1.2 |
| Suporte a Oracle | Depois, via dialect adapter no mesmo produto | Não é build paralelo; adapter sobre o mesmo compiler/IR |
| Timeline da Fase 1 | 10 semanas, com M3 "Pronto para Piloto" na S8 | Caminho crítico externo + dois ciclos de regressão (ver [Plano de 10 Semanas](../03-entrega/plano-10-semanas.md)) |
| Terminologia de fases | "Piloto", nunca "POC"; "POC-ready" → "Pronto para Piloto" | Fase 2 instala o produto real em ambiente controlado, não prova de conceito descartável (ver [Mapeamento Interno ↔ Cliente](../01-contexto-produto/mapeamento-cliente.md)) |

## Decisões ainda abertas

| Decisão | Opções | Owner | Quando necessário |
|---|---|---|---|
| Local model final | Qwen Coder, Qwen Instruct, modelo SQL-oriented | Persival | Semana 4 |
| Runtime final para Tier A | llama.cpp ou equivalente | Persival/Fabio | Semana 4 |
| Runtime final para Tier B/C | vLLM/SGLang/equivalente | Persival/Fabio | Semana 4 |
| SQL parser/validator library | SQLGlot, SQLFluff, custom AST rules | Marcos/Persival | Semana 4 |
| Auth approach | local only, LDAP stub, OIDC stub | Fabio | Semana 5 |
| Packaging approach | native, container, service installer | Fabio | Semana 6 |
| UAT case set | 20-30 casos reais mais safety cases | Erlon/Cole/SME | Semana 7 |
