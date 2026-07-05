# AutoTime Governed SQL Writer Onboarding

This document is the onboarding path for project sponsors, delivery leads and engineers joining the AutoTime Governed SQL Writer effort.

## 10-minute orientation

AutoTime wants a local, customer-controlled assistant that turns report-writer questions into governed SQL for AutoTime's external Report Writer.

The product is not a chatbot that emits SQL. It is a governed generation system:

```text
Natural Language -> IR -> Semantic Catalog -> SQL Compiler -> Scope Engine -> Validators -> Governed SQL
```

The LLM helps interpret the request, but the final SQL must come from controlled semantic resolution, deterministic compilation, scope enforcement and validation.

## What the product does

- Accepts natural-language report questions.
- Uses local model inference inside the customer's environment.
- Maps the request to supported AutoTime report families.
- Generates structured intent.
- Resolves fields, joins, metrics and filters through a semantic catalog.
- Produces copyable SQL for AutoTime's external Report Writer.
- Logs trace, audit and validation information.

## What the product does not do

- It does not execute SQL in production.
- It does not connect to the production database at runtime.
- It does not call cloud LLM APIs.
- It does not bypass AutoTime permissions or Report Writer controls.
- It does not promise valid SQL for unsupported report families or unknown scope rules.

## Read in this order

| Step | Document | Why it matters |
|---:|---|---|
| 1 | [Executive Summary](docs/00-start-here/executive-summary.md) | Shared understanding of the project. |
| 2 | [Product Boundaries](docs/01-product-context/product-boundaries.md) | Rules the implementation must not violate. |
| 3 | [Phase 1 Scope](docs/01-product-context/phase-1-scope.md) | What is included and excluded from the first delivery. |
| 4 | [Architecture Overview](docs/02-architecture/overview.md) | The simplified system model. |
| 5 | [Runtime Flow](docs/02-architecture/runtime-flow.md) | What happens when a user asks a question. |
| 6 | [Validation Flow](docs/02-architecture/validation-flow.md) | How the system blocks, abstains or returns SQL. |
| 7 | [8-Week Delivery Plan](docs/03-delivery/8-week-plan.md) | Work sequence, milestones and release path. |
| 8 | [Open Questions](docs/03-delivery/open-questions.md) | Decisions that need AutoTime or SME input. |

## First-week focus

The first week should produce clarity and working foundations, not polished UX.

Expected first-week outcomes:

- engineering lab environment defined;
- AutoTime demo DB and schema artifacts identified;
- report examples collected;
- Phase 1 report families confirmed;
- semantic catalog format drafted;
- golden dataset case format drafted;
- runtime benchmark plan agreed;
- top open questions assigned to owners.

## Team responsibilities

| Role | Primary focus |
|---|---|
| Delivery / QA | Scope control, risk tracking, acceptance criteria, UAT coordination. |
| Data / SQL / AI Engineering | Semantic catalog, SQL compiler, golden dataset and eval harness. |
| AI Architecture / Tech Lead | Local model strategy, IR design, prompts, guardrails and quality gates. |
| Platform / Fullstack / DevOps | App shell, auth, packaging, deployment, observability and smoke tests. |

See [Team Allocation](docs/03-delivery/team-allocation.md) for the proposed named allocation.

## Critical risks

- Business scope semantics such as "my employees" or "my facility" may be harder than SQL syntax.
- The semantic catalog and golden dataset are first-class engineering assets, not documentation extras.
- Windows support is a product-tier decision and should not be promised as equal to Linux GPU serving before benchmark.
- A release candidate without eval evidence should not be considered ready.

## Detailed reference

After the onboarding path, use:

- [Detailed Solution Architecture](docs/90-reference/detailed-architecture.md)
- [Evaluation Pipeline](docs/90-reference/eval-pipeline.md)
- [Deployment Topologies](docs/90-reference/deployment-topologies.md)
- [Research Notes](docs/99-archive/research-notes.md)
