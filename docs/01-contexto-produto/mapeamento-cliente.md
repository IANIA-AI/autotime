# Mapeamento Interno ↔ Cliente

Referência de vocabulário para qualquer comunicação com o AutoTime.
Documento-base externo: "AutoTime Governed AI Report Writer — Premises
Confirmation & Technical Annex v1.2" (Google Drive, jun/2026, pós-feedback do Cole).

O material interno (este repositório) e o material do cliente contam a mesma
história arquitetural e de escopo. As diferenças abaixo são apenas de
vocabulário — mas precisam ser conhecidas por todo o time antes de qualquer
call, e-mail ou documento enviado ao AutoTime.

## Nome do produto

- **Externo (usar sempre com o cliente):** AutoTime Governed AI Report Writer
- **Interno (este repositório):** AutoTime Governed SQL Writer

## Timeline e números

- Externo: 10 semanas, com os milestones M1/M2/M3 do Annex mapeados.
  M3 = "Pronto para Piloto" na semana 8; semanas 9–10 = Sprint conjunto de
  UAT & Hardening. Ver [Plano de 10 Semanas](../03-entrega/plano-10-semanas.md).
- Os targets internos de eval (IR JSON validity ≥ 98%, SQL parse pass ≥ 95%,
  execution accuracy 80-85% → 90%+, etc. — ver
  [Pipeline de Evals](../90-referencia/pipeline-evals.md)) **nunca** são citados
  ao cliente como compromisso. O framing externo é "engenharia de
  confiabilidade por escopo controlado".

## Writer ≠ Runner (linguagem do Cole)

Report writers operam com admin visibility; a ferramenta **não enforça
acesso**. Scope filters são parametrizados e resolvidos em run-time pelo
AutoTime para quem roda o relatório: o writer escreve "my employees" uma vez;
cada runner vê os seus. Ver a nuance completa em
[Fronteiras do Produto](fronteiras-produto.md#fronteiras-de-scope).

## Work packages

O Annex usa WP1–WP7; o plano interno usa WP0–WP9 — **as numerações não
correspondem** item a item (ex.: packaging é WP7 no Annex e WP8 no plano
interno). Com o cliente, referir work packages sempre pelo nome, nunca pelo
número, até a unificação na proposta técnica formal.

## Terminologia

"Piloto" — nunca "POC". O que a Fase 2 instala é o produto real em ambiente
controlado, não uma prova de conceito descartável. "POC-ready" vira
"Pronto para Piloto" em qualquer material, interno ou externo.

Exceção histórica: a pre-assessment de maio/2026 menciona o "Docker-based
proof of concept" do Projeto 1 (chatbot de documentação) — ali o termo é
correto, pois era de fato um PoC exploratório e descartável, não o produto
sendo entregue.

## Report families

Ver [Report Families](report-families.md) para a taxonomia completa de 9
famílias em waves acordada com o Cole. A Fase 1 permanece em Labor Charge e
Employee; as demais são roadmap de fases futuras.
