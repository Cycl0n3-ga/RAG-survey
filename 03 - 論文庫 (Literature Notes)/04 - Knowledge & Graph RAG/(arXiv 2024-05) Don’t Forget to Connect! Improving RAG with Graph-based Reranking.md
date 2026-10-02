---
paper_id: "Dong2024_GRAGReranking"
title: "Don't Forget to Connect! Improving RAG with Graph-based Reranking"
authors:
  - "Jialin Dong"
  - "Bahare Fatemi"
  - "Bryan Perozzi"
  - "Lin F. Yang"
  - "Anton Tsitsulin"
year: 2024
publication_year: null
venue: "arXiv"
doi: "10.48550/arXiv.2405.18414"
arxiv: "2405.18414"
url: "https://arxiv.org/abs/2405.18414"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(arXiv 2024-05) Don’t Forget to Connect! Improving RAG with Graph-based Reranking.pdf"
tags:
  - paper
  - graph-reranking
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
  - "graph_aware_document_reranking"
  - "document_relation_features"
  - "pairwise_ranking_objective"
benchmark_ids:
  - "Natural Questions"
  - "TriviaQA"
dataset_ids:
  - "Natural Questions"
  - "TriviaQA"
metrics:
  - "MRR"
  - "MHits@10"
  - "MTRR"
  - "TMHits@10"
source_version: arXiv:2405.18414v1
verified_version: arXiv:2405.18414v1
pdf_pages: 19
pdf_sha256: 803d7e5295b4a7f2256a35179a9142d1b1c52b59939b10c46eadec97ac0443da
---

# Don't Forget to Connect! Improving RAG with Graph-based Reranking

> **版本與閱讀範圍：** arXiv:2405.18414 首次提交 2024-05-28，arXiv 只有 v1（19 頁）；此稿為預印本，未查得正式會議／期刊出版資訊。已閱讀全文，以下頁碼依本地 arXiv PDF。

## 一話摘要 (TL;DR)
G-RAG 在 DPR 檢索後建立 document graph，利用問題–文件 AMR 表徵及跨文件連結訓練 GNN reranker，重新排序候選文件供 reader 使用。

## 研究背景與問題定義 (Problem Statement)
ODQA 中有些答案文件與問題字面關聯較弱，單一 query–document relevance 分數可能將其排低。本文研究如何把候選文件間共享的語意／實體連結加入重排，並避免將所有 AMR token 不加選擇地加入模型特徵。[§1–2, pp. 1–3]

## 核心方法與技術架構 (Methodology & Architecture)
先以 DPR 為每個問題取得 100 篇文件；對 question–document pair 以 AMRBART 解析 AMR，將文件文字及由 question 節點出發的 AMR shortest paths 作 node features，再以共享 AMR nodes／edges 數構成 document graph edge features。GNN 更新文件節點表示後依 query embedding 打分重排。作者另以 pairwise ranking loss 訓練 G-RAG-RL，並提出處理 tied rankings 的 MTRR、TMHits@10 指標。[§3–4.2, pp. 3–8]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, p. 8：** 以 NQ／TriviaQA 的 dev/test 評估。G-RAG 的 NQ MRR dev/test = 25.1/24.2、MHits@10 = 49.1/47.2；TriviaQA MRR = 18.5/18.3、MHits@10 = 38.5/39.1。G-RAG-RL 對應 NQ = 27.3/25.7、49.2/47.4；TriviaQA = 19.8/18.3、42.9/39.4。此處清楚分開 dev/test，避免把兩組欄位混讀。
- **Table 2, p. 8：** PaLM 2 L reranker 的 NQ／TriviaQA 表現低於 G-RAG-RL；作者指出生成分數產生大量 ties，故採 tied-ranking metrics。
- **設置：** 每題先由 DPR 檢索 100 篇、每篇約 100 words；GNN 為 2-layer GCN，使用 NQ、TriviaQA；作者報告實驗在 Tesla A100 40GB GPU 執行。[§4.1, pp. 6–8]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 將圖用在 retrieval 後的 candidate reranking，不要求對整個知識圖譜做 traversal；共享 AMR 結構能連結字面 query score 較弱的文件。PAIRWISE loss 對不平衡的正負文件排序有針對性。
- **限制與成本：** 必須對每題 top-100 的 question-document pairs 建 AMR，並訓練 GNN；AMR 解析與 document graph 建構帶來額外前處理。實驗限於 NQ／TriviaQA 與該 DPR/AMRBART 流程；不代表一般 RAG corpus 的端到端 latency。作者亦指出 document graph 規模較小，較複雜 GNN 不一定更合適。[§4.1–4.3, pp. 6–9; Appendix B]
- **比較邊界：** arXiv 預印本表格報告 reranker 的排序指標，不能與生成端 EM／Accuracy 作直接比較。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 分類為 **D05 Query Understanding & Retrieval**；D04 表示文件圖與 AMR 結構特徵，D07 表示排序結果如何改變 reader 所見上下文。paradigm tag 採 `graph_rag`。須與 GRAG（textual ego-subgraph 检索）及 KG-FiD（passage graph 兩階段 reader reranking）分開：本篇的 graph nodes 是候選文件，圖只在排序階段介入。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 原始預印本：[arXiv:2405.18414](https://arxiv.org/abs/2405.18414)；[arXiv-issued DOI](https://doi.org/10.48550/arXiv.2405.18414)（不是正式發表 DOI）。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(arXiv 2024-05) Don’t Forget to Connect! Improving RAG with Graph-based Reranking.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2022-05) KG-FiD - Infusing Knowledge Graph in Fusion-in-Decoder for Open-Domain Question Answering]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings NAACL 2025-04) GRAG - Graph Retrieval-Augmented Generation]]。
