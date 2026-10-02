---
title: "Domain 05 - Query Understanding & Retrieval"
domain_id: "D05"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Retrieval"
last_updated: "2026-09-27"
---

# Domain 05 - Query Understanding & Retrieval

> [!WARNING]
> **Phase 1 closure is authoritative.** 若本頁較早段落與底部「Phase 1 Closure — 2026-09-27」衝突，以 closure 為準；舊文字暫留作 Phase 2 forensic audit，將於 Phase 7 一次正規化。

## Core Question
如何理解 query，選擇 retrieval strategy，並找出、融合與排序最相關的候選 evidence？

```mermaid
flowchart LR
    Q["Query"] --> U["Understand"]
    U -. "optional" .-> RW["Rewrite / Expand / HyDE"]
    U -. "optional" .-> DC["Decompose"]
    U --> RT["Route"]
    RW --> RT
    DC --> RT
    RT --> D["Dense"]
    RT --> S["Sparse"]
    RT --> G["Graph"]
    RT --> H["Hierarchical"]
    D --> F["Fusion / Rerank"]
    S --> F
    G --> F
    H --> F
    DC -. "next hop" .-> MH["Multi-hop"]
    F -. "need next hop" .-> MH
    MH -.-> RT
    F --> EV["Candidate Evidence"]
```

## Includes
- query understanding / constraint extraction
- query rewrite / expansion / HyDE
- decomposition / sub-question planning
- sparse / dense / late-interaction retrieval
- graph / hierarchical retrieval
- fusion / reranking / filtering
- multi-hop / compositional retrieval
- query-adaptive retrieval granularity

## Excludes
- 是否已取得足夠 evidence → D06
- context packing / compression → D07
- general controller / tool orchestration → D12

## Level-2 Topics
- Query Understanding
- Query Transformation
- Query Decomposition
- Retrieval Routing
- Retrieval & Reranking
- Fusion
- Multi-hop Retrieval
- Retrieval Granularity
- Retriever / Joint Training

## Boundary
```text
Relevance ≠ Sufficiency
```
D05 判斷「哪些 evidence 比較相關」；D06 判斷「目前 evidence 是否已足夠完成任務」。

## Representative Notes

**Current primary-note coverage: 19**

- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(EMNLP 2020-11) Dense Passage Retrieval for Open-Domain Question Answering|DPR]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(SIGIR 2020-07) ColBERT - Efficient and Effective Passage Search via Contextualized Late Interaction over BERT|ColBERT]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(NAACL 2022-07) ColBERTv2 - Effective and Efficient Retrieval via Lightweight Late Interaction|ColBERTv2]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(SIGIR 2022-07) SPLADE v2 - Sparse Lexical and Expansion Model for Information Retrieval|SPLADE v2]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(TMLR 2022-08) Unsupervised Dense Information Retrieval with Contrastive Learning|Contriever]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(ACL 2023-07) Precise Zero-Shot Dense Retrieval without Relevance Labels|HyDE]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(ACL 2023-07) Interleaving Retrieval with Chain-of-Thought Reasoning for Knowledge-Intensive Multi-Step Questions|IRCoT]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(EMNLP 2023-12) Query Rewriting in Retrieval-Augmented Large Language Models|Query Rewriting in RAG]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(ICML 2020-07) REALM - Retrieval-Augmented Language Model Pre-Training|REALM]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(ICLR 2024-05) RA-DIT - Retrieval-Augmented Dual Instruction Tuning|RA-DIT]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(NAACL 2024-06) REPLUG - Retrieval-Augmented Black-Box Language Models|REPLUG]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(NeurIPS 2024-12) RankRAG - Unifying Context Ranking with Retrieval-Augmented Generation in LLMs|RankRAG]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(COLM 2024-10) RQ-RAG - Learning to Refine Queries for Retrieval Augmented Generation|RQ-RAG]]
- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2024-12) HippoRAG - Neurobiologically Inspired Long-Term Memory for Large Language Models|HippoRAG]]
- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2024-12) G-Retriever - Retrieval-Augmented Generation for Textual Graph Understanding and Question Answering|G-Retriever]]
- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NAACL 2025-05) Knowledge Graph-Guided Retrieval Augmented Generation|KG2RAG]]
- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2025-11) PropRAG - Guiding Retrieval with Beam Search over Proposition Paths|PropRAG]]
- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2025-12) GFM-RAG - Graph Foundation Model for Retrieval Augmented Generation|GFM-RAG]]
- [[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(NeurIPS 2021-12) BEIR - A Heterogeneous Benchmark for Zero-shot Evaluation of Information Retrieval Models|BEIR]]

