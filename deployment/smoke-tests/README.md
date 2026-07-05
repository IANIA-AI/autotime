# Smoke Tests

Smoke tests devem validar que um pacote instalado funciona em um ambiente limpo.

## Smoke tests mínimos

- App inicia.
- Local model runtime inicia.
- Semantic catalog carrega.
- Health endpoint retorna OK.
- Sample prompt gera IR válido.
- Compiler gera SQL.
- Validators aprovam SQL seguro.
- Validators bloqueiam DDL/DML.
- Audit log é escrito.
- Package version fica visível.
