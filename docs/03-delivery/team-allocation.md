# Team Allocation

## Proposed 4-person delivery model

| Person | Primary role | Secondary role | Allocation |
|---|---|---|---:|
| Erlon Rachi | Project/Delivery Manager | QA, validation, metrics, risk control | ~40% |
| José Marcos Ferreira | Data/SQL/AI Engineer | Semantic catalog, compiler, evals | ~90% |
| Persival Ballesté | AI Architect / Tech Lead | Runtime decision, prompts, guardrails, eval strategy | ~70% |
| Fábio Sarmento | Platform / Fullstack / DevOps / Security | App, packaging, auth, observability | ~90% |

## Estimated effort

Assuming 8 weeks and 40 business days:

| Person | Total hours | Average per business day |
|---|---:|---:|
| Erlon Rachi | 128h | 3.2h/day |
| José Marcos Ferreira | 288h | 7.2h/day |
| Persival Ballesté | 224h | 5.6h/day |
| Fábio Sarmento | 288h | 7.2h/day |

Total estimated effort: **928h**  
Recommended contingency: **1,000-1,050h**

## Practical interpretation

- Erlon: 3 to 4 hours/day.
- Marcos: 7 to 8 hours/day.
- Persival: 5 to 6 hours/day.
- Fabio: 7 to 8 hours/day.

## Role consolidation rationale

The compressed model works because the team combines senior multi-disciplinary profiles:

- Erlon covers project control, acceptance, QA validation and risk.
- Marcos covers data, SQL, schema engineering, semantic catalog and evals.
- Persival covers AI architecture, runtime strategy, prompt/IR/guardrail design and technical leadership.
- Fabio covers fullstack implementation, platform, DevOps, packaging, auth and observability.

## Key risk

The compressed model creates bottlenecks. The biggest bottlenecks are likely to be:

- Marcos on semantic catalog + SQL compiler + evals.
- Fabio on app + packaging + platform + security.
- Persival on architecture + LLM + quality gates.
- Erlon if UAT, metrics and client coordination are underestimated.
