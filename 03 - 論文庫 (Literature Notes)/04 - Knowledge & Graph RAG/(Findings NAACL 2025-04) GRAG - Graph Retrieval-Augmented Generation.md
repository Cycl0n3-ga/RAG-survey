---
paper_id: "Hu2024_GRAG"
title: "GRAG: Graph Retrieval-Augmented Generation"
authors:
  - "Yuntong Hu"
  - "Zhihan Lei"
  - "Zheng Zhang"
  - "Bo Pan"
  - "Chen Ling"
  - "Liang Zhao"
year: 2024
publication_year: 2025
venue: "Findings of NAACL 2025"
doi: "10.18653/v1/2025.findings-naacl.232"
arxiv: "2405.16506"
url: "https://aclanthology.org/2025.findings-naacl.232/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(Findings NAACL 2025-04) GRAG - Graph Retrieval-Augmented Generation.pdf"
tags:
  - paper
  - graph-retrieval
  - textual-graph
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains:
  - "D04"
  - "D07"
  - "D09"
paradigm_tags:
  - "graph_rag"
  - "multi_hop_rag"
adjacent_interfaces: []
research_questions:
  - "textual_subgraph_retrieval"
  - "graph_text_evidence_fusion"
  - "cross_dataset_transfer"
benchmark_ids:
  - "GraphQA"
dataset_ids:
  - "WebQSP"
  - "ExplaGraphs"
metrics:
  - "F1"
  - "Hit@1"
  - "Recall"
  - "Accuracy"
source_version: arXiv:2405.16506v3
verified_version: arXiv:2405.16506v3
pdf_pages: 13
pdf_sha256: 6a1ccc0a1fb6841be975c2f18bd57cded31b74ada4d15191cdddd614e9c8ec6e
---

# GRAG: Graph Retrieval-Augmented Generation

> **版本與閱讀範圍：** arXiv 首發 2024-05；正式發表於 Findings of NAACL 2025。已完整閱讀 arXiv v3（13 頁，2025-07 修訂），本地 PDF 與數值引用均為 v3；此版本晚於正式發表，ACL PDF 端點本次連線逾時，故正式版與 v3 的表格差異尚未核實。以下頁碼採本地 arXiv v3。

## 一話摘要 (TL;DR)
GRAG 將大型文本圖切成可搜尋的 ego-subgraphs，結合子圖文字描述與圖拓撲表示進行檢索，再把圖與文字證據共同交給 LLM 生成答案。

## 研究背景與問題定義 (Problem Statement)
一般文字檢索將圖中的關係展平，可能遺失多跳推理所需的拓撲；直接將整圖交給模型則難以擴展。本文處理 textual graph 問答，聚焦在如何形成大小可控、兼顧語意與結構資訊的檢索單位。[§1–2, pp. 1–3]

## 核心方法與技術架構 (Methodology & Architecture)
方法將圖切為節點周圍的 k-hop ego-subgraphs，形成文字 view 與 graph view 的表示，並依問題檢索相關子圖，再以兩種 view 的嵌入供生成模型使用。作者亦提供可訓練的 prompt-tuning 與 LoRA 設定。主實驗使用 Llama-2-7B；文本向量採 SentenceBERT，圖編碼器為 4 層、每層 4 heads、hidden size 1024 的 GAT。[§3–5, pp. 3–6; Appendix A.3, p. 12]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 2, p. 7：** WebQSP 上 GRAG 的 F1 / Hit@1 / Recall = 0.5022 / 0.7236 / 0.5099，GRAGLoRA = 0.5041 / 0.7275 / 0.5112；ExplaGraphs Accuracy 分別為 0.9223 / 0.9274。G-RetrieverLoRA 在兩資料集對應值為 WebQSP F1 0.5023、Hit@1 0.7016、Recall 0.5002，ExplaGraphs Acc 0.9042。
- **Table 3, p. 7：** 跨資料集 transfer 中，WebQSP→ExplaGraphs Accuracy 0.4540（相對 LLM baseline 表列 +33.77%）；反向在 WebQSP 的 Hit@1 為 0.4237（+2.15%）。這是作者定義的跨資料集設定，不代表一般 zero-shot 部署表現。
- **資料與資源：** Table 1, p. 6 描述 WebQSP 平均每圖 1,370.89 nodes、4,252.37 edges、100,627 tokens；ExplaGraphs 平均 5.17 nodes、4.25 edges、1,396 tokens。Appendix A.3, p. 12 報告 4 張 NVIDIA A10G、Llama-2-7B、SentenceBERT 與 GAT 設定。

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 以受限大小的子圖縮小全圖檢索範圍，並把 graph view 和 text view 一起保留；可用同一設計比較凍結 LLM、prompt tuning 與 LoRA。
- **限制與成本：** 作者指出 k 增大會讓訓練／推論時間增加，超過 3-hop 時子圖 embedding 較易 oversmoothing；增加取回子圖數也可能引入無關資訊。測試集中於 WebQSP 與 ExplaGraphs 兩種圖型，外推到大型異質真實圖仍需驗證。[§5.3, pp. 7–8]
- **版本限制：** 本地 v3 比正式發表時間晚，正式版逐表差異待查；不能將下列表格數值當成已核定的 ACL 出版版數據。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 分類為 **D05 Query Understanding & Retrieval**，D04 是子圖表示／索引介面，D07 是多視圖證據如何提供給生成器，D09 是圖文證據共同支援生成。此 mapping 是 repo 的生命週期分類。GRAG 可與 G-Retriever、SubgraphRAG、GraphRAG 比較其檢索單位與圖結構進入生成階段的方式；基準與圖規模差異須保留。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式來源：[ACL Anthology 論文紀錄與 DOI](https://aclanthology.org/2025.findings-naacl.232/)；[arXiv:2405.16506](https://arxiv.org/abs/2405.16506)（本地全文為 v3）。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(Findings NAACL 2025-04) GRAG - Graph Retrieval-Augmented Generation.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2024-12) G-Retriever - Retrieval-Augmented Generation for Textual Graph Understanding and Question Answering]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2025-05) Simple is Effective - The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation]]。
