---
paper_id: "Han2024_GraphRAGSurvey"
title: "Retrieval-Augmented Generation with Graphs (GraphRAG)"
authors:
  - "Haoyu Han"
  - "Yu Wang"
  - "Harry Shomer"
  - "Kai Guo"
  - "Jiayuan Ding"
  - "Yongjia Lei"
  - "Mahantesh Halappanavar"
  - "Ryan A. Rossi"
  - "Subhabrata Mukherjee"
  - "Xianfeng Tang"
  - "Qi He"
  - "Zhigang Hua"
  - "Bo Long"
  - "Tong Zhao"
  - "Neil Shah"
  - "Amin Javari"
  - "Yinglong Xia"
  - "Jiliang Tang"
year: 2024
publication_year: null
venue: "arXiv"
doi: "10.48550/arXiv.2501.00309"
arxiv: "2501.00309"
url: "https://arxiv.org/abs/2501.00309"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(arXiv 2025-01) Retrieval-Augmented Generation with Graphs (GraphRAG).pdf"
tags:
  - paper
  - survey
  - graph-rag
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "survey"
taxonomy_version: "v2"
taxonomy_home: "CROSS"
primary_domain: null
secondary_domains:
  - "D04"
  - "D05"
  - "D07"
  - "D09"
paradigm_tags: []
adjacent_interfaces: []
research_questions:
  - "graph-rag-component-design"
  - "graph-rag-domain-adaptation"
  - "graph-rag-evaluation-and-resources"
benchmark_ids: []
dataset_ids: []
metrics: []
source_version: arXiv:2501.00309v2
verified_version: arXiv:2501.00309v2
pdf_pages: 88
pdf_sha256: 737b0b8fe0aa8459429b5906d66d0bfcb5246c488add534d3ce23f58a0f7b7fc
---

# Retrieval-Augmented Generation with Graphs (GraphRAG)

> **版本與閱讀範圍：** arXiv v1 於 2024-12-31 提交，v2 於 2025-01-08 修訂；本地 PDF 為 v2，88 頁。書目目前核為 arXiv survey，未找到正式期刊／會議版，因此 publication_year 保留 null。本文是 survey，不提供同條件的 primary-paper 性能比較。

## 一話摘要 (TL;DR)
Han et al. 以 query processor、graph data source、retriever、organizer、generator 五個 component 整理 GraphRAG 方法，並按圖資料領域盤點任務、資源與尚待處理的系統性問題。

## 研究背景與問題定義 (Problem Statement)
作者指出 graph-structured source 具有異質節點、邊與 domain-specific relation，傳統文字／圖像 RAG 的檢索及生成設計不能直接涵蓋這些結構。survey 的問題是：如何建立一套跨 GraphRAG 領域可用的組件框架，整理 query 對圖的對齊、圖檢索、組織證據及生成方法，並比較不同領域的 graph data 和任務。[§1–2, PDF pp.1–6]

## 核心方法與技術架構 (Methodology & Architecture)
這是一篇文獻整理，不是新 GraphRAG pipeline。作者提出五個互動組件：query processor 將使用者 query 轉成可對應圖的 query；graph data source 提供結構化來源；retriever 取回相關圖內容；organizer 重整檢索結果；generator 依 query 和組織後內容產生答案。[Figure 3、§2.1, PDF p.5]

Query processor 分成 entity recognition、relational extraction、query structuration、query decomposition、query expansion（Table 2, PDF p.7）；retriever 的整理涵蓋 entity linking、relational matching、graph traversal、graph kernel、shallow/deep embedding 及 domain expertise（Table 3, PDF p.9）。survey 再分別討論圖來源／領域和不同 organizer、generator 的設計；這個五組件框架是作者的 survey taxonomy，與 repo 的 D01–D14 operational taxonomy 不同。

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Survey coverage：** Table 1, PDF p.6 彙整 knowledge、document、scientific、social 等圖資料領域的任務和查詢例子；它是任務版圖表，不是同一 benchmark 上的性能比較。
- **組件分類：** Table 2, PDF p.7 對照 RAG/GraphRAG 的 query-processing 任務差異；Table 3, PDF p.9 是 retriever strategy 的輸入、輸出及用途分類。這兩表可用作術語索引，不能將代表方法視為同設定 baseline。
- **Open challenges：** §10.2–10.7, PDF pp.50–53 討論 neural/symbolic knowledge 區分、internal/external knowledge calibration 與 reconciliation、accuracy/diversity/novelty、adaptive retrieval、organizer completeness/conciseness、system integration/scalability/trustworthiness，以及 end-to-end、domain-specific、trustworthiness benchmarks。
- **數據可比性：** survey 彙集不同圖領域與不同 task 的文獻，資料、模型、metrics 不一致；本篇不應被用來產生跨研究的總排名或單一 GraphRAG 分數。

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **價值：** 五組件框架有助分辨 query-to-graph alignment、retrieval、evidence organization 與 generation；按領域分類則提醒知識圖譜、文件圖、表格與科學圖不能被單一方法假設取代。它適合作為 GraphRAG 研究線存在與分類視角的 evidence。
- **限制：** arXiv v2 發布於 2025-01，survey coverage 有明確時間界線；大量子領域分述讓方法跨 task 的可比性有限。它不等同 systematic review 或統一實驗，也沒有提供目前所有 GraphRAG 實作的完整 registry。
- **分類界線：** 作者五組件可與 D01–D14 做多對多映射，不可一對一替換：retriever 多落 D05，graph representation/source preparation 觸及 D03–D04，organizer 對應 D07，generator 對應 D09；來源型態本身不是 lifecycle domain。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將其設為 `artifact_type: survey`、`taxonomy_home: CROSS`、`primary_domain: null`，並以 D04、D05、D07、D09 表示涵蓋面，不併入 method paper 的 D04/D05 計數。它和 Peng et al. 的 GraphRAG survey 可並列閱讀：此篇以五組件加 domain-oriented view 組織；Peng et al. 採 graph indexing / graph-guided retrieval / graph-enhanced generation 主線。兩者 taxonomy 皆為 survey 框架，不是 D01–D14 的社群共識。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [arXiv:2501.00309 v2](https://arxiv.org/abs/2501.00309)；[arXiv-issued DOI](https://doi.org/10.48550/arXiv.2501.00309)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(arXiv 2025-01) Retrieval-Augmented Generation with Graphs (GraphRAG).pdf|開啟本地 PDF 檔案]]。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2024-08) Graph Retrieval-Augmented Generation - A Survey|Peng et al. GraphRAG survey]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) GeAR - Graph-enhanced Agent for Retrieval-augmented Generation|GeAR]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2024-12) HippoRAG - Neurobiologically Inspired Long-Term Memory for Large Language Models|HippoRAG]]。
