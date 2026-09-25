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


## A01 Research Directions — Long Context & Sequence Architecture

> 這是 Adjacent Interface 的研究地圖，不計入 D01–D14。

| Research line | Typical mechanism | Representative notes |
|---|---|---|
| Exact / IO-aware attention | exact attention with memory-I/O optimization | [[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(NeurIPS 2022-12) FlashAttention - Fast and Memory-Efficient Exact Attention with IO-Awareness|FlashAttention]] |
| Sparse / structured attention | local, block, random, dilated or hashed attention | [[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(ACL 2020-07) Longformer - The Long-Document Transformer|Longformer]], [[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(ICLR 2020-04) Reformer - The Efficient Transformer|Reformer]] |
| Recurrent / streaming context | recurrent memory or bounded streaming cache | [[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(ACL 2019-07) Transformer-XL - Attentive Language Models Beyond a Fixed-Length Context|Transformer-XL]], [[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(ICLR 2024-05) Efficient Streaming Language Models with Attention Sinks|StreamingLLM]] |
| Linear / state-space sequence models | kernelized attention or selective state-space recurrence | [[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(ICLR 2021-05) Rethinking Attention with Performers|Performer]], [[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(arXiv 2023-12) Mamba - Linear-Time Sequence Modeling with Selective State Spaces|Mamba]] |
| Positional extension | extend usable RoPE / position range | [[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(ICLR 2024-05) YaRN - Efficient Context Window Extension of Large Language Models|YaRN]], [[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(ICML 2024-07) LongRoPE - Extending LLM Context Window Beyond 2 Million Tokens|LongRoPE]] |
| Distributed context | split long sequence/context across devices | [[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(ICLR 2024-05) RingAttention with Blockwise Transformers for Near-Infinite Context|RingAttention]] |
| Compressive / infinite-context memory | local exact context + compressed long-range memory | [[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(arXiv 2024-04) Leave No Context Behind - Efficient Infinite Context Transformers with Infini-attention|Infini-attention]] |
| Efficient long-context tuning | sparse or parameter-efficient context extension | [[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(ICLR 2024-05) LongLoRA - Efficient Fine-tuning of Long-Context Large Language Models|LongLoRA]] |

RAG interface questions:
- 何時整篇直接讀（long-context read），何時 retrieve？
- 名義 context window 與 effective context utilization 差多少？
- long-context read 與 retrieval / hierarchical retrieval 能否混合路由？

## A02 Research Directions — Compression & Inference Efficiency

不要把所有「壓縮」混成同一問題。至少分成：

| Layer | What is compressed | Typical methods | RAG connection |
|---|---|---|---|
| Tokenization / byte-patch | input representation itself | BLT | A03 / model architecture |
| Prompt / input text | visible input tokens | LLMLingua / LongLLMLingua / Selective Context | D07 context construction |
| Retrieved context | retrieved evidence before generation | RECOMP | D07 |
| KV cache width/precision | decoder cache values | KIVI | D14 serving |
| KV cache token retention | which historical KV entries remain | H2O / SnapKV / PyramidKV / Scissorhands | D14 serving |
| KV cache depth | cross-layer cache redundancy | MiniCache | D14 serving |
| KV transport | cache transmission / streaming | CacheGen | D14 distributed serving |
| Learned soft compression | hidden / soft prompt summaries | Gist Tokens | adjacent model-side compression |

核心邊界：
- **Context compression** 可能改變可見 evidence，會影響 faithfulness。
- **KV compression** 通常不改寫文字 evidence，本質是 inference/serving optimization。
- **Tokenizer / byte architecture** 更靠近 A03，不應和 RAG context compression 混成同一 Domain。
