# Golden Dataset

Este diretório irá conter o golden dataset inicial para Text-to-SQL evaluation.

## Campos recomendados

| Campo | Descrição |
|---|---|
| case_id | ID único e estável do caso |
| family | Report family, por exemplo Labor Charge ou Employee |
| complexity | simple, medium, complex |
| question | Pergunta em linguagem natural |
| expected_behavior | generate_sql, abstain, block |
| expected_sql | Expected SQL, quando aplicável |
| expected_result_reference | Fixture ou checksum de result set, quando aplicável |
| requires_scope | Se managerial scope é exigido |
| scope_type | my_employees, my_facility, etc. |
| security_case | Se é um safety test |
| notes | Notas de SME |

## Tamanho inicial alvo

Para a versão de working product de 8 semanas, mire 120-180 casos de alta qualidade.
