---
paper_id: "Mo2025_KGGen"
title: "KGGen: Extracting Knowledge Graphs from Plain Text with Language Models"
authors:
  - "Belinda Mo"
  - "Kyssen Yu"
  - "Joshua Kazdan"
  - "Joan Cabezas"
  - "Proud Mpala"
  - "Lisa Yu"
  - "Chris Cundy"
  - "Charilaos Kanatsoulis"
  - "Sanmi Koyejo"
year: 2025
publication_year: 2025
venue: "NeurIPS 2025"
doi: "10.52202/085713-1010"
arxiv: "2502.09956"
url: "https://proceedings.neurips.cc/paper_files/paper/2025/hash/2b368455e832d2b1a60bcad8c4c6481f-Abstract-Conference.html"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(NeurIPS 2025-12) KGGen - Extracting Knowledge Graphs from Plain Text with Language Models.pdf"
tags:
  - paper
  - knowledge-graph-extraction
  - entity-resolution
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D03"
primary_domain: "D03"
secondary_domains:
  - "D04"
paradigm_tags: []
adjacent_interfaces: []
research_questions:
  - "knowledge_graph_extraction"
  - "entity_resolution"
  - "information_retention"
benchmark_ids:
  - "MINE-1"
  - "MINE-2"
dataset_ids:
  - "MINE-1 articles"
  - "WikiQA"
  - "SemEval-2010 Task 8"
metrics:
  - "MINE information-retention score"
  - "triple validity"
  - "entity recall"
  - "throughput"
---

# KGGen: Extracting Knowledge Graphs from Plain Text with Language Models

> **版本與來源：** arXiv 預印本於 2025 年發布；按 NeurIPS 2025 正式 proceedings PDF 整理。PDF title page 列 9 位作者；NeurIPS landing page 摘要欄作者名單較短，筆記保留 PDF 正式版名單供核對。

## 一話摘要 (TL;DR)
KGGen 以分階段 LLM 抽取、跨來源聚合及 embedding-cluster + LLM 去重，建構較精簡的知識圖，並提出 MINE 評估抽取圖譜能保留多少來源資訊。

## 研究背景與問題定義 (Problem Statement)
現有大型知識圖譜不完整，從文字自動抽取的圖譜則品質與可用性不穩。本文主題是 plain-text-to-KG 建構和資訊保留評估；它是支援 GraphRAG 的建圖方法，不是完整端到端 RAG 框架。[§1–3, pp. 1–3]

## 核心方法與技術架構 (Methodology & Architecture)
1. 以 Gemini 2.0 Flash 分別抽取實體與 subject–predicate–object 關係。
2. 跨文本聚合圖，統一文字格式；此步驟不需 LLM。
3. 對 entity 與 edge label 分別以 SBERT embedding + k-means 分群，再用 BM25 與語意檢索找近鄰，交由 LLM 僅合併確切重複項並挑 canonical name，迭代至無待處理項目。

MINE-1 測試單篇文章中的已知事實能否從抽取圖推得；MINE-2 在 WikiQA 上測 KG-assisted RAG。兩者分開衡量 extraction information retention 與下游 QA。[§4–5, pp. 3–6]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Figure 3 / Table 1, pp. 7–8：** 100 篇文章的 MINE-1 平均分數：KGGen 66.07%、GraphRAG 47.80%、OpenIE 29.84%。Table 1 亦列 Claude Sonnet 3.5 / GPT-4o / Gemini 2.0 Flash 下 KGGen 得分 73 / 66 / 44；抽取三元組有效率人工抽樣 100 條中 KGGen 98%、GraphRAG 0%、OpenIE 55%。分數依論文的 semantic query + LLM 推斷流程，不是完整人工 fact recall gold labels。
- **SemEval-2010 子集, p. 8：** 隨機抽 100 句，KGGen 於 96/100 筆包含兩個人工標註目標實體；這只衡量 entity capture，資料集的關係標籤不足以評細粒度 relation extraction。
- **Table 3, p. 10：** 1M-character novel corpus 上，KGGen extraction+resolution 共 551 秒、5.37M tokens、估計 API cost $0.84；GraphRAG 對同 corpus 需要 2,079 秒（正文另稱 extraction phase 2,319 秒，與表值不一致，應以此處明確標出原文數字差異待核），不宜直接視為嚴格同成本實驗。Table 2 顯示 KGGen 對該 corpus entity 數去重 22.4%、edge 數去重 23%。
- **環境：** 以 Gemini 2.0 Flash 抽取、S-BERT clustering；MINE-1 評估亦測 Claude Sonnet 3.5、GPT-4o。作者說明實驗不需特殊硬體，可在一般機器執行；本文未提供 GPU 配置。[§6, pp. 6–10; Limitations §8, p. 10]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 把跨文件 entity/edge resolution 明確納入抽取流程，並以 MINE-1、MINE-2 區分圖譜資訊保留和下游 RAG 效果；提供處理成本與 throughput 分項。
- **限制與代價：** 作者承認可能過度或不足合併；MINE corpus 最大約 5M tokens，未反映 web-scale；醫療、金融等領域可能需專業知識或 ontology 改善抽取。MINE-1 用 LLM 評估，雖抽樣人工驗證一致率 90.2%，仍有評估器偏差。Table 4 / 正文對 GraphRAG 在 1M 字元處理時間分別報 2,079 / 2,319 秒，需保留原文不一致。
- **比較邊界：** MINE-1 是圖內容保留，MINE-2 是特定 WikiQA retrieval+generation；GraphRAG / OpenIE 對照不構成所有 graph extractor 的完整代表。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將 KGGen 分類為 **D03 Knowledge Extraction & Consolidation**，次領域 D04，因關鍵貢獻在抽取與去重整併，而不是下游 query-time retrieval；不使用 GraphRAG paradigm tag。此 mapping 是本庫建議。MINE-1 也可作為抽取是否保留源資訊的評估 anchor，但 benchmark、dataset 與評分流程需分開記錄。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [NeurIPS 2025 official record](https://proceedings.neurips.cc/paper_files/paper/2025/hash/2b368455e832d2b1a60bcad8c4c6481f-Abstract-Conference.html)；[正式 PDF](https://proceedings.neurips.cc/paper_files/paper/2025/file/2b368455e832d2b1a60bcad8c4c6481f-Paper-Conference.pdf)；[DOI](https://doi.org/10.52202/085713-1010)；[arXiv:2502.09956](https://arxiv.org/abs/2502.09956)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(NeurIPS 2025-12) KGGen - Extracting Knowledge Graphs from Plain Text with Language Models.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2025-12) HyperGraphRAG - Retrieval-Augmented Generation via Hypergraph-Structured Knowledge Representation|HyperGraphRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2019-07) DocRED - A Large-Scale Document-Level Relation Extraction Dataset|DocRED]]。