### Cross-lifecycle Anchors (CROSS)
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(ICML 2022-07) Improving Language Models by Retrieving from Trillions of Tokens|RETRO]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(JMLR 2023-01) Atlas - Few-shot Learning with Retrieval Augmented Language Models|Atlas]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(NeurIPS 2020-12) Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks|RAG (Lewis et al., 2020)]]

### Cross-domain Anchors
- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2026-05) LinearRAG - Linear Graph Retrieval Augmented Generation on Large-scale Corpora|LinearRAG]] (D03 Primary / D05 Secondary: two-stage SpMM semantic bridging + PPR ranking)
- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(arXiv 2024-09) MemoRAG - Moving towards Next-Gen RAG Via Memory-Inspired Knowledge Discovery|MemoRAG]] (D11 Primary / D05 Secondary: memory-inspired cue retrieval)

## Retrieval Strategy Spectrum
舊版「Advanced RAG」頁面的有效內容保留為 retrieval strategy spectrum，但重新放回正確邊界：

| Strategy | Core idea | Canonical home |
|---|---|---|
| Dense retrieval | query / passage single-vector semantic matching | D05 |
| Sparse / lexical | exact / weighted lexical matching | D05 |
| Late interaction | token-level query-document interaction（例如 ColBERT） | D04 encoding + D05 search |
| Hybrid retrieval | dense + sparse + fusion / RRF | D04/D05 |
| Query transformation | rewrite / expansion / HyDE | D05 |
| Decomposition / multi-hop | sub-question → iterative retrieval | D05 |
| Adaptive / active retrieval | decide whether/when to retrieve again | D06（不是 D05 的 relevance 問題） |
| Agent-controlled retrieval | controller selects tools/actions | D12 |
| Graph / PPR retrieval | 局部實體激活 + 全局 PageRank 傳播 (HippoRAG, LinearRAG) | D04 圖索引 + D05 遍歷排序 |
| Retrieval-augmented training | retrieval is trained/used during pretraining, joint retriever-reader training, or dual instruction tuning | D05（with D04 representation/training interface） |

這個表的目的，是避免再把「Advanced RAG」當成一個模糊大 Domain。

## Navigation
- [[02 - 研究領域專題 (Research Domains)/Domain 04 - Knowledge Representation & Indexing|D04 Knowledge Representation & Indexing]]
- [[02 - 研究領域專題 (Research Domains)/Domain 06 - Evidence Sufficiency & Adaptive Retrieval|D06 Evidence Sufficiency & Adaptive Retrieval]]

## Phase 1 Closure — 2026-09-27

> [!IMPORTANT]
> **Canonical name remains D05 Query Understanding & Retrieval.**

**Core question**：Given a query and a searchable index, what evidence should be retrieved, fused and ranked?

**Canonical Level-2**
- Query Transformation: rewrite / expansion / HyDE / disambiguation
- Query Decomposition & Multi-hop Retrieval
- Retrieval & Relevance Modeling: dense / sparse / late-interaction / graph
- Fusion & Reranking
- Retriever–Generator Alignment

**Hard boundary**
- retrieval granularity → D02
- whether/when to retrieve, retry or stop → D06
- general tool/action routing → D12
- using retrieval does not automatically make D05 a secondary contribution

**Paper decisions**
- KEEP DPR, ColBERT/ColBERTv2, SPLADE, Contriever, HyDE, IRCoT, RankRAG, PropRAG, KG²RAG, G-Retriever.
- HippoRAG: MOVE here from D04; D04 secondary.
- GFM-RAG: ADD D05 / D04 secondary.
- Query Rewriting in RAG (EMNLP 2023): ADD.
- RQ-RAG (COLM 2024): ADD.
- RAG 2020, RETRO and Atlas: move to CROSS rather than inflate D05 primary coverage.
- Adaptive-RAG remains D06 primary.
- LinearRAG (ICLR 2026): D03 primary / D05 secondary (two-stage SpMM semantic bridging + PPR ranking).
- MemoRAG (arXiv 2024): REALIGN to D11 primary / D05 secondary (global memory anchor in D11, cue-based retrieval secondary interface).
