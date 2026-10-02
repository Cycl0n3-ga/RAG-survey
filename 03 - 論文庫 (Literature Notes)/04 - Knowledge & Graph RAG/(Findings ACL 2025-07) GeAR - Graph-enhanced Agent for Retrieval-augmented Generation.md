---
paper_id: "Shen2024_GeAR"
title: "GeAR: Graph-enhanced Agent for Retrieval-augmented Generation"
authors:
  - "Zhili Shen"
  - "Chenxin Diao"
  - "Pavlos Vougiouklis"
  - "Pascual Merita"
  - "Shriram Piramanayagam"
  - "Enting Chen"
  - "Damien Graux"
  - "Andre Melo"
  - "Ruofei Lai"
  - "Zeren Jiang"
  - "Zhongyang Li"
  - "Ye Qi"
  - "Yang Ren"
  - "Dandan Tu"
  - "Jeff Z. Pan"
year: 2024
publication_year: 2025
venue: "Findings of ACL 2025"
doi: "10.18653/v1/2025.findings-acl.624"
arxiv: "2412.18431"
url: "https://aclanthology.org/2025.findings-acl.624/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) GeAR - Graph-enhanced Agent for Retrieval-augmented Generation.pdf"
tags:
  - paper
  - multi-hop-question-answering
  - graph-expansion
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains:
  - "D12"
  - "D04"
paradigm_tags:
  - "graph_rag"
  - "multi_hop_rag"
  - "agentic_rag"
adjacent_interfaces: []
research_questions:
  - "passage_graph_expansion"
  - "triple_beam_diversification"
  - "iterative_retrieval_memory"
  - "multi_hop_retrieval"
benchmark_ids:
  - "MuSiQue"
  - "HotpotQA"
  - "2WikiMultiHopQA"
dataset_ids:
  - "MuSiQue"
  - "HotpotQA"
  - "2WikiMultiHopQA"
metrics:
  - "Recall@k"
  - "Exact Match"
  - "F1"
source_version: arXiv:2412.18431v2
verified_version: arXiv:2412.18431v2
pdf_pages: 24
pdf_sha256: ed381fac088ebb547003e88120b23968b485f4162f533d92f862cf8aef224d73
additional_verified_versions:
  - "Findings ACL 2025 (Tables 2–4, Limitations)"
---

# GeAR: Graph-enhanced Agent for Retrieval-augmented Generation

> **版本與閱讀範圍：** arXiv 首發於 2024 年（arXiv:2412.18431），本地 PDF 是 v2（2025-06-22，24 頁）；正式發表於 Findings of ACL 2025，頁 12049–12072，DOI `10.18653/v1/2025.findings-acl.624`。已讀本地 arXiv v2，並以 ACL Anthology 正式全文核對正式書目、Table 2–4 與 Limitations。文中數據的頁碼以下採正式版印刷頁碼。

## 一話摘要 (TL;DR)
GeAR 將 passage–triple 對齊索引、SyncGE 多樣化圖擴展與跨步 gist memory 結合，讓一般 sparse/dense retriever 支援多跳 passage retrieval。

## 研究背景與問題定義 (Problem Statement)
單次 BM25 或 dense retrieval 容易只取回多跳問題中的局部 passage；逐步使用 LLM 沿圖探索又會增加多次生成呼叫。論文探討如何以一個圖式 passage retriever 擴展傳統檢索結果，並在多輪問答中保存已找到的精簡證據，降低多跳檢索的漏召回與重複推理成本。[§1–2, pp. 12049–12050]

## 核心方法與技術架構 (Methodology & Architecture)
離線階段把每個 passage 與抽出的 triples 對齊，形成共享實體相連的 triple graph。SyncGE 先用 base retriever 找 passages，再由 LLM 從這批內容讀出 query-relevant proximal triples；這些 triples 對齊至索引 triple 作為圖搜尋起點。接著以 dense embedding similarity 評分 triple sequence，沿共享 head/tail entity 擴展 diverse triple beams，並以 Reciprocal Rank Fusion 合併擴展 passage 與初始 passages。[§3–4.2, pp. 12050–12052]

