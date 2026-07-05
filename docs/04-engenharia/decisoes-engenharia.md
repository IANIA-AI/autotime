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
| Auth na versão de 8 semanas | Local auth + enterprise auth abstraction | Evita overbuild de LDAP/OIDC/SAML na Fase 1 |
| Windows support | Tiered support | Windows pode funcionar melhor com CPU/llama.cpp; Linux é melhor para GPU |
| Shortlist de model runtime | llama.cpp e vLLM primeiro | Cobre cross-platform CPU e Linux GPU |
| Packaging | Linux package primeiro, Windows best effort/limited tier | Protege o timeline de 8 semanas |

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
