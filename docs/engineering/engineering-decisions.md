# Engineering Decisions

This document tracks proposed and open engineering decisions.

## Proposed decisions

| Decision | Recommended direction | Rationale |
|---|---|---|
| SQL generation strategy | IR + deterministic compiler | Reduces risk of free-form SQL from LLM |
| Runtime DB connection | No runtime DB connection | Product only generates SQL for copy/paste |
| Engineering lab DB | Yes, demo DB only | Required for evals and execution accuracy |
| Initial report families | Labor Charge and Employee | Controlled Phase 1 scope |
| Eval strategy | Golden dataset + execution comparison + safety cases | Makes quality measurable |
| Auth in 8-week version | Local auth + enterprise auth abstraction | Avoids overbuilding LDAP/OIDC/SAML in Phase 1 |
| Windows support | Tiered support | Windows may work better with CPU/llama.cpp; Linux better for GPU |
| Model runtime shortlist | llama.cpp and vLLM first | Covers cross-platform CPU and Linux GPU paths |
| Packaging | Linux package first, Windows best effort/limited tier | Protects the 8-week timeline |

## Decisions still open

| Decision | Options | Owner | When needed |
|---|---|---|---|
| Final local model | Qwen Coder, Qwen Instruct, SQL-oriented model | Persival | Week 4 |
| Final runtime for Tier A | llama.cpp or equivalent | Persival/Fabio | Week 4 |
| Final runtime for Tier B/C | vLLM/SGLang/equivalent | Persival/Fabio | Week 4 |
| SQL parser/validator library | SQLGlot, SQLFluff, custom AST rules | Marcos/Persival | Week 4 |
| Auth approach | local only, LDAP stub, OIDC stub | Fabio | Week 5 |
| Packaging approach | native, container, service installer | Fabio | Week 6 |
| UAT case set | 20-30 real cases plus safety cases | Erlon/Cole/SME | Week 7 |
