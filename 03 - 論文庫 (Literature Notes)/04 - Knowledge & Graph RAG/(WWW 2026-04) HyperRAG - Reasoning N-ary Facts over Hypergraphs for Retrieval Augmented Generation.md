---
paper_id: "Lien2026_HyperRAG_Nary"
title: "HyperRAG: Reasoning N-ary Facts over Hypergraphs for Retrieval Augmented Generation"
authors:
  - "Wen-Sheng Lien"
  - "Yu-Kai Chan"
  - "Hao-Lung Hsiao"
  - "Bo-Kai Ruan"
  - "Meng-Fen Chiang"
  - "Chien-An Chen"
  - "Yi-Ren Yeh"
  - "Hong-Han Shuai"
year: 2026
publication_year: 2026
venue: "Proceedings of the ACM Web Conference 2026 (WWW 2026)"
doi: "10.1145/3774904.3792710"
arxiv: "2602.14470"
url: "https://arxiv.org/abs/2602.14470"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(WWW 2026-04) HyperRAG - Reasoning N-ary Facts over Hypergraphs for Retrieval Augmented Generation.pdf"
tags:
  - paper
  - hypergraph
  - n-ary-relations
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains:
  - "D04"
paradigm_tags:
  - "graph_rag"
adjacent_interfaces: []
research_questions:
  - "n_ary_graph_traversal"
  - "adaptive_retrieval_expansion"
  - "evidence_sufficiency_check"
benchmark_ids:
  - "WikiTopics-CLQA"
dataset_ids:
  - "HotpotQA"
  - "MuSiQue"
  - "2WikiMultiHopQA"
  - "WikiTopics-CLQA"
metrics:
  - "Exact Match"
  - "F1"
  - "MRR"
  - "Hits@10"
---

# HyperRAG: Reasoning N-ary Facts over Hypergraphs for Retrieval Augmented Generation

> **版本說明：** 正式發表於 WWW 2026（DOI 已由 ACM/Crossref metadata 核對）；本地全文是 arXiv:2602.14470 v1（2026-02-16），本文所有頁碼與數字均指此預印版，未以此推定出版版未變動。

## 一話摘要 (TL;DR)
本文研究在 n-ary hypergraph 上直接評分並自適應擴展推理鏈的檢索方法，並以 LLM 參數記憶引導的 beam-search 版本作比較。

## 研究背景與問題定義 (Problem Statement)
作者指出，把多實體、多角色的 n 元事實拆成二元邊會增加推理鏈長度並可能破壞事實整體性；另一方面，靜態 top-k 檢索難以隨超圖密度和查詢調整展開。本文提出 HyperRetriever 與 HyperMemory，分別測試學習式關係鏈檢索和 LLM 參數記憶引導搜尋。[§1–3, pp. 1–5]

## 核心方法與技術架構 (Methodology & Architecture)
- **HyperRetriever：** 以 MLP 結構與語意相容度分數評估 n-ary hyperedge／候選實體，並依局部密度調節擴展；先識別 query entities，再沿 incident hyperedges 逐步評分與展開，避免固定深度或固定分支數。[§3.1, pp. 3–5]
- **HyperMemory：** 以 LLM prompt 評分超邊與尾端實體，採 beam width 3、最大 depth 3；每層把累積證據交由 LLM 判斷是否足以回答，足夠即停止，否則繼續擴展。[§3.2, p. 5]
- **上下文組裝：** 依重要性分配 50% token 給 hyperedges、30% 給 entities、20% 給來源 chunks，超額未用預算再往下一類傳遞。[§3.1, p. 5]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **公開 QA 設定：** HotpotQA、MuSiQue、2WikiMultiHopQA 各以 EM/F1 評分。arXiv v1 Table 2, p. 6 中 HyperRetriever 分別為 42.50/43.65、13.50/14.15、34.00/34.06；HyperMemory 為 35.50/41.51、8.00/12.96、31.50/32.56。該表中 HyperGraphRAG 在 HotpotQA、MuSiQue 分別為 51.00/42.69、22.00/20.02，顯示 HyperRetriever 並非各資料集皆領先。作者回報其 2Wiki F1 相對該表最佳 baseline 提升 11.89%，該敘述依論文原報告保留。[§4.2.2, Table 2, p. 6]
- **跨域 WikiTopics-CLQA：** Table 1, p. 6 的平均 MRR/Hits@10 為 HyperRetriever 36.94/43.78、HyperGraphRAG 35.88/43.24；作者報告 11 個類別中 HyperRetriever 有 9 類排名第一。此結果是候選實體排序指標，不與 QA EM/F1 混用。[§4.3, Table 1, p. 6]
- **消融：** Table 3, p. 7 將 n-ary graph 換為 binary KG 後，平均 MRR 從 36.45 降至 34.15，Hits@10 從 40.59 降至 36.82；這是論文所測資料和設定下的差異。[§4.4.1, Table 3, p. 7]
- **設定與資源：** 使用 GPT-4o-mini；WikiTopics-CLQA 按 11 個 topic 分層抽 1%（約 1,000 題）測效率；實驗在單張 NVIDIA RTX 3090 24 GB 上進行。[§4.1, p. 5; §4.5, p. 8; Appendix A.1]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
HyperRetriever 的結果提示直接以高階關係做檢索可縮短推理鏈；但公開 QA 結果隨資料集與圖結構改變，HotpotQA／MuSiQue 上弱於 HyperGraphRAG，2Wiki 的 F1 才出現相對優勢。HyperMemory 證明單靠 LLM prompt／參數記憶評分在本文設定下表現較不穩定。效率比較使用 WikiTopics-CLQA 的分層 1% 子集，且論文將時間和 context token 量並列；不能將 asymptotic 分析當作所有圖規模下的實測延遲保證。[§4.2–4.5, pp. 6–8]

## 對本專案研究領域的實際意義 (Implications for Research Domains)
主要歸 D05，因核心問題是查詢時沿超圖擴展證據；D04 是必要的表示接口。它和 HyperGraphRAG 的重點不同：後者著重建立及運用 hypergraph 表示，本文著重在 n-ary 結構上的 query-time retrieval。HyperMemory 是一次查詢期間的搜尋策略，不等同 D11 persistent memory。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式書目：[ACM DOI](https://doi.org/10.1145/3774904.3792710)；[arXiv:2602.14470](https://arxiv.org/abs/2602.14470)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(WWW 2026-04) HyperRAG - Reasoning N-ary Facts over Hypergraphs for Retrieval Augmented Generation.pdf|開啟 arXiv v1 全文]]。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2025-12) HyperGraphRAG - Retrieval-Augmented Generation via Hypergraph-Structured Knowledge Representation|HyperGraphRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2025-11) OG-RAG - Ontology-grounded Retrieval-Augmented Generation for Large Language Models|OG-RAG]]。
