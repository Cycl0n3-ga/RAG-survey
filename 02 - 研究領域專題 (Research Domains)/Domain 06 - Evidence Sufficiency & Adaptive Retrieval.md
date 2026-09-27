---
title: "Domain 06 - Evidence Sufficiency & Retrieval Control"
domain_id: "D06"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Retrieval Control"
last_updated: "2026-09-27"
---

# Domain 06 - Evidence Sufficiency & Retrieval Control

> [!WARNING]
> **Phase 1 closure is authoritative.** 若本頁較早段落與底部「Phase 1 Closure — 2026-09-27」衝突，以 closure 為準；舊文字暫留作 Phase 2 forensic audit，將於 Phase 7 一次正規化。

## Core Question
目前 evidence 是否已足以支持回答；若不足，系統應繼續檢索、切換檢索策略、拒答，還是停止？

## Includes
- retrieval necessity / retrieve-vs-no-retrieve
- sufficient-context / evidence-set sufficiency
- retry / corrective / iterative retrieval control
- strategy escalation and stopping
- evidence-gap diagnosis
- evidence-conditioned abstention / selective answering

## Excludes
- relevance ranking / which documents to retrieve → D05
- conflict adjudication / which incompatible evidence wins → D08
- general action/tool orchestration → D12
- evaluation-only sufficiency benchmark → D13

## Two Research Tracks
1. **Evidence Sufficiency**：current evidence set 是否足以回答。
2. **Retrieval Control**：根據 evidence state 決定 retrieve / retry / change strategy / stop / abstain。

## Level-2 Topics
- Retrieval Necessity
- Evidence Sufficiency
- Retrieval Control
- Evidence Gap Diagnosis
- Selective Answering

## Boundary
`Relevance != Sufficiency`。衝突可使 evidence 被判為 insufficient，但真正的 conflict resolution 屬 D08。Explicit requirement-slot decomposition → gap localization → targeted retrieval 仍屬 emerging/project hypothesis。

## Representative Notes

**Current primary-note coverage: 6**

- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(EMNLP 2023-12) Active Retrieval Augmented Generation|FLARE / Active Retrieval]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(ICLR 2024-05) Self-RAG - Learning to Retrieve, Generate, and Critique through Self-Reflection|Self-RAG]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(NAACL 2024-06) Adaptive-RAG - Learning to Adapt Retrieval-Augmented Large Language Models through Question Complexity|Adaptive-RAG]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(arXiv 2024-01) Corrective Retrieval Augmented Generation|CRAG / Corrective RAG]]

## Failure Modes
- **False-sufficient**：背景文字很多，但關鍵 evidence slot 仍缺失，controller 卻提前停止。
- **Infinite retrieval loop**：corpus 根本沒有答案時持續 rewrite / retrieve，直到耗盡 budget。
- **Hyper-conservative abstention**：非關鍵欄位稍有缺失就拒答，造成可回答問題被過度攔截。
- **Cost-blind adaptation**：adaptive controller accuracy 稍升，但額外 LLM/retrieval cost 大於收益。

因此 D06 必須同時報 correctness、abstention 與 retrieval/token/latency budget。

## Navigation
- [[02 - 研究領域專題 (Research Domains)/Domain 05 - Query Understanding & Retrieval|D05 Query Understanding & Retrieval]]
- [[02 - 研究領域專題 (Research Domains)/Domain 07 - Context Construction & Evidence Utilization|D07 Context Construction & Evidence Utilization]]
- [[02 - 研究領域專題 (Research Domains)/Domain 12 - Agentic RAG & Orchestration|D12 Agentic RAG & Orchestration]]

## Phase 1 Closure — 2026-09-27

> [!IMPORTANT]
> **Canonical name: D06 Evidence Sufficiency & Retrieval Control.**
> `adaptive_rag`, `corrective_rag`, and `reflective_rag` are paradigms/method families, not Domain names.

**Core question**：目前 evidence 是否已足以支持回答；若不足，系統應繼續檢索、切換策略、拒答，還是停止？

**Canonical Level-2**
- Retrieval Necessity
- Evidence Sufficiency / Sufficient Context
- Retrieval Control: retry / corrective / escalation / stopping
- Evidence Gap Diagnosis
- Selective Answering / evidence-conditioned abstention

**Hard boundary**
- D05 decides *what* to retrieve.
- D06 decides whether retrieval is needed, whether current evidence is enough, and whether to continue/stop.
- conflict detection may make evidence insufficient; conflict resolution belongs D08.
- explicit requirement-slot decomposition → gap localization → targeted retrieval remains a project hypothesis / emerging line.

**Paper decisions**
- FLARE: KEEP D06.
- Adaptive-RAG: KEEP D06; remove D05 secondary.
- Self-RAG: KEEP D06 / D09 secondary.
- CRAG: KEEP D06 / D07 secondary; remove D05/D12.
- Sufficient Context (ICLR 2025): ADD as canonical direct sufficiency anchor.
- Evidence Sufficiency Benchmark 2026: D13 primary / D06 secondary.
- SURE-RAG 2026: emerging preprint.
