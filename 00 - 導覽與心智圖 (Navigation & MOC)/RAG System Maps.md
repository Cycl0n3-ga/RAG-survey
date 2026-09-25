---
title: "RAG System Maps"
taxonomy_version: "v2"
tags:
  - moc
  - rag
  - architecture
  - system-map
last_updated: "2026-09-26"
---

# RAG System Maps

> [!IMPORTANT]
> 本頁只使用目前正式的 **14 個 Domains（D01–D14）**。  
> 不畫一張超大圖；改用六張小圖。**實線 = 常見主流程，虛線 = optional / feedback / cross-cutting path。**

## 1. Knowledge Preparation → Index

```mermaid
flowchart LR
    SRC["Knowledge Sources"] --> D01["D01 Ingestion & Structure"]
    D01 --> D02["D02 Segmentation & Contextualization"]

    D02 --> RAW["Raw Retrieval Units"]
    RAW --> D04["D04 Representation & Indexing"]

    D02 -. "optional extraction" .-> D03["D03 Knowledge Extraction & Preservation"]
    D01 -. "structured source" .-> D03
    D03 --> SEM["Semantic / Structured Units"]
    SEM --> D04

    D04 --> V["Vector / Multi-vector"]
    D04 --> L["Lexical / Sparse"]
    D04 --> G["Graph"]
    D04 --> H["Hierarchical / Multi-resolution"]
    D04 --> HY["Hybrid"]

    D10["D10 Dynamic Knowledge & Index Maintenance"] -. "insert / update / delete / refresh" .-> D04
```

主要變體：
- **Raw-chunk RAG**：D01 → D02 → D04。
- **Structured / Graph RAG**：D01 → D02 → D03 → D04。
- **Structured source** 可由 D01 直接進 D03，不必先做一般 chunking。
- D03 是可選步驟；Graph / Hierarchical / Proposition 是表示或方法選擇，不是額外 Domain。

## 2. Query Understanding & Retrieval Choices

```mermaid
flowchart LR
    Q["User Query"] --> U["Understand Query"]
    U --> ROUTE["Route / Select Retrieval Strategy"]

    U -. "optional rewrite / expansion / HyDE" .-> RW["Rewrite / Transform"]
    RW --> ROUTE
    U -. "optional decomposition" .-> DEC["Decompose / Sub-question"]
    DEC --> ROUTE

    D04["D04 Indexes"] --> DENSE["Dense / Multi-vector"]
    D04 --> SPARSE["Sparse / Lexical"]
    D04 --> GRAPH["Graph Retrieval"]
    D04 --> HIER["Hierarchical Retrieval"]

    ROUTE --> DENSE
    ROUTE --> SPARSE
    ROUTE --> GRAPH
    ROUTE --> HIER
    ROUTE -. "external source" .-> EXT["Web / API / Tool Retrieval"]

    DENSE --> FUSE["Fusion / Reranking"]
    SPARSE --> FUSE
    GRAPH --> FUSE
    HIER --> FUSE
    EXT --> FUSE

    FUSE --> EV["Candidate Evidence"]
    EV -. "next hop needed" .-> MH["Multi-hop / Iterative Retrieval"]
    MH -.-> ROUTE
```

這整張圖屬 **D05 Query Understanding & Retrieval**。不是每個系統都同時使用所有 retrieval channels。

## 3. Evidence → Context → Generation

```mermaid
flowchart LR
    EV["Candidate Evidence"] --> D06["D06 Evidence Sufficiency"]

    EV -. "time / version / source conflict" .-> D08["D08 Temporal / Conflict / Provenance"]
    D08 --> D06

    D06 -->|Sufficient| FILTER["Filter / Dedup"]
    FILTER --> PACK["Pack Context"]
    PACK -. "optional compression" .-> COMP["Compress"]
    PACK --> ORDER["Order / Position"]
    COMP --> ORDER
    ORDER --> BUDGET["Budget"]
    BUDGET --> D07["D07 Context Utilization"]

    D07 --> D09["D09 Grounded Generation & Attribution"]
    D09 --> OUT["Answer / Report"]

    D06 -. "evidence gap" .-> D05["D05 Retrieve Again"]
    D06 -. "unresolvable" .-> ABS["Abstain"]
    ABS --> OUT

    D09 -. "unsupported / incomplete" .-> D06
```

關鍵邊界：
- **Relevant evidence ≠ sufficient evidence**。
- **Sufficient evidence ≠ model actually used it**。
- D08 是條件式 validation / resolution，不是每個 query 的固定 stage。
- Verification 發現缺證據時應回到 D06/D05，而不只是 regenerate。

## 4. Memory & Agentic Control

```mermaid
flowchart LR
    D11["D11 Memory-Augmented RAG"] -. "memory retrieval" .-> D05["D05 Retrieval"]
    D11 -. "memory context" .-> D07["D07 Context"]
    D09["D09 Generation"] -. "optional memory write" .-> D11

    STATE["Current State"] --> D12["D12 Agentic RAG & Orchestration"]
    D12 -. "rewrite / route / retrieve" .-> D05
    D12 -. "retry / stop / abstain" .-> D06["D06 Sufficiency"]
    D12 -. "resolve source / version" .-> D08["D08 Provenance"]
    D12 -. "verify / generate" .-> D09
```

