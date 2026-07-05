# Escopo da Fase 1

A Fase 1 deve ser tratada como um **Working Product with engineering evidence**, não como uma plataforma enterprise multi-cliente completamente hardened.

## Incluído

- App standalone.
- Local model runtime.
- Report families Labor Charge e Employee.
- Semantic catalog v1.
- Structured IR.
- Deterministic SQL compiler.
- Scope engine.
- SQL guardrails e validators.
- Golden dataset inicial.
- Eval harness.
- Local authentication.
- Audit e request history básicos.
- Linux deployment kit.
- Windows feasibility ou limited tier.
- UAT e release-candidate recommendation.

## Excluído

- Suporte a todas as report families.
- Execução de SQL em produção.
- Integração direta com o AutoTime runtime.
- Cloud LLM APIs.
- Implementação completa de LDAP/OIDC/SAML.
- High availability.
- Multi-node serving.
- Full enterprise hardening.
- Golden dataset grande, com 500+ casos.
- Fine-tuning ou automatic retraining.

## Sucesso da Fase 1

A Fase 1 tem sucesso se o time conseguir demonstrar um fluxo local de governed SQL generation, com eval evidence, smoke-tested deployment e limitações documentadas.
