# Research Domains — Canonical Taxonomy v2

> [!IMPORTANT] 唯一正式計數
> **目前只有 14 個 Canonical RAG Domains（D01–D14）。**

## 為什麼資料夾裡還看得到 17 個 Domain？

根目錄既有的 `Domain 01 ... Domain 17` 是 **Legacy Taxonomy**。因為大量 Literature Notes、MOC 與 Obsidian backlinks 仍指向它們，所以在遷移完成前不直接刪除。

它們的存在 **不代表目前有 17 個 canonical domains**。

Canonical pages 位於：

`02 - 研究領域專題 (Research Domains)/Canonical RAG Domains/`

## 那 32 topics 是什麼？

32 是舊版 Research Taxonomy Map 裡的 **Level-2 research topics inventory**，例如 Chunking、Query Decomposition、Evidence Sufficiency、Citation 等。

它們不是 32 個 top-level domains。新版會把這些 topics 放回 D01–D14 內，或在必要時改成 paradigm tag / adjacent interface。

## 現行四層結構

```text
RAG-survey taxonomy
├── 14 Canonical Domains (D01–D14)       ← top-level research problems
├── Level-2 Topics                        ← chunking, reranking, sufficiency...
├── Paradigm Tags                         ← GraphRAG, Hierarchical RAG, Agentic RAG...
└── 5 Adjacent Interfaces (A01–A05)       ← Long Context, KV Cache, General Agents...
```

## Canonical Domains

1. D01 Document Ingestion & Structure
2. D02 Segmentation & Contextualization
3. D03 Knowledge Extraction & Information Preservation
4. D04 Knowledge Representation & Indexing
5. D05 Query Understanding & Retrieval
6. D06 Evidence Sufficiency & Adaptive Retrieval
7. D07 Context Construction & Evidence Utilization
8. D08 Temporal Conflict & Provenance Resolution
9. D09 Grounded Generation, Attribution & Long-form Synthesis
10. D10 Dynamic Knowledge & Index Maintenance
11. D11 Memory-Augmented RAG
12. D12 Agentic RAG & Orchestration
13. D13 RAG Evaluation & Failure Attribution
14. D14 RAG Systems, Robustness & Security

## Migration progress

- ✅ 125 paper notes 已加入 Taxonomy v2 YAML mapping。
- ✅ Legacy Domain 04 已拆到 D02 / D03。
- ⏳ 其他 legacy pages 仍待內容搬移、Wikilink 修復與 archive。

## Navigation

- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|Canonical Taxonomy v2]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Paradigm Tags|RAG Paradigm Tags]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|Adjacent Interfaces]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/Paper Domain Migration Manifest|Paper Migration Manifest]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/Canonical RAG Domain Migration Map|Legacy Migration Map]]
