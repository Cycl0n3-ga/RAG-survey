---
title: "RAG Adjacent Interfaces"
taxonomy_version: "v2"
tags: [taxonomy, rag, adjacent]
last_updated: "2026-09-25"
---

# RAG Adjacent Interfaces

> [!IMPORTANT]
> 這些研究線與 RAG 高度互動，但**不是 RAG core lifecycle Domain**。文獻可透過 `taxonomy_home: Axx` 與 `adjacent_interfaces` 保留，不應為了塞進 D01–D14 而扭曲分類。

| ID | Adjacent Interface | Scope | Typical connection to RAG |
|---|---|---|---|
| A01 | Long Context & Sequence Architecture | positional extension, efficient/sparse attention, recurrent/SSM sequence models, long-context benchmarks | D05 retrieval-vs-read routing、D07 context utilization |
| A02 | Context/KV Compression & Inference Efficiency | prompt compression, KV quantization/eviction, cache transport/serving | D07 post-retrieval compression、D14 serving cost |
| A03 | Tokenization & General Model Architecture | byte/patch tokenization or other non-RAG model architecture | corpus representation / model efficiency interface |
| A04 | General Agents & Tool Use | ReAct, Toolformer, AutoGen, WebGPT, generic agent benchmarks | D12 Agentic RAG when retrieval/evidence control is added |
| A05 | Continual Learning & Model Editing | parametric/non-parametric update beyond ordinary index maintenance | D10 dynamic knowledge、D11 memory |

## Classification rule

- 若 primary contribution 不修改 RAG lifecycle，本篇 `taxonomy_home` 使用 Axx，而不是硬塞 Dxx。
- 若一篇 adjacent paper 對 RAG 有直接影響，可同時列 `secondary_domains`。
- `primary_domain` 僅接受 D01–D14；Axx paper 設為 `null`。
