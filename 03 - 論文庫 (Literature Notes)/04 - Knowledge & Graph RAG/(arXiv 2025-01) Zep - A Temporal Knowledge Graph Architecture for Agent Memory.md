---
paper_id: "Rasmussen2025_Zep"
title: "Zep: A Temporal Knowledge Graph Architecture for Agent Memory"
authors: ["Preston Rasmussen", "Pavlo Paliychuk", "Travis Beauvais", "Jack Ryan", "Daniel Chalef"]
year: 2025
publication_year: null
venue: "arXiv"
doi: null
arxiv: "2501.13956"
url: "https://arxiv.org/abs/2501.13956"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(arXiv 2025-01) Zep - A Temporal Knowledge Graph Architecture for Agent Memory.pdf"
tags: ["paper", "agent-memory", "temporal-knowledge-graph"]
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D11"
primary_domain: "D11"
secondary_domains: ["D04", "D05"]
paradigm_tags: ["memory_augmented_rag"]
adjacent_interfaces: []
research_questions: ["persistent_memory", "temporal_fact_validity", "memory_retrieval"]
benchmark_ids: ["Deep Memory Retrieval", "LongMemEval"]
dataset_ids: ["Multi-Session Chat subset", "LongMemEval-s"]
metrics: ["accuracy", "latency", "context tokens"]
---

# Zep: A Temporal Knowledge Graph Architecture for Agent Memory

> **版本：** arXiv v1，2025-01-20；本地 PDF 是該預印本全文。正式出版版本尚未核得。Zep 與其核心 Graphiti 是本文同一工作，不另計兩篇。

## 一話摘要 (TL;DR)
Zep 以 Graphiti 動態維護 episode、semantic entity、community 子圖及雙時間 edge，供 agent 保存、更新並檢索對話和結構化資料。

## 研究背景與問題定義 (Problem Statement)
靜態文件檢索難以處理對話和業務資料持續新增、事實更新及歷史關係變化。本文提出面向 agent memory 的服務架構，不是一般文件 GraphRAG 的通用比較。[§1–2, pp. 1–4]

## 核心方法與技術架構 (Methodology & Architecture)
Graphiti 用 episode 子圖記錄來源事件、semantic subgraph 表示 entities/facts、community subgraph 儲存摘要。Edges 同時記錄 valid-time 與 transaction-time；新事實若與時間重疊的 edge 矛盾，可令舊 edge 在相應時間失效。檢索融合 cosine、BM25、BFS，並可用 RRF/MMR、mention count、node distance 或 cross-encoder rerank；context constructor 輸出 facts、有效時間與 entity/community summaries。[§2–3, pp. 2–5]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, p. 6：** DMR 500 個對話子集上，GPT-4-turbo 設定的 Zep accuracy 94.8%、MemGPT 文獻報告 93.4%、full-conversation 94.4%；作者指出每段約 60 則訊息，現代 context window 可容納，故此 benchmark 區辨力有限。
- **Table 2, p. 7：** LongMemEval-s 平均約 115K tokens。GPT-4o-mini full-context 55.4% / 31.3s / 115K tokens，Zep 63.8% / 3.20s / 1.6K；GPT-4o full-context 60.2% / 28.9s / 115K，Zep 71.2% / 2.58s / 1.6K。
- **設定：** Graph construction 用 gpt-4o-mini-2024-07-18；embedding/reranking 用 BGE-M3；回答用 GPT-4o-mini 或 GPT-4o。測試在 2024-12 至 2025-01 執行，Zep service 位於 AWS us-west-2；baseline 沒有相同網路路徑，latency 條件不對稱。[§4, pp. 5–7]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 雙時間 edge 保存目前狀態與歷史變化；多路召回整合文字、語意與圖距離線索；長對話實驗顯示 context token 可大幅減少。
- **限制：** 社群增量更新採 label propagation heuristic，作者指出社群會逐漸偏離完整重算結果，仍需週期 refresh。DMR 是短對話單輪事實題；LongMemEval 的 MemGPT 直接復現未成功；本文未測全部 Graphiti 功能或 Zep 與結構化 business data 的聯合 benchmark。[§2.3、§4–5, pp. 4–8]
- **比較邊界：** latency 包含 Zep 雲端網路路徑而 baseline 不同；需連同架構條件解讀。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將 Zep 歸於 **D11 Persistent Memory Management**，次領域 D04、D05；使用 `memory_augmented_rag`。對話記憶更新不自動等於外部 source synchronization。本文補足對話／事件型圖記憶與有效時間查詢案例。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [arXiv:2501.13956 v1](https://arxiv.org/abs/2501.13956)；[PDF](https://arxiv.org/pdf/2501.13956)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(arXiv 2025-01) Zep - A Temporal Knowledge Graph Architecture for Agent Memory.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2024-12) HippoRAG - Neurobiologically Inspired Long-Term Memory for Large Language Models|HippoRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICML 2025-07) From RAG to Memory - Non-Parametric Continual Learning for Large Language Models|HippoRAG 2]]。
