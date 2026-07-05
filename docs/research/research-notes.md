# Research and Engineering Notes

## Main conclusion

The project should not be designed as “put a local LLM in front of the schema.” It should be designed as a governed engineering system:

```text
Lab + Golden Dataset + Semantic Catalog + IR + Compiler + Guardrails + Local Runtime + Packaging + UAT
```

## Text-to-SQL enterprise reality

Enterprise Text-to-SQL remains hard because real schemas are large, irregular, versioned and semantically ambiguous. Accuracy depends heavily on:

- schema representation;
- business glossary;
- join constraints;
- examples;
- scoping rules;
- evals;
- failure handling.

The product should therefore optimize for controlled generation, not unconstrained model autonomy.

## Evals strategy

Evals should be a discipline, not a single library.

The evaluation stack should include:

1. Static SQL eval.
2. IR schema eval.
3. Execution eval in lab demo DB.
4. SME semantic eval.
5. Safety and abstention eval.

LLM-as-judge may help in auxiliary classification, but should not be the primary correctness metric for SQL.

## Runtime strategy

Shortlist for Phase 1:

- llama.cpp for CPU/cross-platform profile.
- vLLM for Linux GPU profile.

Other runtimes such as SGLang, TensorRT-LLM and TGI may be tracked, but a broad benchmark should not be part of the compressed 8-week critical path.

## Windows/Linux strategy

The product should not promise equal capability across Windows and Linux before benchmark.

Recommended positioning:

- Tier A: Windows/Linux CPU-compatible using llama.cpp or equivalent.
- Tier B/C: Linux GPU recommended for higher concurrency.

## What not to cut in the 8-week plan

Do not cut:

- engineering lab;
- golden dataset;
- semantic catalog;
- IR;
- SQL compiler;
- scope engine;
- validators;
- eval harness.

Cuts should happen in:

- project ceremony;
- benchmark breadth;
- UX refinement;
- enterprise auth depth;
- Windows hardening;
- documentation polish;
- large-scale golden dataset.
