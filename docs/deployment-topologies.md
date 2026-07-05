# On-Prem Deployment Topologies

This document describes deployment tiers for CPU-only, Linux GPU and higher-concurrency on-premise installations.

```mermaid
flowchart TB
    subgraph CUSTOMER["Customer-Controlled On-Prem Environment"]
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

    APP -. no runtime DB connection .- DB
    APP -. no cloud .- CLOUDX[(External Cloud / LLM APIs)]

    subgraph TIERA["Tier A - CPU / Cross-Platform / up to approx. 10 users"]
        A_OS[Windows or Linux]
        A_RUNTIME[llama.cpp Server]
        A_MODEL[7B-14B Quantized GGUF]
        A_QUEUE[Strict Queue + Rate Limits]
    end

    subgraph TIERB["Tier B - Linux GPU / up to approx. 20 users"]
        B_OS[Linux]
        B_RUNTIME[vLLM or equivalent]
        B_MODEL[14B-32B Model]
        B_GPU[Single GPU >= 16-24GB VRAM]
        B_BATCH[Continuous Batching]
    end

    subgraph TIERC["Tier C - Linux GPU / up to approx. 30 users"]
        C_OS[Linux]
        C_RUNTIME[vLLM / SGLang / equivalent]
        C_MODEL[32B or optimized 14B]
        C_GPU[Higher VRAM GPU or multi-worker]
        C_GATEWAY[Local Gateway + Worker Replicas]
    end

    TIERA --> APP
    TIERB --> APP
    TIERC --> APP
```

## Deployment assumptions

- Each customer has its own installation.
- The customer installs on its own hardware or VM.
- The product runs without external calls.
- Model weights, catalog and validators are packaged locally.
- Generated SQL is copied by the user and executed outside the solution in AutoTime's Report Writer.

## Recommended tiers

| Tier | Target | Runtime | OS | Notes |
|---|---|---|---|---|
| Tier A | up to 10 users | llama.cpp | Windows/Linux | Best compatibility; lower throughput |
| Tier B | up to 20 users | vLLM or equivalent | Linux | Better GPU serving and batching |
| Tier C | up to 30 users | vLLM/SGLang/equivalent | Linux | Requires careful sizing and possibly multiple workers |

## Windows versus Linux

Windows support should be treated as a product-tier decision, not as a universal commitment.

Recommended framing:

- Windows can be considered for CPU-compatible installations using a runtime such as llama.cpp.
- Linux should be the recommended production tier for GPU serving and higher concurrency.
- If GPU serving requires vLLM or equivalent runtimes that are stronger on Linux, Windows should be documented as limited or not recommended for that tier.

## Offline package

The deployment kit should include:

- app binaries or container artifacts;
- model weights or sideload procedure;
- semantic catalog pack;
- config templates;
- smoke tests;
- install guide;
- admin guide;
- troubleshooting guide;
- version manifest.
