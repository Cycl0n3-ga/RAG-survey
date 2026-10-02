---
paper_id: "Luo2025_HyperGraphRAG"
title: "HyperGraphRAG: Retrieval-Augmented Generation via Hypergraph-Structured Knowledge Representation"
authors:
  - "Haoran Luo"
  - "Haihong E"
  - "Guanting Chen"
  - "Yandan Zheng"
  - "Xiaobao Wu"
  - "Yikai Guo"
  - "Qika Lin"
  - "Yu Feng"
  - "Zemin Kuang"
  - "Meina Song"
  - "Yifan Zhu"
  - "Luu Anh Tuan"
year: 2025
publication_year: 2025
venue: "NeurIPS 2025"
doi: "10.52202/085713-5089"
arxiv: "2503.21322"
url: "https://proceedings.neurips.cc/paper_files/paper/2025/hash/df55ee6e59f8ac4a625219e11fe9ddba-Abstract-Conference.html"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(NeurIPS 2025-12) HyperGraphRAG - Retrieval-Augmented Generation via Hypergraph-Structured Knowledge Representation.pdf"
tags:
  - paper
  - hypergraph
  - n-ary-relations
verification_status: "verified"
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
  - "n_ary_knowledge_representation"
  - "hypergraph_retrieval"
  - "retrieval_efficiency"
benchmark_ids:
  - "HyperGraphRAG evaluation"
dataset_ids:
  - "UltraDomain Agriculture"
  - "UltraDomain Computer Science"
  - "UltraDomain Legal"
  - "UltraDomain Mix"
  - "International hypertension guidelines"
metrics:
  - "F1"
  - "Retrieval Similarity"
  - "Generation Evaluation"
source_version: NeurIPS 2025 proceedings
verified_version: NeurIPS 2025 proceedings
pdf_pages: 29
pdf_sha256: 2fae859984154a402b48f33de63c0a8d62fe4d15c61894d14d31f07da2a4a05c
---

# HyperGraphRAG: Retrieval-Augmented Generation via Hypergraph-Structured Knowledge Representation

> **版本與來源：** NeurIPS 2025 正式版，NeurIPS 2025 主會議論文；預印本 arXiv:2503.21322。作者依正式 proceedings PDF title page 記錄。

## 一話摘要 (TL;DR)
HyperGraphRAG 以超邊承載多元關係事實，結合 hypergraph 建構、雙向擴展檢索及 chunk-RAG 融合，供 LLM 生成答案。

## 研究背景與問題定義 (Problem Statement)
作者指出一般圖的單一邊連接兩個節點，將 n-ary facts 拆成多條二元關係可能造成結構碎片化。本文研究超圖表示能否在多領域 RAG 中保留多實體事實並改善檢索與生成。其 “first” 屬作者對工作的定位；本筆記不將其外推為所有超圖型 RAG 的優先權結論。[§1, pp. 1–2]

## 核心方法與技術架構 (Methodology & Architecture)
建圖時以 LLM 從文件抽取 n-ary facts，形成 hyperedges 及其實體集合，並以 bipartite/vector representations 支援搜尋。查詢時先抽取 query entities，分別以相似度檢索相關 entities 與 hyperedges，再雙向展開補齊事實中的實體／超邊，亦可與 chunk-based retrieval 結合。最後將擴展後知識及可選文字片段交給 LLM 回答。[§4, pp. 4–6]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 2, p. 7：** 五個 domain（Medicine、Agriculture、CS、Legal、Mix）以 F1、retrieval similarity (R-S)、generation evaluation (G-E) 評估。overall 行中 Medicine HyperGraphRAG F1/R-S/G-E 為 35.35/70.19/59.35；StandardRAG 為 27.90/62.57/55.66。這是本文自建問答及特定 LLM-as-judge 設定，不是公開 benchmark leaderboard。
- **設定：** GPT-4o-mini 作抽取與生成，text-embedding-3-small 作向量模型；檢索使用 kV=60、τV=50、kH=60、τH=5、kC=5、τC=0.5。五個 domain 的資料包含 UltraDomain 內容與高血壓指引，問題涵蓋 1–3 hop，答案由人工驗證。實驗在 80-core CPU、512GB RAM 伺服器執行；論文未報 GPU。
- **比較邊界：** Table 2 的方法以共同 generation prompt 和 GPT-4o-mini 控制比較；R-S 是取回知識與建題 ground-truth knowledge 的語意相似度，G-E 是 LLM judge 七維平均，不應當作標準 fact accuracy。[§5.1–5.2, pp. 6–7]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 將 n-ary facts 保持為同一超邊概念，並將結構化事實檢索與傳統 chunks 融合；對不同 source arity 分組報告結果，也分析建圖／生成時間成本。
- **限制與代價：** LLM 抽取及向量索引帶來建圖與更新成本；ontology/knowledge extraction 品質和超邊檢索閾值影響結果。評測來源及 QA 為論文所構造／抽樣，不足以直接代表任意工業語料或網路規模圖譜；G-E 受 judge 模型影響。
- **作者附錄限制說明：** Appendix I 記錄需更多研究圖規模化與實驗重現性；可擴展性結論應依其測試資料量和模型/API 設定理解。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將其放在 **D04 Representation & Indexing**，次領域 D03（文字轉圖）與 D05（檢索）；使用 `graph_rag`。這是 repo mapping。它補足二元 entity-relation graph 的表示軸，可與 OG-RAG 的 ontology-grounded hyperedge、KGGen 的 entity resolution 比較建構方式；指標和測試語料各異，不能跨文直接排名。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [NeurIPS 2025 official record](https://proceedings.neurips.cc/paper_files/paper/2025/hash/df55ee6e59f8ac4a625219e11fe9ddba-Abstract-Conference.html)；[正式 PDF](https://proceedings.neurips.cc/paper_files/paper/2025/file/df55ee6e59f8ac4a625219e11fe9ddba-Paper-Conference.pdf)；[DOI](https://doi.org/10.52202/085713-5089)；[arXiv:2503.21322](https://arxiv.org/abs/2503.21322)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(NeurIPS 2025-12) HyperGraphRAG - Retrieval-Augmented Generation via Hypergraph-Structured Knowledge Representation.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2025-11) OG-RAG - Ontology-grounded Retrieval-Augmented Generation for Large Language Models|OG-RAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2024-12) G-Retriever - Retrieval-Augmented Generation for Textual Graph Understanding and Question Answering|G-Retriever]]。
