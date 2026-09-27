---
title: "Domain 09 - Grounded Generation & Long-form Synthesis"
domain_id: "D09"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Generation"
last_updated: "2026-09-27"
---

# Domain 09 - Grounded Generation & Long-form Synthesis

> [!WARNING]
> **Phase 1 closure is authoritative.** 若本頁較早段落與底部「Phase 1 Closure — 2026-09-27」衝突，以 closure 為準；舊文字暫留作 Phase 2 forensic audit，將於 Phase 7 一次正規化。

## Core Question
如何從已取得的 evidence 產生其 claims 可被支持、可追溯的答案或長篇 synthesis，並在生成過程中發現 unsupported content 時進行 revision、citation 或 selective abstention？

## Includes
- evidence-conditioned grounded answer generation
- claim→evidence attribution / citation generation
- unsupported-claim detection and revision
- selective abstention
- outline / section planning
- multi-source long-form synthesis
- cross-section revision and consistency

## Excludes
- whether evidence is sufficient → D06
- context selection / compression / packing → D07
- benchmark / metric-only evaluation → D13
- general action/tool orchestration → D12

## Level-2 Topics
- Grounded Answer Generation
- Attribution & Citation
- Verification & Revision
- Selective Abstention
- Long-form Evidence Synthesis

## Boundary
D06：是否夠證據；D09：在已給 evidence 下生成可支持輸出。Generation-time verifier 若會修改／重寫輸出屬 D09；若只做 scoring / benchmark 則屬 D13。

## Representative Notes

**Current primary-note coverage: 8**

- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(NAACL 2024-06) Assisting in Writing Wikipedia-like Articles From Scratch with Large Language Models|STORM]]
- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(arXiv 2024-11) OpenScholar - Synthesizing Scientific Literature with Retrieval-Augmented Language Models|OpenScholar]]
- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(ACL 2026-08) EviReport - From Reasoned Outlines to Evidence Tracked Long-Form Reports|EviReport]]
- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(ACL 2026-08) EFSG - Evidence-First Structured Generation for Multilingual RAG Report Generation|EFSG]]
- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(arXiv 2022-03) Teaching language models to support answers with verified quotes|GopherCite]]

## Long-form Orchestration Patterns

長篇生成至少有三種不同 orchestration pattern，不能全部叫「一次生成」：

1. **Outline-first / research-first**：先研究與建立大綱，再依 section 對應 evidence 撰寫；STORM 是代表工作。
2. **Evidence-first fixed pool**：生成前先整理/封存 evidence pool，再從固定證據寫作；適合強調 auditability 的設計。
3. **Gap-aware iterative writing**：寫作或規劃過程發現 coverage gap 時再追加 retrieval；EviReport 類工作靠近這一路線。

### Generic long-document synthesis patterns

早期/通用 long-document pipeline 常見 **Map-Reduce、Refine、tree-search / Tree-of-Thought-like orchestration**。這些可以用於 summarization / synthesis，但本身不是 RAG-specific Domain；只有在它們與 evidence retrieval、citation、verification 或 gap-aware control 結合時，才進入 D09/D12 的研究範圍。

### Evidence Store 與 Claim-Evidence Ledger

- **Evidence Store**：一個可選的系統設計，用穩定 evidence ID、source span、provenance 保存可引用證據；不是所有長文方法的必要條件。
- **Claim-Evidence Ledger**：project-specific 可審計機制，將 generated claim 對應 supporting / contradicting evidence、verification status 與 section。其 canonical 定義放在 [[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/Idea 04 - End-to-End RAG Failure Attribution and Evidence Governance|Idea 04]]。
- fixed evidence pool 與 iterative retrieval 應作為可比較的設計選擇，而非先驗宣稱其中一種必然較好。



> [!NOTE]
> [[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(EMNLP 2023-12) Enabling Large Language Models to Generate Text with Citations|ALCE]] contributes citation evaluation benchmarks/metrics, so it is D13-primary with D09 secondary relevance.

## Navigation
- [[02 - 研究領域專題 (Research Domains)/Domain 07 - Context Construction & Evidence Utilization|D07 Context Construction & Evidence Utilization]]
- [[02 - 研究領域專題 (Research Domains)/Domain 13 - RAG Evaluation & Failure Attribution|D13 RAG Evaluation & Failure Attribution]]

## Phase 1 Closure — 2026-09-27

> [!IMPORTANT]
> **Canonical name: D09 Grounded Generation & Long-form Synthesis.**

**Core question**：如何從已取得的 evidence 產生其 claims 可被支持、可追溯的答案或長篇 synthesis，並在生成過程中發現 unsupported content 時進行 revision、citation 或 selective abstention？

**Canonical Level-2**
- Grounded Answer Generation
- Attribution & Citation
- Verification & Revision
- Selective Abstention
- Long-form Evidence Synthesis: outline / section planning / multi-source synthesis / cross-section revision

**Hard boundary**
- D06: is evidence enough?
- D07: what context reaches the generator?
- D09: given evidence/context, produce supported output.
- D13: evaluate/score output rather than generate/repair it.
- D12: action/tool orchestration; multi-stage writing alone is not automatically agentic.

**Paper decisions**
- KEEP GopherCite, STORM, OpenScholar, EviReport, EFSG.
- STORM: fix DOI `10.18653/v1/2024.naacl-long.347`; remove unsupported headline win-rate claims.
- OpenScholar: remove D12/`agentic_rag` unless stronger action-policy evidence is documented.
- EviReport: keep D09; remove unsupported Source Hash / Evidence Ledger / “38% gap recovery” claims unless verified.
- EFSG: high-priority rewrite; current repo metrics overclaim shared-task performance.
- ADD RARR (ACL 2023) and RioRAG (ACL 2026).
- Claim–Evidence Ledger remains project Idea 04, not an established paper mechanism.
