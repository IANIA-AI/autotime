# Report Families — Taxonomia e Roadmap

Este documento registra a taxonomia completa de report families discutida com
o Cole (AutoTime), conforme o Annex v1.2. A Fase 1 do projeto permanece restrita
a **Labor Charge** e **Employee** — as demais famílias são roadmap de fases
futuras e estão listadas aqui para dar ao time visão de para onde o semantic
catalog e o SQL compiler crescem.

## Por que isso importa agora

O semantic catalog, o structured IR e o SQL compiler construídos na Fase 1 para
Labor Charge e Employee são desenhados para serem reutilizáveis pelas famílias
seguintes — não uma reescrita por família. Entender o roadmap completo ajuda a
tomar decisões de design que não travam a extensão futura (ex.: nomenclatura de
entidades no catalog, estrutura do IR, granularidade das scope rules).

## Tiers

- **T1:** famílias determinísticas / high-assurance, com counterparts diretos
  em relatórios existentes do AutoTime e melhor fit para validação por SQL.
- **T2:** famílias analíticas ou prospectivas, com maior abstração de negócio
  e roadmap posterior à estabilização do core.

## Famílias por wave

| Wave | Report family | Tier | Fase |
|---|---|---|---|
| Wave 1 | Accrual Reporting | T2 | Roadmap |
| Wave 1 | Labor Charge Reporting | T1 | **Fase 1 (em andamento)** |
| Wave 1 | Overtime Reporting | T1 | Roadmap próximo a Labor Charge |
| Wave 1 | Employee Reporting | T1 | **Fase 1 (em andamento)** |
| Wave 1 | Signature Reporting | T1 | Roadmap |
| Wave 1 | Reconciliation Reporting | T2 | Roadmap |
| Wave 2 | Scheduling & Forecasting | T2 | Roadmap avançado |
| Wave 2 | CA Meal Penalty | T2 | Roadmap |
| Wave 2 | Utilization & Productivity | T2 | Roadmap |

## Exemplos citados no Annex v1.2

| Report family | Exemplos de relatórios |
|---|---|
| Accrual Reporting | Accrual validation; balance payouts; valor/liability de balances nos books |
| Labor Charge Reporting | Labor charges por employee/date; por multiple orders/date; total hourly labor por cost center; direct-charged labor |
| Overtime Reporting | OT summary por date; por date + job class; direct vs indirect; daily hours/%; daily worked/signed |
| Employee Reporting | Active employees por cost center; employee roster; hours/absences por date; plant roster; gaps em shift/schedule/home location/job code |
| Signature Reporting | Supervisor signatures; unsigned labor; unsigned timesheets |
| Reconciliation Reporting | Payroll reconciliation entre timecard e payroll export |
| Scheduling & Forecasting | Approaching overtime; accrual forecast; shift mismatch |
| CA Meal Penalty | Penalties, waiver/lunch-time usage, trends e repeat offenders |
| Utilization & Productivity | Utilization manhour totals por week/shift; productivity e efficiency trends |

Existing AutoTime reports dessas famílias são o validation set natural para
accuracy checks e regressão. A Fase 1 usa Labor Charge Reporting e Employee
Reporting como primeiro envelope de entrega; Overtime Reporting tende a seguir
naturalmente Labor Charge, mas permanece fora da Fase 1 até decisão explícita.

## Escopo controlado

A expansão para novas report families fora de Labor Charge e Employee é
explicitamente **fora do escopo da Fase 1** (ver
[Escopo da Fase 1](escopo-fase-1.md) e o risco "Scope creep para novas report
families" no [Plano de 10 Semanas](../03-entrega/plano-10-semanas.md)).

## Referências

- [Mapeamento Interno ↔ Cliente](mapeamento-cliente.md)
- Annex v1.2 (Google Drive) — seção de taxonomia de report families
