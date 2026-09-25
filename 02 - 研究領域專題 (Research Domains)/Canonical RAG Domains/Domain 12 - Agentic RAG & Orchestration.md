---
title: "Domain 12 - Agentic RAG & Orchestration"
domain_id: "D12"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Cross-Lifecycle Control"
last_updated: "2026-09-25"
---

# Domain 12 - Agentic RAG & Orchestration

> [!IMPORTANT]
> 本頁依「RAG lifecycle 中的研究問題」分類。GraphRAG、Hierarchical RAG、Adaptive RAG、Agentic RAG、Multimodal RAG 等不再與 lifecycle Domain 平行，而以 paradigm tags 管理。

## Core Question
系統如何根據 state 自主選擇下一個 RAG action、工具、資料源或子任務？

## Includes
- planning / routing
- tool use
- controller / policy
- multi-agent coordination
- research workflow orchestration
- iterative search-think-act loops

## Excludes
- 只有 adaptive retriever → D06
- 純 reasoning tree（非 RAG）
- 單一 retriever architecture → D05

## Classification Rules
- 一篇論文可跨多個 Domain，但必須指定一個 Primary Domain。
- 其餘影響層級列為 Secondary Domains。
- 架構型名稱使用 paradigm tags，而非新增 top-level Domain。
- 尚未由既有文獻直接支持的完整方法組合放入 `04 - 研究想法與待驗證提案`。

## Navigation
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|Canonical Taxonomy v2]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Paradigm Tags|RAG Paradigm Tags]]
