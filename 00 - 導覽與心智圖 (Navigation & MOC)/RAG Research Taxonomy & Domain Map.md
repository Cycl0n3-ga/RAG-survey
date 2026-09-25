---
title: "RAG Research Taxonomy & Domain Map"
taxonomy_version: "v2"
tags:
  - taxonomy
  - survey
  - rag
  - research-map
last_updated: "2026-09-26"
---

# RAG Research Taxonomy & Domain Map

> [!IMPORTANT]
> 本 repo 只使用 **14 個正式 RAG Research Domains（D01–D14）**。
> Topic、Paradigm Tag、Adjacent Interface 都不是額外 Domain。
>
> **D01–D14 是 operational taxonomy，不是宣稱為某篇 survey 的既有標準。** 主流 survey 通常使用更粗的 indexing / retrieval / post-retrieval / generation / evaluation 等軸；本 repo 為了可實驗、可歸因而再細分。

## 0. Survey-Aligned Simple View

對外只需要記住 6 個 supergroups；D01–D14 是其內部細分，不另建立第三套編號：

| Supergroup | Domains | 對應主流 survey 常見概念 |
|---|---|---|
| **Source & Knowledge Construction** | D01–D04 | parsing / chunking / extraction / representation / indexing |
| **Retrieval & Evidence Control** | D05–D08 | query / retrieval / reranking / adaptive retrieval / post-retrieval validation |
| **Grounded Generation** | D09 | evidence-grounded generation / attribution / long-form synthesis |
| **Stateful & Agentic RAG** | D10–D12 | dynamic knowledge / memory / iterative-agentic orchestration |
| **Evaluation** | D13 | retrieval + generation evaluation / diagnosis |
| **Deployment & Trust** | D14 | efficiency / robustness / privacy / security / governance |

這 6 組只是 navigation layer；正式 paper metadata 仍只使用 D01–D14。

## 1. Core Lifecycle

```mermaid
flowchart LR
    SRC["Knowledge Sources"] --> D01["D01 Ingestion & Structure"]
    D01 --> D02["D02 Segmentation & Contextualization"]

    D02 --> D04["D04 Representation & Indexing"]
    D02 -. "optional extraction" .-> D03["D03 Knowledge Extraction & Preservation"]
    D03 --> D04

    Q["User Query"] --> D05["D05 Query Understanding & Retrieval"]
    D04 --> D05

    D05 --> D06["D06 Evidence Sufficiency & Adaptive Retrieval"]
    D05 -. "when time / source / version matters" .-> D08["D08 Temporal / Conflict / Provenance"]
    D08 --> D06

    D06 --> D07["D07 Context Construction & Utilization"]
    D07 --> D09["D09 Grounded Generation & Long-form Synthesis"]

    D06 -. "gap / retry" .-> D05
    D09 -. "unsupported / incomplete" .-> D06
```

D03 與 D08 都是條件式路徑：
- raw-chunk RAG 可由 D02 直接進 D04；
- 只有需要 structured knowledge 時才走 D03；
- 只有 time / version / source conflict 需要顯式處理時才走 D08；source authority / credibility arbitration 是較薄的可選子題。

## 2. Cross-Lifecycle Domains

```mermaid
flowchart LR
    D10["D10 Dynamic Knowledge & Index Maintenance"] --> CORE["Core RAG Lifecycle"]
    D11["D11 Memory-Augmented RAG"] --> CORE
    D12["D12 Agentic RAG & Orchestration"] --> CORE
    CORE --> D13["D13 Evaluation & Failure Attribution"]
    D14["D14 Systems, Robustness & Security"] --> CORE
```

## 3. The 14 Domains

