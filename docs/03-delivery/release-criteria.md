# Release Criteria

A release candidate should not be declared unless the project can show working product behavior plus engineering evidence.

## Minimum criteria

- App runs standalone in the supported environment.
- Local model runtime works without cloud dependency.
- Labor Charge and Employee report families are supported.
- SQL is generated through the IR + compiler path.
- Validators block DDL/DML and unsafe operations.
- Scope rules are applied when required.
- Unsupported scope leads to abstention.
- Golden dataset runs end-to-end.
- Eval report is generated.
- Installation smoke tests pass.
- UAT has been executed with AutoTime SME involvement.
- Known limitations are documented.

## Evidence expected

- Demo of end-to-end natural-language to governed SQL flow.
- Eval report with pass/fail metrics and failure taxonomy.
- Smoke-test output for supported installation tier.
- UAT notes and issue list.
- Documented release recommendation: go, conditional go or no-go.

## Not sufficient

- A prompt demo that generates plausible SQL without compiler validation.
- A model benchmark without business-case evals.
- A UI demo without catalog, scope and validator evidence.
- A release candidate that depends on cloud LLM APIs.
