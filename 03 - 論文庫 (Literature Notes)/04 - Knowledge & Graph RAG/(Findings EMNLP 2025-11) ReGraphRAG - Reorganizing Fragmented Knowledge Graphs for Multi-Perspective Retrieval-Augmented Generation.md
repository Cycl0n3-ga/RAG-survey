---
paper_id: "Kim2025_ReGraphRAG"
title: "ReGraphRAG: Reorganizing Fragmented Knowledge Graphs for Multi-Perspective Retrieval-Augmented Generation"
authors:
  - "Soohyeong Kim"
  - "Seok Jun Hwang"
  - "JungHyoun Kim"
  - "Jeonghyeon Park"
  - "Yong Suk Choi"
year: null
publication_year: 2025
venue: "Findings of the Association for Computational Linguistics: EMNLP 2025"
doi: "10.18653/v1/2025.findings-emnlp.290"
arxiv: null
url: "https://aclanthology.org/2025.findings-emnlp.290/"
pdf_file: null
tags:
  - paper
  - fragmented-knowledge-graphs
  - graph-reorganization
verification_status: "abstract_only"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D04"
primary_domain: "D04"
secondary_domains:
  - "D03"
  - "D05"
paradigm_tags:
  - "graph_rag"
adjacent_interfaces: []
research_questions:
  - "graph_reorganization"
  - "multi_perspective_retrieval"
  - "query_aware_reranking"
benchmark_ids: []
dataset_ids: []
metrics:
  - "Diversity win rate"
---

# ReGraphRAG: Reorganizing Fragmented Knowledge Graphs for Multi-Perspective Retrieval-Augmented Generation

> **全文待取得：** 書目資訊由 ACL Anthology entry 與 DOI 核對；目前僅能核讀官方摘要。ACL PDF endpoint 在本環境多次逾時，作者公開程式庫亦尚未提供可驗證的本地論文 PDF；因此不記錄正文機制細節、benchmark 名稱、表格數值或硬體設定，亦不宣稱已閱讀全文。`verification_status` 保持 `abstract_only`。

## 一話摘要 (TL;DR)
ReGraphRAG 摘要提出 Graph Reorganization、Perspective Expansion 與 Query-aware Reranking 三個模組，用於修整碎裂圖並支援多視角檢索。

## 研究背景與問題定義 (Problem Statement)
摘要將問題描述為：由非結構化文件抽取知識圖譜時會產生互相斷裂的子圖，使圖檢索難以提供連貫的多跳證據。具體碎裂定義與其量化方式待全文核驗。[官方摘要]

## 核心方法與技術架構 (Methodology & Architecture)
摘要列出 Graph Reorganization、Perspective Expansion、Query-aware Reranking 三項組件，但未提供足夠細節確認其輸入輸出、演算法、資料流或成本。待取得 ACL 正式 PDF 後補記。[官方摘要]

## 主要實驗結果與證據 (Empirical Results & Evidence)
官方摘要僅稱在四個 benchmarks 上比較，報告平均 diversity win rate 超過 80%，並稱 ablation 支持 graph reorganization 與 perspective expansion 的貢獻。摘要未列 benchmarks 名稱、比較對象、指標公式、分母、表格編號、模型或測試設定；此處不把該數字解讀成 80% accuracy，也不補寫無法核實的實驗條件。[官方摘要]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
在全文取得前，無法核實該方法如何新增圖邊、如何控制幻覺或錯誤重連、以及重組成本與 reranking latency。摘要中的「diversity win rate」須回到全文確認定義與比較基線，不能與 answer accuracy 直接比較。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
暫定 D04 為主域（圖組織／表示），D03 涉及抽取後圖結構整理，D05 涉及查詢時 reranking；此為摘要層級的暫定 mapping。取得全文後應重審 taxonomy mapping 與各模組邊界。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [ACL Anthology 官方 entry／摘要／DOI](https://aclanthology.org/2025.findings-emnlp.290/)，DOI [10.18653/v1/2025.findings-emnlp.290](https://doi.org/10.18653/v1/2025.findings-emnlp.290)。
- 正式 PDF：[ACL Anthology PDF](https://aclanthology.org/2025.findings-emnlp.290.pdf)（官方來源可瀏覽；本地副本待下載，暫無本地 PDF wikilink）。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings NAACL 2025-04) GRAG - Graph Retrieval-Augmented Generation|GRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2025-11) PropRAG - Guiding Retrieval with Beam Search over Proposition Paths|PropRAG]]。
