# Referência de Topologias On-Prem de Deployment

Este documento de referência descreve tiers de deployment para CPU-only, Linux GPU e instalações on-premise de maior concorrência.

```mermaid
flowchart TB
    subgraph CUSTOMER["Ambiente On-Prem Customer-Controlled"]
        USER[Report Writers]
        APP[Standalone Web App]
        CATALOG[Local Semantic Catalog]
        MODEL[Local Model Weights]
        LOGS[Local Logs + Audit]
        OUTPUT[Generated SQL<br/>copy/paste only]
        RW[External AutoTime Report Writer]
        DB[(AutoTime Database)]
    end

    USER --> APP
    APP --> CATALOG
    APP --> MODEL
    APP --> LOGS
    APP --> OUTPUT
    OUTPUT --> RW
    RW --> DB

    APP -. sem runtime DB connection .- DB
    APP -. sem cloud .- CLOUDX[(External Cloud / LLM APIs)]

    subgraph TIERA["Tier A - CPU / Cross-Platform / até aprox. 10 usuários"]
        A_OS[Windows ou Linux]
        A_RUNTIME[llama.cpp Server]
        A_MODEL[7B-14B Quantized GGUF]
        A_QUEUE[Strict Queue + Rate Limits]
    end

    subgraph TIERB["Tier B - Linux GPU / até aprox. 20 usuários"]
        B_OS[Linux]
        B_RUNTIME[vLLM ou equivalente]
        B_MODEL[14B-32B Model]
        B_GPU[Single GPU >= 16-24GB VRAM]
        B_BATCH[Continuous Batching]
    end

    subgraph TIERC["Tier C - Linux GPU / até aprox. 30 usuários"]
        C_OS[Linux]
        C_RUNTIME[vLLM / SGLang / equivalente]
        C_MODEL[32B ou 14B otimizado]
        C_GPU[Higher VRAM GPU ou multi-worker]
        C_GATEWAY[Local Gateway + Worker Replicas]
    end

    TIERA --> APP
    TIERB --> APP
    TIERC --> APP
```

## Premissas de deployment

- Cada cliente tem sua própria instalação.
- O cliente instala em seu próprio hardware ou VM.
- O produto roda sem chamadas externas.
- Model weights, catalog e validators são empacotados localmente.
- Generated SQL é copiado pelo usuário e executado fora da solução no AutoTime Report Writer.

## Tiers recomendados

| Tier | Target | Runtime | OS | Observações |
|---|---|---|---|---|
| Tier A | até 10 usuários | llama.cpp | Windows/Linux | Melhor compatibilidade; throughput menor |
| Tier B | até 20 usuários | vLLM ou equivalente | Linux | Melhor GPU serving e batching |
| Tier C | até 30 usuários | vLLM/SGLang/equivalente | Linux | Exige sizing cuidadoso e possivelmente múltiplos workers |

## Windows versus Linux

Windows support deve ser tratado como uma decisão de product tier, não como compromisso universal.

Framing recomendado:

- Windows pode ser considerado para instalações CPU-compatible usando runtime como llama.cpp.
- Linux deve ser o production tier recomendado para GPU serving e maior concurrency.
- Se GPU serving exigir vLLM ou runtimes equivalentes mais fortes em Linux, Windows deve ser documentado como limitado ou não recomendado para esse tier.

## Offline package

O deployment kit deve incluir:

- app binaries ou container artifacts;
- model weights ou sideload procedure;
- semantic catalog pack;
- config templates;
- smoke tests;
- install guide;
- admin guide;
- troubleshooting guide;
- version manifest.
