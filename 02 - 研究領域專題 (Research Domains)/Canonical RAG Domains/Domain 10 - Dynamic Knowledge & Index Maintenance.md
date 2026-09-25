---
title: "Domain 10 - Dynamic Knowledge & Index Maintenance"
domain_id: "D10"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Cross-Lifecycle"
migration_status: "scaffold"
last_updated: "2026-09-25"
---

# Domain 10 - Dynamic Knowledge & Index Maintenance

> [!IMPORTANT] Canonical Domain v2
> 本頁依「RAG lifecycle 中的研究問題」分類。GraphRAG、Hierarchical RAG、Adaptive RAG、Agentic RAG、Multimodal RAG 等不再與 lifecycle Domain 平行，而以 paradigm tags 管理。
> 目前為 migration scaffold；舊 Domain 尚未刪除。

## Core Question
外部知識新增、修改、刪除或失效時，RAG index 如何正確且低成本地維護？

## Includes
- incremental indexing
- insert / update / delete semantics
- staleness detection
- embedding refresh
- entity resolution across versions
- graph / community / summary recomputation
- version-aware retrieval

## Excludes
- conversation memory → D11
- evidence conflict resolution → D08

## Classification Rules
- 一篇論文可跨多個 Domain，但必須指定一個 Primary Domain。
- 其餘影響層級列為 Secondary Domains。
- 架構型名稱使用 paradigm tags，而非新增 top-level Domain。
- 尚未由既有文獻直接支持的完整方法組合放入 `04 - 研究想法與待驗證提案`。

## Navigation
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|Canonical Taxonomy v2]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Paradigm Tags|RAG Paradigm Tags]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/Canonical RAG Domain Migration Map|Migration Map]]
