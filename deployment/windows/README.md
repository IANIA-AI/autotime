# Windows Deployment

Windows support deve ser tratado como uma decisão de product tier.

## Posicionamento recomendado

- Windows pode ser viável para CPU-compatible deployments usando llama.cpp ou equivalente.
- High-throughput GPU serving deve ser posicionado como Linux-first.
- Se Windows não suportar o runtime selecionado de forma confiável, documentar como tier limitado ou não suportado para esse runtime.

## A definir

- Install mode.
- Service wrapper.
- Local model path.
- Config path.
- Log path.
- Smoke test procedure.
