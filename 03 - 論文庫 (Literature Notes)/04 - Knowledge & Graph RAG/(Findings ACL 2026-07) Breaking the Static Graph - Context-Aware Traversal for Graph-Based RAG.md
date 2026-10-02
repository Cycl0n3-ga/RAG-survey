---
paper_id: "Lau2026_CatRAGTraversal"
title: "Breaking the Static Graph: Context-Aware Traversal for Graph-Based RAG"
authors: ["Kwun Hang Lau", "Fangyuan Zhang", "Boyu Ruan", "Yingli Zhou", "Qintian Guo", "Ruiyuan Zhang", "Xiaofang Zhou"]
year: 2026
publication_year: 2026
venue: "Findings of ACL 2026"
doi: "10.18653/v1/2026.findings-acl.290"
arxiv: "2602.01965"
url: "https://aclanthology.org/2026.findings-acl.290/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(arXiv 2026-02) CatRAG - Context-Aware Traversal for Robust Retrieval-Augmented Generation.pdf"
tags: ["paper", "query-aware-traversal", "reasoning-completeness"]
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains: ["D04", "D13"]
paradigm_tags: ["graph_rag", "multi_hop_rag"]
adjacent_interfaces: []
research_questions: ["query_aware_graph_traversal", "evidence_chain_completeness", "retrieval_evaluation"]
benchmark_ids: ["MuSiQue", "2WikiMultiHopQA", "HotpotQA", "HoVer"]
dataset_ids: ["MuSiQue", "2WikiMultiHopQA", "HotpotQA", "HoVer"]
metrics: ["Recall@5", "F1", "Accuracy", "Full Chain Retrieval", "Joint Success Rate"]
---

# Breaking the Static Graph: Context-Aware Traversal for Graph-Based RAG

> **版本界線：** ACL Anthology 正式版收錄於 Findings ACL 2026，頁 5849–5863；本地 PDF 是 arXiv v1（2026-02-02），預印題名為 “CatRAG: Context-Aware Traversal for Robust Retrieval-Augmented Generation”。出版社 PDF 端點連線逾時，因此正式版全文與預印本差異未核。下列表格數字依 arXiv v1 頁碼整理。

## 一話摘要 (TL;DR)
CatRAG 在 HippoRAG 2 的 PPR 圖檢索上加入 symbolic anchoring、query-aware dynamic edge weighting 和 key-fact passage enhancement，以補齊多跳證據鏈。

## 研究背景與問題定義 (Problem Statement)
靜態圖檢索的 edge weight 在索引時固定，可能忽略 query-specific relevance，使隨機漫步偏向高 degree hub，造成部分 recall 尚可但完整推理鏈缺失。本文研究 traversal 時如何調整 query-conditioned navigation，並以 evidence-chain completeness 補充一般 recall 指標。[§1–3, arXiv PDF pp. 1–4]

## 核心方法與技術架構 (Methodology & Architecture)
1. **Symbolic anchoring：** 以弱 entity constraints 引導 random walk。
2. **Query-aware dynamic edge weighting：** 由 LLM 評估邊與 query 的相關性，動態調整 traversal 權重。
3. **Key-fact passage enhancement：** 對可能包含關鍵事實的來源 passage 加權。

最後用 PPR 排序 passages，再交給 Llama reader。這裡的 reasoning completeness 是評估完整取回鏈的能力，不等於 D06 的充分性判定或 retry/stop controller。[§3–4, pp. 3–6]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 2, arXiv p. 7：** 四資料集 Recall@5，CatRAG 在 MuSiQue / 2Wiki / HotpotQA / HoVer 為 64.9 / 87.0 / 89.5 / 76.8；HippoRAG 2 為 61.4 / 85.9 / 87.1 / 71.2。HoVer 隨機抽 1,000 claims。
- **Table 3, arXiv p. 7：** Llama-3.3-70B-Instruct reader 下 CatRAG F1 / HoVer accuracy 為 45.0 / 69.7 / 71.4 / 69.0；HippoRAG 2 為 43.2 / 68.1 / 69.4 / 67.2。
- **Table 4–5, arXiv pp. 7–8：** 另報 Full Chain Retrieval (FCR) 與 Joint Success Rate (JSR)，並對三個模組作消融。
- **設定：** GPT-4o-mini 作 LLM 元件，text-embedding-3-small 作 retriever，Llama-3.3-70B-Instruct 作 reader，使用 top-5 passages；結構方法採相同 extractor/retriever 控制比較。正式版全文與此 arXiv v1 數字是否一致待核。[§4–6, pp. 6–9]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 同時評估 passage recall、QA、FCR/JSR，避免以部分命中推定完整推理成功；包含模組消融。
- **限制與代價：** Dynamic edge weighting 需 query-time LLM inference，增加延遲和計算量；粗粒度 pruning 只能緩解。僅用 text-embedding-3-small 以隔離拓樸效果；作者未公開完整程式碼。HoVer 使用抽樣資料。[§7, p. 9]
- **比較邊界：** 部分 HippoRAG 2 基線結果標記為引用文獻數字；需與本文重跑結果區分。作者的 “Static Graph Fallacy” 是研究診斷，不是所有固定圖檢索必然失效的證明。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將其歸入 **D05 Query Understanding & Retrieval**，次領域 D04（圖權重／表示）、D13（完整證據鏈評估）；使用 `graph_rag`、`multi_hop_rag`。這是 repo mapping。它補足 PPR retrieval 的 query-conditioned traversal；不因 “complete evidence chain” 一詞就視為已解決 D06 evidence sufficiency。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [ACL Anthology 正式紀錄／DOI／頁碼](https://aclanthology.org/2026.findings-acl.290/)；[正式版 PDF](https://aclanthology.org/2026.findings-acl.290.pdf)（本環境連線逾時）；[arXiv:2602.01965 v1](https://arxiv.org/abs/2602.01965)；[可取得全文 PDF](https://arxiv.org/pdf/2602.01965)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(arXiv 2026-02) CatRAG - Context-Aware Traversal for Robust Retrieval-Augmented Generation.pdf|開啟本地 arXiv v1 PDF]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICML 2025-07) From RAG to Memory - Non-Parametric Continual Learning for Large Language Models|HippoRAG 2]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) GNN-RAG - Graph Neural Retrieval for Efficient Large Language Model Reasoning on Knowledge Graphs|GNN-RAG]]。
