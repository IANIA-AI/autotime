# Linux Deployment

Linux é o production tier recomendado para local inference com GPU.

## Candidate runtime profiles

- vLLM ou equivalente para GPU serving.
- llama.cpp para CPU ou deployments mais simples.
- Instalação como local service ou containerized installation, dependendo das restrições do cliente.

## A definir

- GPU requirements.
- VRAM sizing.
- Service manager approach.
- Ports e firewall rules.
- Offline model bundle layout.
- Smoke test commands.