多步 GeAR 在每輪 retrieval 後讀取 passages，將支持原問題的 proximal triples 累積為 gist memory；LLM 評估現有記憶是否足以回答，若不足便結合前輪推理改寫子問題，繼續檢索。停止時，記憶中的 triples 重新連回來源 passages，與歷輪檢索結果做 RRF。[§5, pp. 12052–12053]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 2, p. 12054：** 在 MuSiQue、2WikiMultiHopQA、HotpotQA 上，multi-step GeAR 的 Recall@5/10/15 分別為 `58.4/67.6/71.5`、`89.1/95.3/95.9`、`93.4/96.8/97.3`。同表的 HippoRAG + IRCoT 為 `48.8/54.5/58.9`、`82.9/90.6/93.0`、`90.1/94.7/95.9`。評測比較限於作者所列的 benchmark、retrieved passage k 值及實作設定。
- **Table 3, p. 12055：** 使用 top-5 passages 的端到端 QA 中，GeAR 的 EM/F1：MuSiQue `19.0/35.6`、2Wiki `47.4/62.3`、HotpotQA `50.4/69.4`；HippoRAG + IRCoT 分別為 `14.2/25.9`、`45.6/59.0`、`49.2/67.9`。此表將檢索與 generator 結果合併，需與 Table 2 的 retrieval recall 分開閱讀。
- **Table 4, p. 12055：** 對 Hybrid + SyncGE 的多樣性 beam search 消融，在三個資料集及 R@5/10/15 均高於不加 diversity weighting 的版本；例如 MuSiQue R@10 為 `57.7` 對 `53.9`。這是該單一檢索器配置內的消融，不代表多樣性必然改善其他圖搜尋器。
- **評測條件：** 比較要求 LLM 的方法及 triple extraction 採 GPT-4o mini（`gpt-4o-mini-2024-07-18`），temperature 0；QA 使用論文附錄 prompts。資料集為 MuSiQue、HotpotQA、2WikiMultiHopQA。正式版主要結果不提供跨硬體的 latency／吞吐量基準。[§6, pp. 12053–12055]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** SyncGE 以 embedding model 探索三元組圖，避免在每條圖邊上都呼叫 LLM；diverse beam search 增加候選鏈差異，實驗中改善多跳 passage recall；gist memory 將跨輪證據壓成 triples，供 query rewriting 與停止判斷使用。
- **限制：** 作者將範圍限於以 triples 連接 passages 的 retrieval。實體消歧與 KG completion 可再改進；dense embedding scoring 也可替換為 NLI 等方案。gist memory、reasoner 與 query rewriter 沿用既有設計，並非本文單獨深入優化的模組。[§9, p. 12056]
- **比較邊界：** Table 2 是檢索 Recall@k；Table 3 是 top-5 passages 下的 QA EM/F1。不同表的分數不可直接互比。效能也受 passage–triple 抽取品質、entity linking 與所用 LLM 影響；論文結果不能外推成對所有一般 RAG 場景的優勢。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 歸類為 **D05 Query Understanding & Retrieval**，D12 表示跨輪檢索、答案充分性判斷與 query rewrite 的 action loop，D04 表示 passage–triple 對齊索引。`agentic_rag` 標籤描述檢索控制方式；gist memory 是同一問答任務的短期證據狀態，不據此歸為 D11 Persistent Memory Management。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式來源：[ACL Anthology 正式版與 DOI](https://aclanthology.org/2025.findings-acl.624/)；[arXiv:2412.18431](https://arxiv.org/abs/2412.18431)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) GeAR - Graph-enhanced Agent for Retrieval-augmented Generation.pdf|開啟本地 PDF 檔案]]（arXiv v2）。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) GNN-RAG - Graph Neural Retrieval for Efficient Large Language Model Reasoning on Knowledge Graphs|GNN-RAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2024-12) HippoRAG - Neurobiologically Inspired Long-Term Memory for Large Language Models|HippoRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2024-11) GraphReader - Building Graph-based Agent to Enhance Long-Context Abilities of Large Language Models|GraphReader]]。
