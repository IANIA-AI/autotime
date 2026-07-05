# Perguntas Abertas para AutoTime

Estes itens devem ser validados com AutoTime, Cole, Harold e SMEs relevantes.

## Produto e uso

1. Qual é o número esperado de named users por cliente?
2. Qual é a peak concurrency esperada: até 10, 20 ou 30 inference requests simultâneos?
3. Que expectativa de latency é aceitável para report writers?
4. O produto deve retornar somente SQL, ou SQL mais explicação e caveats?
5. Os usuários devem poder avaliar, aceitar, rejeitar ou anotar generated SQL?

## Infraestrutura

1. Quais são os ambientes mínimo e típico dos clientes?
2. Quais clientes são Windows-only?
3. Quais clientes podem rodar Linux VMs?
4. GPUs estão disponíveis ou são esperadas?
5. Air-gapped installations são exigidas?
6. Clientes podem instalar local model weights?
7. Containers são aceitáveis, ou instalação native/service deve ser suportada?

## Database e schema

1. Qual versão do AutoTime é o target baseline?
2. Quão estável é o schema entre versões de clientes?
3. Existem mudanças específicas de schema no AutoTime 2.3+ e 2.4+?
4. Quais schema artifacts são canônicos?
5. As tabelas query_context e query_* são suficientes para inferir o comportamento do Report Writer?
6. Existem report SQL examples para Labor Charge e Employee?

## Scoping e security

1. Como o AutoTime representa "my employees"?
2. Como o AutoTime representa "my facility"?
3. Quais hierarchy tables devem ser consideradas authoritative?
4. Qual é a relação entre Security Roles e managerial scope?
5. Quais scoping rules precisam ser suportadas na Fase 1?
6. Quais scoping rules devem causar abstention se solicitadas?

## Golden dataset e UAT

1. Quem no AutoTime validará expected SQL?
2. Quem fornecerá perguntas reais de relatório?
3. Quantos casos Cole/SME conseguem validar por semana?
4. O que define "correct enough" para o working product inicial?
5. Quais existing reports são mais representativos?
6. Quais negative ou unsafe cases devem ser incluídos?

## Deployment e release

1. Qual é o formato preferido de instalação?
2. Quem instalará o produto durante UAT?
3. O que deve estar incluído no deployment kit?
4. Qual security/compliance documentation do cliente será esperada?
5. Qual é o go/no-go criterion para o primeiro customer pilot?