- **D11 = persistent state lifecycle**。
- **D12 = action selection / control plane**。
- 兩者都不是固定線性 pipeline stage。

## 5. Failure Diagnosis & Repair

```mermaid
flowchart LR
    SIG["Failure Signal"] --> DIAG["Diagnose Failure Type"]

    DIAG --> E1["Parsing / Segmentation Error"]
    DIAG --> E2["Extraction / Consolidation Error"]
    DIAG --> E3["Representation / Index Error"]
    DIAG --> E4["Retrieval Miss"]
    DIAG --> E5["Insufficient Evidence"]
    DIAG --> E6["Temporal / Provenance Conflict"]
    DIAG --> E7["Context Utilization Failure"]
    DIAG --> E8["Unsupported / Incomplete Generation"]

    E1 --> D01["D01 / D02 Repair"]
    E2 --> D03["D03 Re-extract / Reconcile"]
    E3 --> D04["D04 Re-index / Change Representation"]
    E4 --> D05["D05 Rewrite / Retrieve"]
    E5 --> D06["D06 Retry / Stop"]
    E6 --> D08["D08 Resolve"]
    E7 --> D07["D07 Repack / Reorder"]
    E8 --> D09["D09 Verify / Regenerate"]

    D12["D12 Controller"] -. "optional policy" .-> DIAG
```

重點不是「失敗就再檢索」，而是先判斷錯在哪一層，再選 repair action。

## 6. Evaluation, Systems & Adjacent Interfaces

```mermaid
flowchart LR
    CORE["D01-D12 Core RAG System"]

    CORE -. "evaluate / diagnose" .-> D13["D13 Evaluation & Failure Attribution"]
    D14["D14 Systems, Robustness & Security"] -. "latency / cost / observability / reliability" .-> CORE

    A01["A01 Long Context"] -. "hybrid retrieval-vs-read" .-> D05["D05 Retrieval"]
    A01 -. "direct long-context read" .-> D07["D07 Context"]
    A02["A02 Context / KV Compression"] -.-> D07
    A02 -. "serving efficiency" .-> D14
    A03["A03 Tokenization / Model Architecture"] -.-> CORE
    A04["A04 General Agents / Tool Use"] -.-> D12["D12 Agentic RAG"]
    A05["A05 Continual Learning / Model Editing"] -.-> D10["D10 Dynamic Knowledge"]
```

- **D13** 是 evaluation plane，不是「最後一步」。
- **D14** 是 deployment / systems plane，不是 retrieval algorithm。
- **A01–A05** 是 Adjacent Interfaces，不計入 14 Domains。

## Domain Index

| ID | Domain |
|---|---|
| D01 | [[02 - 研究領域專題 (Research Domains)/Domain 01 - Document Ingestion & Structure|Document Ingestion & Structure]] |
| D02 | [[02 - 研究領域專題 (Research Domains)/Domain 02 - Segmentation & Contextualization|Segmentation & Contextualization]] |
| D03 | [[02 - 研究領域專題 (Research Domains)/Domain 03 - Knowledge Extraction & Information Preservation|Knowledge Extraction & Information Preservation]] |
| D04 | [[02 - 研究領域專題 (Research Domains)/Domain 04 - Knowledge Representation & Indexing|Knowledge Representation & Indexing]] |
| D05 | [[02 - 研究領域專題 (Research Domains)/Domain 05 - Query Understanding & Retrieval|Query Understanding & Retrieval]] |
| D06 | [[02 - 研究領域專題 (Research Domains)/Domain 06 - Evidence Sufficiency & Adaptive Retrieval|Evidence Sufficiency & Adaptive Retrieval]] |
| D07 | [[02 - 研究領域專題 (Research Domains)/Domain 07 - Context Construction & Evidence Utilization|Context Construction & Evidence Utilization]] |
| D08 | [[02 - 研究領域專題 (Research Domains)/Domain 08 - Temporal Conflict & Provenance Resolution|Temporal Conflict & Provenance Resolution]] |
| D09 | [[02 - 研究領域專題 (Research Domains)/Domain 09 - Grounded Generation Attribution & Long-form Synthesis|Grounded Generation, Attribution & Long-form Synthesis]] |
| D10 | [[02 - 研究領域專題 (Research Domains)/Domain 10 - Dynamic Knowledge & Index Maintenance|Dynamic Knowledge & Index Maintenance]] |
| D11 | [[02 - 研究領域專題 (Research Domains)/Domain 11 - Memory-Augmented RAG|Memory-Augmented RAG]] |
| D12 | [[02 - 研究領域專題 (Research Domains)/Domain 12 - Agentic RAG & Orchestration|Agentic RAG & Orchestration]] |
| D13 | [[02 - 研究領域專題 (Research Domains)/Domain 13 - RAG Evaluation & Failure Attribution|RAG Evaluation & Failure Attribution]] |
| D14 | [[02 - 研究領域專題 (Research Domains)/Domain 14 - RAG Systems, Robustness & Security|RAG Systems, Robustness & Security]] |

## Related

- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|RAG Research Taxonomy]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Paradigm Tags|Paradigm Tags]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|Adjacent Interfaces]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Benchmark Catalog|Benchmark Catalog]]
