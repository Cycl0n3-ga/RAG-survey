---
paper_id: "Zheng2025_GRADA"
title: "GRADA: Graph-based Reranking against Adversarial Documents Attack"
authors:
  - "Jingjie Zheng"
  - "Aryo Pradipta Gema"
  - "Giwon Hong"
  - "Xuanli He"
  - "Pasquale Minervini"
  - "Youcheng Sun"
  - "Qiongkai Xu"
year: 2025
publication_year: 2025
venue: "EMNLP 2025"
doi: "10.18653/v1/2025.emnlp-main.1132"
arxiv: "2505.07546"
url: "https://aclanthology.org/2025.emnlp-main.1132/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(EMNLP 2025-11) GRADA - Graph-based Reranking against Adversarial Documents Attack.pdf"
tags:
  - paper
  - retrieval-security
  - adversarial-document-defense
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D14"
primary_domain: "D14"
secondary_domains:
  - "D05"
  - "D04"
paradigm_tags:
  - "graph_rag"
adjacent_interfaces: []
research_questions:
  - "adversarial-document-reranking"
  - "document-similarity-graph-defense"
  - "robust-retrieval-quality-tradeoff"
benchmark_ids:
  - "Natural Questions"
  - "MS MARCO"
  - "HotpotQA"
dataset_ids:
  - "Natural Questions"
  - "MS MARCO"
  - "HotpotQA"
metrics:
  - "Attack Success Rate"
  - "Exact Match"
source_version: arXiv:2505.07546v3
verified_version: arXiv:2505.07546v3
pdf_pages: 23
pdf_sha256: 8d471634bb9890498cbb6403ea2e5b7f981d6ce1ee7a4ecc69b49ee24076c97e
---

# GRADA: Graph-based Reranking against Adversarial Documents Attack

> **版本與閱讀範圍：** 預印本初次提交於 2025-05-12；本地全文為 arXiv v3（2025-09-18，23 頁）。正式發表於 EMNLP 2025，DOI `10.18653/v1/2025.emnlp-main.1132`。方法和實驗數據依本地 arXiv v3 全文；正式 Anthology metadata 已核，正式出版 PDF 未取得，故不宣稱已逐表比對正式版。

## 一話摘要 (TL;DR)
GRADA 在初步召回的文件間建立相似度圖，以資訊傳播重排並篩除與語料群體脫節的可疑文件，降低 query-similar poisoning 對 RAG 的攻擊成功率。

## 研究背景與問題定義 (Problem Statement)
一般 relevance reranker 專注 query–document 相關度；攻擊文件可刻意貼近 query，因而混入候選，同時又和多數良性文件差異很大。論文研究如何加入文件彼此的關係訊號，以降低 PoisonedRAG、PIA、Hotflip 與 Phantom 等攻擊對檢索及回答的影響。[§1–3, PDF pp.1–5]

## 核心方法與技術架構 (Methodology & Architecture)
先以 dense retriever 取得候選文件。GRADA 對候選文件建構加權無向圖，節點為文件，邊權為文件相似度；作者測試 Doc-to-Doc Similarity（D2DSIM）及 Hybrid Relevance Similarity（HRSIM），後者同時使用文件對文件與文件對 query 的分數。接著在文件圖上做迭代資訊傳播，使高相互支持的群集累積分數，低連結的候選受抑制；最後保留排名前 n 的文件供 generator 使用。[§3.1–3.3, PDF pp.3–5]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **資料與設定：** Natural Questions、MS MARCO、HotpotQA；使用 GPT-3.5-Turbo 0125、GPT-4o、Qwen2.5 與 LLaMA 3 等 victim LLM，Contriever 作初始 dense retriever。每資料集每次抽 100 題、3 個 random seeds；每個 attack–defense 條件共 900 題。作者只注入一篇 poisoned document，初始取回 10 篇並供 generator top 5 篇（Keyword Aggregation 依其自身流程）。[§4.1, PDF p.5]
- **Table 1, PDF p.6：** GPT-3.5-Turbo、PIA attack 下，NQ／MS MARCO 的無防禦 ASR 為 `98%/88%`，GRADA-D2DSIM-EBD 為 `2%/3%`，HRSIM 為 `2%/1%`；同一條件下 NQ 的 EM 為 `58.3%/61.7%`（D2DSIM-EBD/HRSIM），MS MARCO 為 `70.5%/74.3%`。對 PoisonedRAG，HRSIM 將 NQ／MS MARCO ASR 由 `55.7%/46.5%` 降至 `3%/8.5%`。這些數字限於表中兩個模型、攻擊、retrieval budget 與資料集。
- **Table 2, PDF p.7：** 對白箱 PoisonedRAG(Hotflip) 與 Phantom，HRSIM 在 GPT-3.5-Turbo 與 Llama3.1-8B 上多數條件降低 ASR；HotpotQA 上仍高於 NQ/MS MARCO 的一些攻擊案例，顯示 multi-hop 需求會影響穩定性。
- **Table 3, PDF p.7：** benign inputs 下有品質代價差異。例如 GPT-3.5-Turbo / HotpotQA，無防禦 EM `64.3%`、HRSIM `50.0%`；NQ 為 `58.6%` 對 `62.0%`。不能只看 attack ASR 而忽略乾淨 query 的 answer quality。

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 在候選集內利用文件間一致性，補上 query relevance 本身難以偵測孤立 poisoning 的情況；HRSIM 可結合文件相似度與 query relevance。論文在 benign-input 表格中也量測回答 EM，呈現防禦與正常任務效用的 trade-off。
- **限制：** 作者指出多跳推理攻擊上效果較弱，poisoned documents 數量增加時防禦能力下降；方法假設攻擊文件為少數，當其成為多數時效果衰減。[§5, PDF p.9]
- **比較邊界：** 攻擊者能力、poison 文件數量、top-k、LLM、retriever 及攻擊資料集皆會改變 ASR；ASR 下降不能等同於所有安全風險都解除。此處的 graph 是候選文件相似度圖，不是從文件抽取 entity–relation KG。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將其定位為 **D14 RAG Systems, Security & Privacy** 主域，D05 是 candidate reranking，D04 是文件相似度圖結構。它補足 GraphRAG 文獻中「圖也可當檢索防禦結構」這種不同於語義 KG traversal 的方向；分類為 `graph_rag` 是 repo 的廣義 cross-cutting 標記，不表示其圖是知識圖譜。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [EMNLP 2025 ACL Anthology record／DOI](https://aclanthology.org/2025.emnlp-main.1132/)；[arXiv:2505.07546 v3](https://arxiv.org/abs/2505.07546)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(EMNLP 2025-11) GRADA - Graph-based Reranking against Adversarial Documents Attack.pdf|開啟本地 PDF 檔案]]（arXiv v3）。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(USENIX Security 2025-08) PoisonedRAG - Knowledge Corruption Attacks to Retrieval-Augmented Generation of Large Language Models|PoisonedRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2026-07) LogicPoison - Logical Attacks on Graph Retrieval-Augmented Generation|LogicPoison]]。
