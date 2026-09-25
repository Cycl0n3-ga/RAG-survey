---
title: "RAG System Maps"
taxonomy_version: "v2"
tags:
  - moc
  - rag
  - architecture
  - system-map
last_updated: "2026-09-25"
---

# RAG System Maps

> [!IMPORTANT]
> 本頁只畫目前有效的 **14 個 Domains（D01–D14）**。  
> 為保持可讀性，把完整 RAG 拆成四張小圖；虛線代表 optional / feedback / cross-cutting path。

## 1. Knowledge Preparation & Indexing

```mermaid
flowchart LR
    SRC["Knowledge Sources"] --> D01["D01 Ingestion & Structure"]
    D01 --> D02["D02 Segmentation & Contextualization"]

    D02 --> RAW["Raw Retrieval Units"]
    D02 -. "optional extraction" .-> D03["D03 Knowledge Extraction & Preservation"]
    D03 --> SEM["Semantic / Structured Units"]

    RAW --> D04["D04 Representation & Indexing"]
    SEM --> D04

    D04 --> VEC["Vector / Lexical / Hybrid"]
    D04 --> GRAPH["Graph"]
    D04 --> HIER["Hierarchical / Multi-resolution"]

    D10["D10 Dynamic Knowledge & Index Maintenance"] -. "update / refresh" .-> D04
```

**可選路徑：**
- Raw-chunk RAG：D01 → D02 → D04。
- Structured / Graph RAG：D01 → D02 → D03 → D04。
- D03 不是所有 RAG 的必要步驟。
- Graph / Hierarchical / Proposition 是 representation / paradigm choices，不是額外 Domain。

## 2. Query → Evidence → Context → Generation

```mermaid
flowchart LR
    Q["User Query"] --> D05["D05 Query Understanding & Retrieval"]
    D04["D04 Index"] --> D05

    D05 --> EV["Candidate Evidence"]

    EV -. "when needed" .-> D08["D08 Temporal / Conflict / Provenance"]
    EV --> D06["D06 Evidence Sufficiency"]
    D08 --> D06

    D06 -->|Sufficient| D07["D07 Context Construction & Utilization"]
    D06 -. "Gap / Retry" .-> D05

    D07 --> D09["D09 Grounded Generation & Long-form Synthesis"]
    D09 --> OUT["Answer / Report"]

    D09 -. "Unsupported / Incomplete" .-> D06
    D06 -. "Unresolvable" .-> ABS["Abstain"]
    ABS --> OUT
```

**可選路徑：**
- D08 只在 freshness、version、authority、source conflict 等問題出現時啟用。
- D06 不只是 retrieve/stop，也可把 gap 送回 D05。
- D09 verification 發現缺證據時可回到 D06，而不是只 regenerate。

## 3. Memory & Agentic Control

```mermaid
flowchart LR
    D11["D11 Memory-Augmented RAG"] -. "memory retrieval" .-> D05["D05 Retrieval"]
    D11 -. "memory context" .-> D07["D07 Context"]

    D12["D12 Agentic RAG & Orchestration"] -. "rewrite / route / retrieve" .-> D05
    D12 -. "retry / stop" .-> D06["D06 Sufficiency"]
    D12 -. "verify / generate / abstain" .-> D09["D09 Generation"]

    D09 -. "optional memory write" .-> D11
```

D11 管 persistent state；D12 管 action selection。兩者都不是固定 pipeline stage。

## 4. Evaluation, Systems & Adjacent Interfaces

```mermaid
flowchart LR
    CORE["D01-D12 RAG System"]

    CORE --> D13["D13 Evaluation & Failure Attribution"]
    D14["D14 Systems & Reliability"] -. "latency / cost / observability" .-> CORE

    A01["A01 Long Context"] -.-> CORE
    A02["A02 Context / KV Compression"] -.-> CORE
    A03["A03 Tokenization / Model Architecture"] -.-> CORE
    A04["A04 General Agents / Tool Use"] -.-> D12
    A05["A05 Continual Learning / Model Editing"] -.-> D10["D10 Dynamic Knowledge"]
```

- **D13**：觀察與歸因，不是最後一個 pipeline step。
- **D14**：deployment / reliability plane，不是 retrieval algorithm。
- **A01–A05**：Adjacent Interfaces，不計入 14 Domains。

## 5. Failure / Repair Paths

```mermaid
flowchart LR
    SIG["Failure Signal"] --> DIAG["Diagnose Failure Type"]
    D12["D12 Controller"] -. "select repair" .-> DIAG

    DIAG --> EX["Extraction Error"]
    DIAG --> RM["Retrieval Miss"]
    DIAG --> GAP["Insufficient Evidence"]
    DIAG --> CF["Temporal / Provenance Conflict"]
    DIAG --> UG["Unsupported / Incomplete Generation"]

    EX --> D03["D03 Re-extract / Expand Source"]
    RM --> D05["D05 Rewrite / Retrieve"]
    GAP --> D06["D06 Retry / Stop / Abstain"]
    CF --> D08["D08 Resolve Time / Source / Version"]
    UG --> D09["D09 Verify / Repair Generation"]

    D03 -.-> SIG
    D05 -.-> SIG
    D06 -.-> SIG
    D08 -.-> SIG
    D09 -.-> SIG
```

這張圖只表達 **repair action space**；不是所有系統都需要完整 controller。  
重點是不要把 extraction error、retrieval miss、insufficient evidence、temporal conflict 與 generation failure 全部當成「再檢索一次」。

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
| D14 | [[02 - 研究領域專題 (Research Domains)/Domain 14 - RAG Systems & Reliability|RAG Systems & Reliability]] |

## Related

- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|RAG Research Taxonomy]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Paradigm Tags|Paradigm Tags]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|Adjacent Interfaces]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Benchmark Catalog|Benchmark Catalog]]
