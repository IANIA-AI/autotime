# Critérios de Release

Um release candidate não deve ser declarado sem demonstrar comportamento de working product mais engineering evidence.

## Critérios mínimos

- App roda standalone no ambiente suportado.
- Local model runtime funciona sem cloud dependency.
- Report families Labor Charge e Employee são suportadas.
- SQL é gerado pelo caminho IR + compiler.
- Validators bloqueiam DDL/DML e unsafe operations.
- Scope rules são aplicadas quando exigidas.
- Scope não suportado leva a abstention.
- Golden dataset roda end-to-end.
- Eval report é gerado.
- Installation smoke tests passam.
- UAT foi executado com envolvimento de AutoTime SME.
- Limitações conhecidas estão documentadas.
- Evidence pack final foi produzido.
- Go/no-go técnico foi assinado por Persival.
- Aceite/UAT foi conduzido por Erlon.
- Deployment kit foi revisado por Fábio.
- Eval/scoping foi validado por Marcos.

## Evidência esperada

- Demo do fluxo end-to-end de natural-language para governed SQL.
- Eval report com métricas pass/fail e failure taxonomy.
- Smoke-test output para o installation tier suportado.
- UAT notes e issue list.
- Evidence pack final.
- Release recommendation documentada: go, conditional go ou no-go.

## Não é suficiente

- Prompt demo que gera SQL plausível sem compiler validation.
- Model benchmark sem business-case evals.
- UI demo sem evidência de catalog, scope e validators.
- Release candidate que depende de cloud LLM APIs.
