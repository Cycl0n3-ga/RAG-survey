---
paper_id: "Zhou2026_HyperRAG_Hyperbolic"
title: "Query-Aware Knowledge Retrieval via Hyperbolic Structuring"
authors:
  - "Chuang Zhou"
  - "Junnan Dong"
  - "Yilin Xiao"
  - "Shengyuan Chen"
  - "Su Dong"
  - "Di Yin"
  - "Xing Sun"
  - "Zhaozhuo Xu"
  - "Xiao Huang"
year: null
publication_year: 2026
venue: "ACL 2026 (Long Papers)"
doi: "10.18653/v1/2026.acl-long.986"
arxiv: null
url: "https://aclanthology.org/2026.acl-long.986/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(ACL 2026-07) Query-Aware Knowledge Retrieval via Hyperbolic Structuring.pdf"
tags:
  - paper
  - hyperbolic-embeddings
  - query-aware-graph
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
  - "query_aware_graph_construction"
  - "hyperbolic_retrieval"
  - "incremental_graph_updates"
benchmark_ids: []
dataset_ids:
  - "HotpotQA"
  - "2WikiMultiHopQA"
  - "MuSiQue"
metrics:
  - "String-Match Accuracy"
  - "GPT-evaluation Accuracy"
---

# Query-Aware Knowledge Retrieval via Hyperbolic Structuring

> **版本與來源：** ACL Anthology 正式全文，ACL 2026 long paper, pp. 21601–21614；DOI 10.18653/v1/2026.acl-long.986。未找到對應 arXiv ID，因此 preprint year 與 arXiv 均留空。ACL PDF 為本地核對全文版本。

## 一話摘要 (TL;DR)
HyperRAG 將靜態共現邊與逐查詢推導的隱式關係合併成 passage graph，再以雙曲嵌入檢索 query-relevant passages。

## 研究背景與問題定義 (Problem Statement)
作者聚焦於固定、query-agnostic 圖無法呈現個別問題所需推理關係的情況，並提出把 query-specific connections 融入全域圖結構的方案。論文的研究主張是查詢驅動的圖結構能補足只靠共現或固定 ontology 的連結。[§1, pp. 1–2]

## 核心方法與技術架構 (Methodology & Architecture)
1. **Explicit edges：** 從每個 passage 抽 key terms；兩段共享關鍵詞比例至少 0.15 即連邊，每段最多 5 個這類鄰居。[§3.1, p. 2]
2. **Implicit edges：** LLM 將 query 分解成 atomic reasoning units，依各子問題取回 evidence passages，並建立 query-specific links；再把 implicit tree 與 explicit tree 的共同節點合併、避免 cycle，形成查詢導向的融合樹。[§3.1, pp. 2–3]
3. **Hyperbolic representation：** passage embeddings 投影到 Poincaré ball，以鄰接節點距離訓練結構表示。新 query 產生的子圖採局部增量訓練，作者報告約每 100 個 query 做一次全圖 recalibration；推論選取最接近 query 的約 3 個 leaf passages。[§3.2–3.3, pp. 3–4]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **主表：** HotpotQA、2WikiMultiHopQA、MuSiQue 每項資料集各 1,000 問題，語料約 10,000 chunks；GPT-4o-mini 生成。Table 1, p. 5 同時報 String-Match Accuracy 與 GPT-evaluation Accuracy。HyperRAG 的兩項數值依序為 HotpotQA 57.4/58.9、2Wiki 50.8/52.3、MuSiQue 34.7/35.4。表內兩項分數不是 EM/F1。[§4.1–4.2, Table 1, p. 5]
- **消融：** Table 2, p. 7 的 GPT-evaluation accuracy 顯示，只用 semantic retrieval 為 45.1/43.5/23.2；加入 explicit edges 為 49.8/46.9/26.3；implicit edges 為 55.2/50.0/31.9；完整方法為 58.9/52.3/35.4（HotpotQA/2Wiki/MuSiQue）。[§4.4, Table 2, p. 7]
- **速度：** 作者報告對約 1,000 queries、10,000 passages 建圖需數分鐘；優化設定下每 query 的 retrieval+generation 約 1.5 秒。論文未在實驗設定中交代 GPU 或硬體型號，故本筆記不補推硬體條件。[§4.3, pp. 5–6]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
查詢專屬連結由 LLM 推導，能表達靜態共現圖沒有的任務線索；代價是每個 query 需要額外推理並更新向量表示。作者指出雙曲搜尋不直接相容 FAISS 等高度優化向量檢索庫，效率略低，並提出平行化作為未來方向。[§4.3, p. 6; Limitations, p. 9] 三個 QA 語料及 GPT judge 僅代表該設定；不宜據此推廣至其他域或更大規模語料。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
主歸 D04，因主要技術貢獻是把顯式／隱式邊融合成可學習的圖表示；D05 涵蓋 query-driven evidence linking 與 top-k retrieval，D07 涵蓋檢索後提供給生成模型的 passage context。此分類是 repo taxonomy mapping，非作者原分類。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 原始全文與 metadata：[ACL Anthology entry](https://aclanthology.org/2026.acl-long.986/)、[DOI](https://doi.org/10.18653/v1/2026.acl-long.986)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(ACL 2026-07) Query-Aware Knowledge Retrieval via Hyperbolic Structuring.pdf|開啟 ACL 正式版 PDF]]。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2024-11) GraphReader - Building Graph-based Agent to Enhance Long-Context Abilities of Large Language Models|GraphReader]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(WWW 2026-04) HyperRAG - Reasoning N-ary Facts over Hypergraphs for Retrieval Augmented Generation|HyperRAG (n-ary)]]。
