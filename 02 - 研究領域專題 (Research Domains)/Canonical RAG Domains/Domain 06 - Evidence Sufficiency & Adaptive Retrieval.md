---
title: "Domain 06 - Evidence Sufficiency & Adaptive Retrieval"
domain_id: "D06"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Retrieval Control"
migration_status: "scaffold"
last_updated: "2026-09-25"
---

# Domain 06 - Evidence Sufficiency & Adaptive Retrieval

> [!IMPORTANT] Canonical Domain v2
> 本頁依「RAG lifecycle 中的研究問題」分類。GraphRAG、Hierarchical RAG、Adaptive RAG、Agentic RAG、Multimodal RAG 等不再與 lifecycle Domain 平行，而以 paradigm tags 管理。
> 目前為 migration scaffold；舊 Domain 尚未刪除。

## Core Question
目前 evidence 是否足以回答問題；若不足，缺什麼、下一個 retrieval action 是什麼、何時停止？

## Includes
- retrieval necessity
- evidence coverage / completeness / sufficiency
- gap localization
- adaptive / corrective / iterative retrieval
- stopping policy
- retrieval-time abstention / escalation

## Excludes
- general relevance ranking → D05
- conflict / time / source resolution → D08
- general agent orchestration → D12

## Classification Rules
- 一篇論文可跨多個 Domain，但必須指定一個 Primary Domain。
- 其餘影響層級列為 Secondary Domains。
- 架構型名稱使用 paradigm tags，而非新增 top-level Domain。
- 尚未由既有文獻直接支持的完整方法組合放入 `04 - 研究想法與待驗證提案`。

## Navigation
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|Canonical Taxonomy v2]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Paradigm Tags|RAG Paradigm Tags]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/Canonical RAG Domain Migration Map|Migration Map]]
