---
title: "Domain 14 - RAG Systems Robustness & Security"
domain_id: "D14"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Deployment"
migration_status: "scaffold"
last_updated: "2026-09-25"
---

# Domain 14 - RAG Systems Robustness & Security

> [!IMPORTANT] Canonical Domain v2
> 本頁依「RAG lifecycle 中的研究問題」分類。GraphRAG、Hierarchical RAG、Adaptive RAG、Agentic RAG、Multimodal RAG 等不再與 lifecycle Domain 平行，而以 paradigm tags 管理。
> 目前為 migration scaffold；舊 Domain 尚未刪除。

## Core Question
如何在真實部署下控制成本、延遲、可觀測性與攻擊面，並維持 RAG 可靠性？

## Includes
- latency / throughput / cost
- indexing / serving scalability
- cache / batching
- observability
- privacy / access control
- retrieval / corpus poisoning
- prompt injection through retrieved content
- noise / adversarial robustness

## Excludes
- 純 LLM inference architecture → Adjacent Interface
- benchmark methodology → D13

## Classification Rules
- 一篇論文可跨多個 Domain，但必須指定一個 Primary Domain。
- 其餘影響層級列為 Secondary Domains。
- 架構型名稱使用 paradigm tags，而非新增 top-level Domain。
- 尚未由既有文獻直接支持的完整方法組合放入 `04 - 研究想法與待驗證提案`。

## Navigation
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|Canonical Taxonomy v2]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Paradigm Tags|RAG Paradigm Tags]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/Canonical RAG Domain Migration Map|Migration Map]]
