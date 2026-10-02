---
paper_id: "Chen2026_PathRAG"
title: "PathRAG: Pruning Graph-Based Retrieval Augmented Generation with Relational Paths"
authors:
  - "Boyu Chen"
  - "Zirui Guo"
  - "Zidan Yang"
  - "Yuluo Chen"
  - "Junze Chen"
  - "Zhenghao Liu"
  - "Chuan Shi"
  - "Cheng Yang"
year: 2025
publication_year: 2026
venue: "Proceedings of the AAAI Conference on Artificial Intelligence 40(36)"
doi: "10.1609/aaai.v40i36.40268"
arxiv: "2502.14902"
url: "https://ojs.aaai.org/index.php/AAAI/article/view/40268"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(AAAI 2026-03) PathRAG - Pruning Graph-Based Retrieval Augmented Generation with Relational Paths.pdf"
tags:
  - paper
  - graph-path-retrieval
  - prompt-construction
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains:
  - "D07"
paradigm_tags:
  - "graph_rag"
adjacent_interfaces: []
research_questions:
  - "path_retrieval"
  - "context_construction"
  - "retrieval_efficiency"
benchmark_ids:
  - "UltraDomain"
  - "SQuALITY"
  - "SummScreen"
dataset_ids:
  - "Legal"
  - "History"
  - "Biology"
  - "Mix"
  - "SQuALITY"
  - "SummScreen"
metrics:
  - "LLM-as-a-judge win rate"
  - "BLEU"
  - "ROUGE"
  - "METEOR"
source_version: AAAI 2026 proceedings
verified_version: AAAI 2026 proceedings
pdf_pages: 9
pdf_sha256: 7b004da59de37027172df1b3f042e0bca48b90840a088b7e0481ffb3afb7112c
---

# PathRAG: Pruning Graph-Based Retrieval Augmented Generation with Relational Paths

> **版本與來源：** arXiv 預印本於 2025 年發布；本地 PDF 對應 AAAI 2026 正式版，刊於第 40 卷第 36 期，頁 30183–30191。

## 一話摘要 (TL;DR)
PathRAG 從 indexing graph 擷取相關節點間的高可信 relational paths，以 flow-based pruning 移除低貢獻路徑，並按可信度安排 prompt 順序。

## 研究背景與問題定義 (Problem Statement)
作者認為若干 graph-based RAG 檢索結果有冗餘、而且常把節點與邊平鋪到 prompt，可能降低答案邏輯性並增加 token 使用。PathRAG 聚焦既有文字關聯圖上的 query-time 路徑篩選和上下文組織。摘要中的「主要限制是冗餘」是作者對其研究對象的診斷，不能泛化成所有 GraphRAG 系統的共同瓶頸。[pp. 30183–30185, §1–3]

## 核心方法與技術架構 (Methodology & Architecture)
流程分成三階段：先用 LLM 從 query 抽取關鍵字，透過 embedding 相似度取得 query-related nodes；再由節點沿鄰接邊傳遞衰減資源，利用距離感知的 early stopping 剪枝，估計候選路徑可靠度並保留 top-K；最後串接路徑內節點／邊的文字描述，按可靠度遞增排列，使高分路徑靠近 prompt 尾端。[pp. 30184–30186, §3]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, p. 30187：** 六個 Legal、History、Biology、Mix、SQuALITY、SummScreen 資料集上，以 GPT-4o-mini judge 計算答案兩兩比較勝率。對所有列出的 baseline 平均，PathRAG 在 comprehensiveness、diversity、logicality、relevance、coherence 的平均 win rate 分別為 62.52%、65.37%、60.68%、59.92%、59.43%。這些是 LLM judge win rates，不是絕對正確率。
- **Table 4, p. 30188：** SQuALITY 人寫摘要上的自動指標中，PathRAG BLEU-1/2 為 35.41/13.81、ROUGE-1/2 F1 為 15.35/3.95、METEOR 18.53；作者報告相對最佳 baseline 平均改善 7.06%。
- **設定：** 所有方法使用 GPT-4o-mini，embedding 使用 text-embedding-3-small，indexing graph 遵循 GraphRAG 建構方法；輸入長度上限 8,000 tokens。PathRAG 固定 N=40、K=15、α=0.7；對含隨機性的元件平均十次試驗。作者在 Agriculture 與 CS 調參，再測其他資料集。論文未列明本實驗硬體，因此不能據此作硬體延遲或成本比較。[§4, pp. 30186–30189]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 同一 base LLM 及固定 prompt token 上限下比較多種 GraphRAG / text-RAG baseline；消融測試 flow pruning、路徑順序及 path-based prompt 的作用。
- **限制與代價：** 五項主要品質指標來自 GPT-4o-mini 評審，受評審模型與 prompt 影響；SQuALITY/SummScreen 以外多缺少標準化 reference answer，作者亦提出未來加入人工評估。檢索複雜度分析依賴取回節點數遠小於全圖的設定。索引建圖成本與硬體未充分列明。
- **比較邊界：** win rate 只能解讀為該批模型、資料集與 judge 條件下的相對偏好，不能等同 factuality 或普遍性能優勢。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將 PathRAG 放在 **D05 Query Understanding & Retrieval**，次領域 D07，因為貢獻同時涵蓋候選路徑檢索與 prompt context 組裝；使用 `graph_rag`。這個 mapping 是 repo taxonomy 建議。它也提供與 LightRAG 的鄰居擴展、GraphRAG 的 community context 比較的路徑單位案例；此比較需維持本文同一 GPT-4o-mini 控制條件。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [AAAI 2026 正式論文頁與 PDF](https://ojs.aaai.org/index.php/AAAI/article/view/40268)；[DOI](https://doi.org/10.1609/aaai.v40i36.40268)；[arXiv:2502.14902](https://arxiv.org/abs/2502.14902)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(AAAI 2026-03) PathRAG - Pruning Graph-Based Retrieval Augmented Generation with Relational Paths.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2024-10) LightRAG - Simple and Fast Retrieval-Augmented Generation|LightRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2024-04) From Local to Global - A Graph RAG Approach to Query-Focused Summarization|GraphRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2025-05) Simple is Effective - The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation|SubgraphRAG]]。
