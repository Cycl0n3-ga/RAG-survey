---
paper_id: "Li2025_StructRAG"
title: "StructRAG: Boosting Knowledge Intensive Reasoning of LLMs via Inference-time Hybrid Information Structurization"
authors: ["Zhuoqun Li", "Xuanang Chen", "Haiyang Yu", "Hongyu Lin", "Yaojie Lu", "Qiaoyu Tang", "Fei Huang", "Xianpei Han", "Le Sun", "Yongbin Li"]
year: 2024
publication_year: 2025
venue: "ICLR 2025"
doi: null
arxiv: "2410.08815"
url: "https://proceedings.iclr.cc/paper_files/paper/2025/hash/5975754c7650dfee0682e06e1fec0522-Abstract-Conference.html"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(ICLR 2025-05) StructRAG - Boosting Knowledge Intensive Reasoning of LLMs via Inference-time Hybrid Information Structurization.pdf"
tags: ["paper", "context-structurization", "task-conditioned-routing"]
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D07"
primary_domain: "D07"
secondary_domains: ["D03", "D05"]
paradigm_tags: []
adjacent_interfaces: []
research_questions: ["context_construction", "task_conditioned_structure_selection", "knowledge_utilization"]
benchmark_ids: ["Loong", "Podcast Transcripts evaluation"]
dataset_ids: ["Loong", "Podcast Transcripts"]
metrics: ["LLM-judged score", "Exact Match", "LLM-judge win rate"]
source_version: ICLR 2025 proceedings
verified_version: ICLR 2025 proceedings
pdf_pages: 18
pdf_sha256: 99471b7e33b4aecb028b77405d38c902e55599082eff7c28bb2cc8cbb550b2a2
---

# StructRAG: Boosting Knowledge Intensive Reasoning of LLMs via Inference-time Hybrid Information Structurization

> **版本：** arXiv 預印本於 2024 年發布；本地 PDF 為 ICLR 2025 正式版。

## 一話摘要 (TL;DR)
StructRAG 依任務選擇 table、graph、algorithm、catalogue 或 chunk 等知識結構，重組散落文件資訊後再回答。

## 研究背景與問題定義 (Problem Statement)
長文件與知識密集任務中的答案線索可能散落在多處，固定 chunk 檢索可能漏掉關鍵資訊或帶入雜訊。本文研究 inference-time 任務條件化結構化；graph 是候選格式之一，而非所有輸入都轉成圖。[§1–3, pp. 1–4]

## 核心方法與技術架構 (Methodology & Architecture)
Hybrid Structure Router 決定當前任務適合的結構；Scattered Knowledge Structurizer 把文件重組為所選結構；Structured Knowledge Utilizer 將複合問題拆成子問題並從結構化內容取證回答。Router 以 Qwen2-7B-Instruct 和合成 preference data 做 DPO；另外兩個模組使用 Qwen2-72B-Instruct。[§3, pp. 3–5；§5.1, p. 6]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, p. 7：** Loong 四種任務、四種文件長度組，以 LLM score 及 exact match 評估。StructRAG overall 為 60.38 / 0.23；最長文件 Set 4 為 51.42 / 0.10。作者報告較長組的相對改善較大。
- **Table 2, p. 7：** Podcast Transcripts 的 LLM head-to-head win rate 中，StructRAG 對 GraphRAG 平均為 53.00%；comprehensiveness、diversity、empowerment、directness 分別 61、68、42、41。
- **Table 3, p. 8：** 移除 router、structurizer、utilizer 後 overall LLM score 由 60.38 降至 45.33、53.92、55.94。
- **資源：** Router 是 Qwen2-7B-Instruct，使用 900 preference pairs、3 epochs；結構化與回答模組用 Qwen2-72B-Instruct。平均 latency 報為 StructRAG 9.7 分鐘、RQ-RAG 9.0 分鐘、GraphRAG 217.1 分鐘；未列硬體，不能視為硬體無關成本。[§5, pp. 6–9]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 不把 graph 當所有任務的固定結構；消融與固定單一結構實驗檢查 router 及重組流程的作用。
- **限制：** Router 需訓練及偏好資料，72B 模組也有顯著運算需求。結構化可能改寫細節格式，作者展示金額格式變化造成 exact-match 失敗。主要結果依賴 LLM 評分；未提供完整硬體／API 成本。
- **比較邊界：** Loong score、Podcast win rate、latency 是不同任務及指標，不能合併成單一排名。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將其歸入 **D07 Context Construction & Utilization**，次領域 D03、D05；不加 `graph_rag`，因 graph 只是多種候選表示之一。此分類是 repo mapping。它是研究「先選 evidence 形狀、再生成」的代表，可與 graph-only RAG 對照其適用範圍。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [ICLR 2025 正式紀錄](https://proceedings.iclr.cc/paper_files/paper/2025/hash/5975754c7650dfee0682e06e1fec0522-Abstract-Conference.html)；[正式 PDF](https://proceedings.iclr.cc/paper_files/paper/2025/file/5975754c7650dfee0682e06e1fec0522-Paper-Conference.pdf)；[arXiv:2410.08815](https://arxiv.org/abs/2410.08815)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(ICLR 2025-05) StructRAG - Boosting Knowledge Intensive Reasoning of LLMs via Inference-time Hybrid Information Structurization.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2025-05) Simple is Effective - The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation|SubgraphRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2024-04) From Local to Global - A Graph RAG Approach to Query-Focused Summarization|GraphRAG]]。
