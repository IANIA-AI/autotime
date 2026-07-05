# Alocação do Time

## Modelo proposto de entrega com 4 pessoas

| Pessoa | Papel principal | Papel secundário | Alocação |
|---|---|---|---:|
| Erlon Rachi | Project/Delivery Manager | QA, validation, metrics, risk control | ~40% |
| José Marcos Ferreira | Data/SQL/AI Engineer | Semantic catalog, compiler, evals | ~90% |
| Persival Ballesté | AI Architect / Tech Lead | Runtime decision, prompts, guardrails, eval strategy | ~70% |
| Fábio Sarmento | Platform / Fullstack / DevOps / Security | App, packaging, auth, observability | ~90% |

## Esforço estimado

Assumindo 8 semanas e 40 dias úteis:

| Pessoa | Horas totais | Média por dia útil |
|---|---:|---:|
| Erlon Rachi | 128h | 3,2h/dia |
| José Marcos Ferreira | 288h | 7,2h/dia |
| Persival Ballesté | 224h | 5,6h/dia |
| Fábio Sarmento | 288h | 7,2h/dia |

Esforço total estimado: **928h**<br/>
Contingência recomendada: **1.000-1.050h**

## Interpretação prática

- Erlon: 3 a 4 horas/dia.
- Marcos: 7 a 8 horas/dia.
- Persival: 5 a 6 horas/dia.
- Fabio: 7 a 8 horas/dia.

## Racional de consolidação de papéis

O modelo comprimido funciona porque o time combina perfis senior multi-disciplinares:

- Erlon cobre project control, acceptance, QA validation e risk.
- Marcos cobre data, SQL, schema engineering, semantic catalog e evals.
- Persival cobre AI architecture, runtime strategy, prompt/IR/guardrail design e technical leadership.
- Fabio cobre fullstack implementation, platform, DevOps, packaging, auth e observability.

## Risco principal

O modelo comprimido cria gargalos. Os maiores gargalos tendem a ser:

- Marcos em semantic catalog + SQL compiler + evals.
- Fabio em app + packaging + platform + security.
- Persival em architecture + LLM + quality gates.
- Erlon se UAT, metrics e client coordination forem subestimados.
