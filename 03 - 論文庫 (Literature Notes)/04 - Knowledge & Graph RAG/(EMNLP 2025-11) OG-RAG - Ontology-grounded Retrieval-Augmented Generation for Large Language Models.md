---
paper_id: "Sharma2025_OG-RAG"
title: "OG-RAG: Ontology-grounded retrieval-augmented generation for large language models"
authors:
  - "Kartik Sharma"
  - "Peeyush Kumar"
  - "Yunqing Li"
year: 2024
publication_year: 2025
venue: "EMNLP 2025"
doi: "10.18653/v1/2025.emnlp-main.1674"
arxiv: "2412.15235"
url: "https://aclanthology.org/2025.emnlp-main.1674/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(EMNLP 2025-11) OG-RAG - Ontology-grounded Retrieval-Augmented Generation for Large Language Models.pdf"
tags:
  - paper
  - ontology
  - hypergraph
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D04"
primary_domain: "D04"
secondary_domains:
  - "D05"
  - "D07"
paradigm_tags:
  - "graph_rag"
adjacent_interfaces: []
research_questions:
  - "ontology_grounding"
  - "hypergraph_retrieval"
  - "context_attribution"
benchmark_ids:
  - "OG-RAG domain QA evaluation"
dataset_ids:
  - "Soybean"
  - "Wheat"
  - "News"
metrics:
  - "Context Recall"
  - "Context Entity Recall"
  - "Answer Similarity"
  - "Answer Correctness"
  - "Answer Relevance"
---

# OG-RAG: Ontology-grounded retrieval-augmented generation for large language models

> **版本與來源：** 預印本 arXiv:2412.15235 發布於 2024 年；本文按 ACL Anthology 所收 EMNLP 2025 正式版及頁碼整理。

## 一話摘要 (TL;DR)
OG-RAG 以 domain ontology 引導文件事實形成超圖，再用 query 尋找較小的相關 hyperedge context，以支援領域問答及來源歸因。

## 研究背景與問題定義 (Problem Statement)
泛用 LLM 缺乏專業領域知識，傳統向量檢索未必遵循領域概念與關係。OG-RAG 研究如何用 ontology 約束事實組織與檢索，面向農業與新聞等特定知識問答，而不是提出通用百科 KG 或無領域設定的 graph construction。[pp. 32962–32964, §§1–3]

## 核心方法與技術架構 (Methodology & Architecture)
方法先用 ontology mapping 及 LLM 將來源文件轉成 factual blocks，再將 blocks 轉成 hypergraph，hyperedge 連結具語義的事實與對應 ontology 概念。查詢時找相關 hypernodes、擴展候選 hyperedges，並用最佳化選取較精簡的 context；生成階段把選取的超圖證據提供給 LLM。另評估 context attribution 與基於已取回事實的 deduction。[§4, pp. 32964–32966]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, p. 32967：** Soybean / Wheat / News 三種資料中，OG-RAG context recall (C-Rec) 為 0.84 / 0.95 / 0.82，context entity recall (C-ERec) 為 0.41 / 0.34 / 0.52。表註稱各指標 95% CI ≤0.05；部分 GraphRAG-News 結果因運算超過一天未完成。
- **Table 2–4, pp. 32968–32969：** 分別比較 answer quality、retrieval efficiency、context attribution；指標含 answer similarity/correctness/relevance、回應支持時間等，請以各表指標定義解讀，不能簡化為單一 accuracy。
- **設定與硬體：** 評估兩個農業問答資料集與 News，使用 GPT-4o、GPT-4o-mini、Llama 3.1 系列；索引／ontology mapping 使用 GPT-4o。Appendix dataset stats 顯示 News 超圖含 7,497 節點、4,573 hyperedges；作者註明相關 query 實驗不需 GPU，在 Ubuntu 18.04、Intel Xeon 環境執行。[§5–6, pp. 32966–32970; Appendix B, p. 32974]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** ontology 提供領域型概念框架；可依答案事實評 context recall、entity recall 及 attribution，而不只用文字相似度衡量檢索。比較包含 RAG、RAPTOR 與 GraphRAG。
- **限制與代價：** 需可用且適合的 domain ontology，且要執行 LLM 抽取／mapping；作者說明評測採特定 domain 資料，不能與通用 RAG datasets 等同。News 資料經篩選；論文亦提及擴大資料集與超圖會帶來規模議題。結果依賴特定模型與資料集。
- **比較邊界：** Table 1 context recall 等與 Table 2 answer metrics 不同。論文摘要所稱提升比例不能脫離其 baseline、測試資料與 LLM 設定使用。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將 OG-RAG 歸為 **D04 Representation & Indexing**，次領域 D05 檢索與 D07 context construction/utilization；使用 `graph_rag`。這是 repo mapping。它補足 HyperGraphRAG 的超邊表示之外，ontology 如何控制 domain-specific graph extraction 及 evidence retrieval 的介面；兩文資料與評測不同，適合比較設計，不適合直接比高低。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [ACL Anthology 正式紀錄、DOI 與頁碼](https://aclanthology.org/2025.emnlp-main.1674/)；[正式 PDF](https://aclanthology.org/2025.emnlp-main.1674.pdf)；[arXiv:2412.15235](https://arxiv.org/abs/2412.15235)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(EMNLP 2025-11) OG-RAG - Ontology-grounded Retrieval-Augmented Generation for Large Language Models.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2025-12) HyperGraphRAG - Retrieval-Augmented Generation via Hypergraph-Structured Knowledge Representation|HyperGraphRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2025-12) KGGen - Extracting Knowledge Graphs from Plain Text with Language Models|KGGen]]。
