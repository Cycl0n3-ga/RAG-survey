---
paper_id: "Yu2021_KGFID"
title: "KG-FiD: Infusing Knowledge Graph in Fusion-in-Decoder for Open-Domain Question Answering"
authors:
  - "Donghan Yu"
  - "Chenguang Zhu"
  - "Yuwei Fang"
  - "Wenhao Yu"
  - "Shuohang Wang"
  - "Yichong Xu"
  - "Xiang Ren"
  - "Yiming Yang"
  - "Michael Zeng"
year: 2021
publication_year: 2022
venue: "ACL 2022"
doi: "10.18653/v1/2022.acl-long.340"
arxiv: "2110.04330"
url: "https://aclanthology.org/2022.acl-long.340/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(ACL 2022-05) KG-FiD - Infusing Knowledge Graph in Fusion-in-Decoder for Open-Domain Question Answering.pdf"
tags:
  - paper
  - knowledge-graph
  - open-domain-qa
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains:
  - "D04"
  - "D07"
paradigm_tags:
  - "graph_rag"
adjacent_interfaces: []
research_questions:
  - "graph_aware_passage_reranking"
  - "retrieval_computation_tradeoff"
  - "passage_relationship_modeling"
benchmark_ids:
  - "Natural Questions"
  - "TriviaQA"
dataset_ids:
  - "Natural Questions"
  - "TriviaQA"
metrics:
  - "Exact Match"
  - "Hits@K"
source_version: arXiv:2110.04330v2
verified_version: arXiv:2110.04330v2
pdf_pages: 14
pdf_sha256: a5ed2d4098f0299833b3ada66d0292fa92c3f363aba3da96c8be82566319aaf2
---

# KG-FiD: Infusing Knowledge Graph in Fusion-in-Decoder for Open-Domain Question Answering

> **版本與閱讀範圍：** arXiv 首發 2021-10；ACL 2022 正式發表。已閱讀 arXiv v2 全文（14 頁，2022-06 修訂）；ACL 官方 PDF 端點本次連線逾時，因此本地數據與頁碼均以 arXiv v2 為準，正式版逐表差異未核實。作者、DOI、正式 venue 與頁碼依 ACL Anthology 紀錄。

## 一話摘要 (TL;DR)
KG-FiD 將檢索 passages 轉為 passage graph，以兩階段圖式重排減少進入 FiD 深層 reader 的候選段落，在 NQ、TriviaQA 上提升 EM，並提供準確率與推論計算量的取捨。

## 研究背景與問題定義 (Problem Statement)
FiD 將所有 top-k 段落編碼後交由 decoder 融合，當檢索候選數大時，編碼成本隨段落數增加。作者研究如何利用段落間知識圖關係重排並縮小深層 reader 的候選數，同時保留對答案相關段落的覆蓋。[§1–2, pp. 1–3]

## 核心方法與技術架構 (Methodology & Architecture)
第一階段用問題與 passage embeddings 建立 passage graph，圖神經網路依問題訊號重排候選；第二階段讓候選 passages 進入 encoder 前段，再用 graph-based reranking 決定哪些 passages 繼續通過較深 encoder layers，最後由 FiD decoder 融合。本文以 DPR 取回 passages，評估 T5 base／large；計算比較中 N1 是 reader 輸入段落數、L1 是第二階段重排前所用 encoder layers。[§3–4, pp. 3–7]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, p. 8：** 在作者自有實作下，FiD base 的 NQ / TriviaQA EM = 48.8 / 66.2，KG-FiD base = 49.6 / 66.7；FiD large = 51.9 / 68.7，KG-FiD large = 53.4 / 69.8。表列評測資料為 Natural Questions 與 TriviaQA。
- **Table 2, p. 9：** large model、N1=100 的 FiD 基線 FLOPs 比率為 1.00x，NQ EM 51.9、延遲 1.65s；KG-FiD L1=6 為 0.38x FLOPs、NQ EM 52.0、0.70s，TriviaQA EM 68.9、0.68s；KG-FiD L1=24 為 0.90x FLOPs、NQ EM 53.4、1.49s，TriviaQA EM 69.8、1.48s。這些是該文 large 設定下每題 latency，不可外推為跨系統服務延遲。
- **Table 3, p. 9：** 移除 stage-1 或 stage-2 皆使 NQ／TriviaQA EM 下降，支持兩個重排階段在本文實驗中的增益。
- **硬體：** 可讀全文報告 FLOPs 與每題 latency，但沒有清楚列出 Table 2 延遲的 GPU 型號／服務硬體；故此處不補推硬體設定。指標為 EM，另以 NQ passage ranking 圖報 Hits@K。[§4.3, pp. 7–9]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 將 KG 用於 passages 之間的關係與排序，而非要求 LLM 直接遍歷完整 KG；兩階段設計可把計算集中到較少 passages。
- **限制與成本：** 要建 passage graph 並訓練 GNN reranker；收益依檢索到的候選與 passage graph 品質而定。不同 L1 會改變準確率、FLOPs 及延遲，沒有單一配置在所有指標上同時最優。UniK-QA 使用額外 Wikipedia tables，原文提醒不可與本文設定直接視為公平比較。[§4.3, pp. 7–9]
- **版本限制：** 上述數字為 arXiv v2 全文所載；正式 ACL 版是否有表格變更尚待取得 publisher PDF 確認。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 分類為 **D05 Query Understanding & Retrieval**，D04 記錄 passage graph 的表示與檢索介面，D07 記錄被重排後送入 reader 的上下文選擇。GraphRAG 在此指 passage-level graph-aware retrieval/reranking；不可與把原始文檔抽成實體關係 KG 的 GraphRAG pipeline 混成同一索引物件。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式來源：[ACL Anthology 論文紀錄與 DOI](https://aclanthology.org/2022.acl-long.340/)；[arXiv:2110.04330](https://arxiv.org/abs/2110.04330)（本地全文為 v2）。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(ACL 2022-05) KG-FiD - Infusing Knowledge Graph in Fusion-in-Decoder for Open-Domain Question Answering.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2024-12) G-Retriever - Retrieval-Augmented Generation for Textual Graph Understanding and Question Answering]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) GNN-RAG - Graph Neural Retrieval for Efficient Large Language Model Reasoning on Knowledge Graphs]]。