| ID | Domain | Core question |
|---|---|---|
| D01 | [[02 - 研究領域專題 (Research Domains)/Domain 01 - Document Ingestion & Structure|Document Ingestion & Structure]] | 如何把來源轉成保留結構與 provenance 的 corpus？ |
| D02 | [[02 - 研究領域專題 (Research Domains)/Domain 02 - Segmentation & Contextualization|Segmentation & Contextualization]] | 應切成什麼 retrieval units，且如何保留必要上下文？ |
| D03 | [[02 - 研究領域專題 (Research Domains)/Domain 03 - Knowledge Extraction & Information Preservation|Knowledge Extraction & Information Preservation]] | 要抽哪些 semantic units，並如何避免資訊失真？ |
| D04 | [[02 - 研究領域專題 (Research Domains)/Domain 04 - Knowledge Representation & Indexing|Knowledge Representation & Indexing]] | 知識如何表示、編碼與建立 index？ |
| D05 | [[02 - 研究領域專題 (Research Domains)/Domain 05 - Query Understanding & Retrieval|Query Understanding & Retrieval]] | 如何理解 query，搜尋、融合與 rerank 候選 evidence？ |
| D06 | [[02 - 研究領域專題 (Research Domains)/Domain 06 - Evidence Sufficiency & Adaptive Retrieval|Evidence Sufficiency & Adaptive Retrieval]] | 何時 retrieve/retry/stop；以及 evidence set 是否足夠？ |
| D07 | [[02 - 研究領域專題 (Research Domains)/Domain 07 - Context Construction & Evidence Utilization|Context Construction & Evidence Utilization]] | 如何建構有限 context，並確保模型實際利用 evidence？ |
| D08 | [[02 - 研究領域專題 (Research Domains)/Domain 08 - Temporal Conflict & Provenance Resolution|Temporal Conflict & Provenance Resolution]] | 如何處理 freshness、時間/版本與互相衝突的 evidence？ |
| D09 | [[02 - 研究領域專題 (Research Domains)/Domain 09 - Grounded Generation Attribution & Long-form Synthesis|Grounded Generation, Attribution & Long-form Synthesis]] | 如何產生可驗證、可歸因的答案或長篇報告？ |
| D10 | [[02 - 研究領域專題 (Research Domains)/Domain 10 - Dynamic Knowledge & Index Maintenance|Dynamic Knowledge & Index Maintenance]] | Knowledge base 變動時如何正確更新？ |
| D11 | [[02 - 研究領域專題 (Research Domains)/Domain 11 - Memory-Augmented RAG|Memory-Augmented RAG]] | 如何管理可跨 interaction/task 持續演化的 derived memory？ |
| D12 | [[02 - 研究領域專題 (Research Domains)/Domain 12 - Agentic RAG & Orchestration|Agentic RAG & Orchestration]] | 誰決定下一個 retrieve / tool / verify / generate action？ |
| D13 | [[02 - 研究領域專題 (Research Domains)/Domain 13 - RAG Evaluation & Failure Attribution|RAG Evaluation & Failure Attribution]] | 如何分離 retrieval、evidence、context、generation 的問題來源？ |
| D14 | [[02 - 研究領域專題 (Research Domains)/Domain 14 - RAG Systems, Robustness & Security|RAG Systems, Robustness & Security]] | 如何管理 latency、cost、observability、robustness 與 security？ |

## 4. Other Axes

- **Level-2 Topics**：Domain 內的細分問題，例如 chunking、reranking、sufficiency、citation。
- **Paradigm Tags**：GraphRAG、Hierarchical RAG、Adaptive RAG、Agentic RAG、Multimodal RAG。
- **Adjacent Interfaces**：Long Context、KV Cache、General Agents、Continual Learning 等與 RAG 高度相關但不屬於 core lifecycle 的研究線。

## 5. Hard Boundaries

```text
Segmentation != Extraction != Representation
Relevance != Sufficiency != Utilization != Faithfulness
Dynamic Index != Persistent Memory
Domain != Paradigm Tag != Benchmark
```

## Navigation

- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG System Maps|RAG System Maps]]
- [[02 - 研究領域專題 (Research Domains)/README|Research Domains]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Paradigm Tags|RAG Paradigm Tags]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|RAG Adjacent Interfaces]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Benchmark Catalog|RAG Benchmark Catalog]]
