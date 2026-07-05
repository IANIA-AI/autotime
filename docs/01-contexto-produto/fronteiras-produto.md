# Fronteiras do Produto

Estas fronteiras são inegociáveis, a menos que o escopo do projeto seja explicitamente alterado.

## Fronteiras de runtime

O runtime do produto entregue:

- não executa SQL em produção;
- não conecta ao production database;
- não chama cloud LLM APIs;
- não depende de serviços externos para geração;
- não contorna o AutoTime external Report Writer;
- não substitui autorização ou runtime security do AutoTime.

## Fronteiras de geração

O LLM não deve produzir o SQL final confiável diretamente.

O LLM pode ajudar a produzir structured intent, mas o governed SQL precisa ser produzido por meio de:

- semantic catalog resolution;
- deterministic SQL compilation;
- scope enforcement;
- SQL parsing e validation;
- policy checks;
- controlled refusal quando o pedido for não suportado ou inseguro.

## Fronteiras de scope

O produto não deve fingir que entende business scope se não consegue aplicar esse scope de forma determinística.

Exemplos que exigem regras explícitas:

- my employees;
- my facility;
- my department;
- my team;
- employees under my management hierarchy.

Scope desconhecido ou não suportado deve gerar abstention, não SQL adivinhado.

## Fronteiras de deployment

O modelo alvo de deployment é customer-controlled e on-premise.

Windows support é uma decisão de tier, não uma promessa de capacidade igual em todos os runtime profiles. Linux deve continuar sendo a direção recomendada para GPU-backed higher-concurrency serving até que benchmark evidence indique o contrário.
