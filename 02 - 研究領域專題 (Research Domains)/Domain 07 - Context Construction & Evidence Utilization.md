---
title: "Domain 07 - Context Construction & Utilization"
domain_id: "D07"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Post-Retrieval"
last_updated: "2026-09-27"
---

# Domain 07 - Context Construction & Utilization

> [!WARNING]
> **Phase 1 closure is authoritative.** 若本頁較早段落與底部「Phase 1 Closure — 2026-09-27」衝突，以 closure 為準；舊文字暫留作 Phase 2 forensic audit，將於 Phase 7 一次正規化。

## Core Question
候選 evidence 已取得後，如何在有限有效的 context budget 中進行選擇、去重、壓縮、排序與配置，並使模型可靠利用關鍵資訊？

## Includes
- post-retrieval context selection / deduplication
- RAG-specific evidence compression
- context packing and token-budget allocation
- evidence ordering / position-aware allocation
- distractor handling and retrieved-context utilization

## Excludes
- relevance reranking → D05
- generic prompt / KV compression → A02
- parametric-vs-retrieved factual conflict → D08
- citation / claim support generation → D09
- generic security robustness → D14

## Level-2 Topics
- Post-Retrieval Context Selection
- Context Compression
- Context Packing & Budget Allocation
- Ordering & Position
- Retrieved-Context Utilization

## Boundary
D05 問「哪些候選較相關？」；D07 問「哪些內容值得真正佔據有限 prompt budget，以及模型是否能有效使用它們？」。Knowledge conflict 不屬 D07，應進 D08。

## Representative Notes

**Current primary-note coverage: 5**

- [[03 - 論文庫 (Literature Notes)/02 - Compression & KV Cache/(ICLR 2024-05) RECOMP - Improving Retrieval-Augmented LMs with Compression and Selective Augmentation|RECOMP]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(EMNLP 2024-11) Chain-of-Note - Enhancing Robustness in Retrieval-Augmented Language Models|Chain-of-Note]]

## Failure Modes Retained from Earlier Synthesis

這些是 D07 要保留的診斷視角：
- **Position bias / Lost in the Middle**：evidence 已進 context，但位置造成利用率下降。
- **Distractor vulnerability**：高相似但錯誤或無關 evidence 稀釋關鍵資訊。
- **Parametric-prior conflict**：模型偏向內部參數知識，而忽略更新後的 retrieved evidence。
- **Packing failure**：正確 evidence 被排序、截斷或壓縮方式破壞。

這些 failure 與 D05 retrieval miss 不同：**Gold evidence 已存在於候選或 final context 時，錯誤不能再全部歸咎於 retriever。**



> [!NOTE]
> [[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(TACL 2024-01) Lost in the Middle - How Language Models Use Long Contexts|Lost in the Middle]] is an A01 long-context evaluation anchor with D07/D13 relevance, not a RAG-specific D07-primary method.

## Navigation
- [[02 - 研究領域專題 (Research Domains)/Domain 06 - Evidence Sufficiency & Adaptive Retrieval|D06 Evidence Sufficiency & Adaptive Retrieval]]
- [[02 - 研究領域專題 (Research Domains)/Domain 09 - Grounded Generation Attribution & Long-form Synthesis|D09 Grounded Generation & Long-form Synthesis]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|RAG Adjacent Interfaces]]

## Phase 1 Closure — 2026-09-27

> [!IMPORTANT]
> **Canonical name: D07 Context Construction & Utilization.**

**Core question**：候選 evidence 已取得後，如何在有限有效的 context budget 中進行選擇、去重、壓縮、排序與配置，並使模型可靠利用關鍵資訊？

**Canonical Level-2**
- Post-Retrieval Context Selection / deduplication
- RAG-specific Context Compression
- Context Packing & Budget Allocation
- Ordering & Position
- Retrieved-Context Utilization / distractor sensitivity

**Hard boundary**
- relevance reranking → D05
- generic prompt/KV compression → A02
- parametric-vs-retrieved factual conflict → D08
- citation / claim support in output → D09
- generic noise/security robustness is not automatically D14; distractor use in supplied context can be D07

**Paper decisions**
- RECOMP: KEEP D07.
- Chain-of-Note: KEEP D07; D06 secondary; update DOI to `10.18653/v1/2024.emnlp-main.813`.
- SARA (ACL 2026): ADD.
- The Distracting Effect (ACL 2025): ADD.
- Attention Basin / AttnRank (ACL 2026): ADD.
- LongLLMLingua and Selective Context remain A02 with D07 interface.
- Lost in the Middle remains A01 / D07+D13 interface.
