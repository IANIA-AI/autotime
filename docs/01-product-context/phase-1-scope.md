# Phase 1 Scope

Phase 1 should be framed as a **Working Product with engineering evidence**, not a fully hardened multi-client enterprise platform.

## Included

- Standalone app.
- Local model runtime.
- Labor Charge and Employee report families.
- Semantic catalog v1.
- Structured IR.
- Deterministic SQL compiler.
- Scope engine.
- SQL guardrails and validators.
- Initial golden dataset.
- Eval harness.
- Local authentication.
- Basic audit and request history.
- Linux deployment kit.
- Windows feasibility or limited tier.
- UAT and release-candidate recommendation.

## Excluded

- Support for all report families.
- Production SQL execution.
- Direct integration with AutoTime runtime.
- Cloud LLM APIs.
- Complete LDAP/OIDC/SAML implementation.
- High availability.
- Multi-node serving.
- Full enterprise hardening.
- Large 500+ case golden dataset.
- Fine-tuning or automatic retraining.

## Phase 1 success

Phase 1 succeeds if the team can show a local governed SQL generation flow, with eval evidence, smoke-tested deployment and documented limitations.
