# Golden Dataset

This directory will contain the initial golden dataset for Text-to-SQL evaluation.

## Recommended fields

| Field | Description |
|---|---|
| case_id | Stable unique case ID |
| family | Report family, e.g. Labor Charge or Employee |
| complexity | simple, medium, complex |
| question | Natural language question |
| expected_behavior | generate_sql, abstain, block |
| expected_sql | Expected SQL, when applicable |
| expected_result_reference | Result-set fixture or checksum, when applicable |
| requires_scope | Whether managerial scope is required |
| scope_type | my_employees, my_facility, etc. |
| security_case | Whether this is a safety test |
| notes | SME notes |

## Initial target size

For the 8-week working-product version, target 120-180 high-quality cases.
