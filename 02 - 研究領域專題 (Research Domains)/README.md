# Research Domains

> [!IMPORTANT]
> 本資料夾就是目前唯一正式的 RAG taxonomy：**14 個 Research Domains（D01–D14）**。

## Structure

```text
Research Domains
├── D01 Document Parsing & Structure Recovery
├── D02 Segmentation & Retrieval Granularity
├── D03 Knowledge Extraction & Consolidation
├── D04 Representation & Indexing
├── D05 Query Understanding & Retrieval
├── D06 Evidence Sufficiency & Retrieval Control
├── D07 Context Construction & Utilization
├── D08 Evidence Reconciliation
├── D09 Grounded Generation & Long-form Synthesis
├── D10 Knowledge & Index Maintenance
├── D11 Persistent Memory Management
├── D12 RAG Orchestration & Action Control
├── D13 Evaluation & Failure Attribution
└── D14 RAG Systems, Security & Privacy
```

## Domain Index

- [[02 - 研究領域專題 (Research Domains)/Domain 01 - Document Ingestion & Structure|D01 Document Parsing & Structure Recovery]]
- [[02 - 研究領域專題 (Research Domains)/Domain 02 - Segmentation & Contextualization|D02 Segmentation & Retrieval Granularity]]
- [[02 - 研究領域專題 (Research Domains)/Domain 03 - Knowledge Extraction & Information Preservation|D03 Knowledge Extraction & Consolidation]]
- [[02 - 研究領域專題 (Research Domains)/Domain 04 - Knowledge Representation & Indexing|D04 Representation & Indexing]]
- [[02 - 研究領域專題 (Research Domains)/Domain 05 - Query Understanding & Retrieval|D05 Query Understanding & Retrieval]]
- [[02 - 研究領域專題 (Research Domains)/Domain 06 - Evidence Sufficiency & Adaptive Retrieval|D06 Evidence Sufficiency & Retrieval Control]]
- [[02 - 研究領域專題 (Research Domains)/Domain 07 - Context Construction & Evidence Utilization|D07 Context Construction & Utilization]]
- [[02 - 研究領域專題 (Research Domains)/Domain 08 - Temporal Conflict & Provenance Resolution|D08 Evidence Reconciliation]]
- [[02 - 研究領域專題 (Research Domains)/Domain 09 - Grounded Generation Attribution & Long-form Synthesis|D09 Grounded Generation & Long-form Synthesis]]
- [[02 - 研究領域專題 (Research Domains)/Domain 10 - Dynamic Knowledge & Index Maintenance|D10 Knowledge & Index Maintenance]]
- [[02 - 研究領域專題 (Research Domains)/Domain 11 - Memory-Augmented RAG|D11 Persistent Memory Management]]
- [[02 - 研究領域專題 (Research Domains)/Domain 12 - Agentic RAG & Orchestration|D12 RAG Orchestration & Action Control]]
- [[02 - 研究領域專題 (Research Domains)/Domain 13 - RAG Evaluation & Failure Attribution|D13 Evaluation & Failure Attribution]]
- [[02 - 研究領域專題 (Research Domains)/Domain 14 - RAG Systems, Robustness & Security|D14 RAG Systems, Security & Privacy]]

## Other Axes

- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Paradigm Tags|Paradigm Tags]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|Adjacent Interfaces]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|Taxonomy & Domain Map]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Benchmark Catalog|Benchmark Catalog]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/Survey Papers Index|Survey Papers Index]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/技術全景與 Pareto 權衡分析 (Trade-offs)|技術全景與 Pareto 權衡分析 (Trade-offs)]]

## Literature Coverage Snapshot

> [!NOTE]
> 下表是 **2026-10-02 的 metadata 重算快照**：209 份含 `paper_id` 的 literature notes 中，155 份有 D01–D14 `primary_domain`，54 份為 Adjacent/CROSS。只計 primary；secondary 關聯、摘要候選與 UIE 簡報工件不計入。這是筆記數量，並非已驗證方法數或領域重要性排序；新增／移動 paper 後需重新計算。

| Domain | Primary notes |
|---|---:|
| D01 | 5 |
| D02 | 5 |
| D03 | 19 |
| D04 | 12 |
| D05 | 36 |
| D06 | 7 |
| D07 | 6 |
| D08 | 9 |
| D09 | 8 |
| D10 | 1 |
| D11 | 8 |
| D12 | 8 |
| D13 | 22 |
| D14 | 9 |

> Duplicate cleanup queue 詳見 [[00 - 導覽與心智圖 (Navigation & MOC)/Phase 1 Taxonomy Closure Audit - 2026-09-27#12. Phase 3 Duplicate Cleanup Queue|Phase 1 Audit — Duplicate Cleanup Queue]]。

目前的 coverage gap 應以 Level-2 research question 處理，而不是再增加 Domain：
- **D01**：RAG-specific parsing／structure recovery 的專門 survey coverage 仍需補核；Huang 的 pre-retrieval 概述不代替專門 survey。
- **D03**：entity linking／event argument extraction 的新候選尚待全文核實；information-preserving extraction 的整體壓力測試仍屬研究提案。
- **D06**：retrieval control、evidence-set sufficiency 與 answer-risk calibration 分開管理；完整 gap controller 仍屬 Idea 02。
- **D08**：provenance lineage / approval-state / applicability-scope governance 仍薄。
- **D10**：production CRUD / deletion propagation / dependency-aware invalidation 仍薄。
- **D11**：forgetting / invalidation / governance 比 write-retrieve-memory literature 薄。
- **D14**：observability/tracing、tenant isolation、derived-data deletion/privacy governance 仍薄。

## Phase 1 Canonical Names — 2026-09-27

The canonical display names above are authoritative after Phase 1 closure. Existing filenames remain unchanged until Phase 7 path normalization.

Key cleanup outcomes:
- D03 preservation is a quality lens; canonical research problem is extraction + consolidation.
- D08 is restored to general evidence reconciliation instead of temporal-only scope.
- D11 is defined by persistent derived-state lifecycle, not the word “memory”.
- D12 is defined by state→action orchestration, not by whether a system uses agents.
- D14 no longer uses generic robustness as a catch-all; adversarial integrity/security remains in D14 while ordinary distractor/context robustness is assigned to the relevant lifecycle domain.

## D01–D06 Classification Refresh — 2026-10-02

- D01：分開表格偵測／結構／功能角色與公式轉寫。
- D02：分開 indexed／retrieved／reader-context units，明定 query-adaptive 粒度的 D02/D04/D05/D07 分工。
- D03：分開 entity recognition／coreference／linking 與 event trigger／argument roles／inter-event relations。
- D04：以 unit × encoding × index organization 整理；semantic graph 與 ANN neighbor graph 分開。
- D05：以 query transformation 及 alignment signal／trained module 比較方法；reranking 依問題仍屬 D05。
- D06：以 trigger timing × signal × decision 整理；停止取證、充分性與統計 coverage 分開。
- Huang 2404.10981 收為 CROSS survey，已核 2024 v2 內容與 2026 正式書目；全文版本與 coverage 對照集中見 [[00 - 導覽與心智圖 (Navigation & MOC)/Survey Papers Index|Survey Papers Index]]。

## Audit Trail
- [[00 - 導覽與心智圖 (Navigation & MOC)/Phase 1 Taxonomy Closure Audit - 2026-09-27|Phase 1 Taxonomy Closure Audit]]
