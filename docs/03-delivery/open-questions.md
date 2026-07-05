# Open Questions for AutoTime

These items should be validated with AutoTime, Cole, Harold and relevant SMEs.

## Product and usage

1. What is the expected number of named users per customer?
2. What is the expected peak concurrency: up to 10, 20 or 30 simultaneous inference requests?
3. What latency expectation is acceptable for report writers?
4. Should the product return only SQL, or SQL plus explanation and caveats?
5. Should users be able to rate, accept, reject or annotate generated SQL?

## Infrastructure

1. What are the minimum and typical customer environments?
2. Which customers are Windows-only?
3. Which customers can run Linux VMs?
4. Are GPUs available or expected?
5. Are air-gapped installations required?
6. Are customers allowed to install local model weights?
7. Are containers acceptable, or should native/service installation be supported?

## Database and schema

1. Which AutoTime version is the target baseline?
2. How stable is the schema across customer versions?
3. Are there version-specific schema changes in AutoTime 2.3+ and 2.4+?
4. Which schema artifacts are canonical?
5. Are query_context and query_* tables sufficient to infer Report Writer behavior?
6. Are there existing report SQL examples for Labor Charge and Employee?

## Scoping and security

1. How does AutoTime represent “my employees”?
2. How does AutoTime represent “my facility”?
3. What hierarchy tables should be considered authoritative?
4. What is the relationship between Security Roles and managerial scope?
5. Which scoping rules must be supported in Phase 1?
6. Which scoping rules should cause abstention if requested?

## Golden dataset and UAT

1. Who at AutoTime will validate expected SQL?
2. Who will provide real report questions?
3. How many cases can Cole/SME validate per week?
4. What defines “correct enough” for the initial working product?
5. Which existing reports are most representative?
6. Which negative or unsafe cases should be included?

## Deployment and release

1. What is the preferred installation format?
2. Who will install the product during UAT?
3. What should be included in the deployment kit?
4. What customer security/compliance documentation will be expected?
5. What is the go/no-go criterion for a first customer pilot?
