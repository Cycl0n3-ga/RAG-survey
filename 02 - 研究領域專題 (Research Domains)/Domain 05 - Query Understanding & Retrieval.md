---
title: "Domain 05 - Query Understanding & Retrieval"
domain_id: "D05"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Retrieval"
last_updated: "2026-09-25"
---

# Domain 05 - Query Understanding & Retrieval

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

## Boundary
```text
Relevance ≠ Sufficiency
```
D05 判斷「哪些 evidence 比較相關」；D06 判斷「目前 evidence 是否已足夠完成任務」。

## Navigation
- [[02 - 研究領域專題 (Research Domains)/Domain 04 - Knowledge Representation & Indexing|D04 Knowledge Representation & Indexing]]
- [[02 - 研究領域專題 (Research Domains)/Domain 06 - Evidence Sufficiency & Adaptive Retrieval|D06 Evidence Sufficiency & Adaptive Retrieval]]
