---
paper_id: "Liang2025_FastToG"
title: "Fast Think-on-Graph: Wider, Deeper and Faster Reasoning of Large Language Model on Knowledge Graph"
authors:
  - "Xujian Liang"
  - "Zhaoquan Gu"
year: 2025
publication_year: null
venue: "arXiv"
doi: "10.48550/arXiv.2501.14300"
arxiv: "2501.14300"
url: "https://arxiv.org/abs/2501.14300"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(arXiv 2025-01) Fast Think-on-Graph - Wider, Deeper and Faster Reasoning of Large Language Model on Knowledge Graph.pdf"
tags:
  - paper
  - knowledge-graph
  - community-search
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
  - "multi_hop_rag"
adjacent_interfaces: []
research_questions:
  - "community_level_graph_search"
  - "local_community_detection"
  - "community_to_text_representation"
benchmark_ids:
  - "CWQ"
  - "WebQSP"
  - "QALD"
  - "ZSRE"
  - "TREx"
  - "Creak"
dataset_ids:
  - "CWQ"
  - "WebQSP"
  - "QALD"
  - "ZSRE"
  - "TREx"
  - "Creak"
metrics:
  - "Accuracy"
  - "LLM call count"
---

# Fast Think-on-Graph: Wider, Deeper and Faster Reasoning of Large Language Model on Knowledge Graph

> **版本與閱讀範圍：** arXiv 首發 2025-01-24，arXiv:2501.14300 v1（11 頁）；未查得正式發表紀錄。已讀本地預印本全文，表格頁碼依 arXiv PDF。

## 一話摘要 (TL;DR)
FastToG 將 query-time 局部 KG 社群當成多條推理鏈的擴展單位，並以 modularity pruning 與 community-to-text 轉換降低逐節點 traversal 的搜尋負擔。

## 研究背景與問題定義 (Problem Statement)
逐節點 KG 搜尋在圖稠密時容易產生大量候選路徑；只擴一條鏈又可能無法觸及較遠關聯。FastToG 把多路徑寬度與社群級擴展結合，處理如何在擴大候選關係的同時限制每輪提供給 LLM 的資訊與呼叫數。[§1–3, pp. 1–5]

## 核心方法與技術架構 (Methodology & Architecture)
每輪從 topic entity 周圍抽取 local subgraph，做 community detection；以 modularity-based coarse pruning 和 LLM fine pruning 挑選社群，W 條鏈各自擴展。社群可用規則 Triple-to-Text 或 Graph-to-Text 表述，合併給 LLM 判斷是否足以回答，若不足則續輪。作者設定 W=3、Dmax=5、最大社群大小 4，主比較用 Louvain；最壞呼叫數公式為 2WDmax+Dmax+2，即此設定下最多 37 次 LLM 呼叫。[§3, pp. 2–5; §4, p. 6]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, p. 6：** GPT-4o-mini 下，FastToG Graph-to-Text (g2t) 在 CWQ、WebQSP、QALD、ZSRE、TREx、Creak 的 Accuracy 為 45.0、65.8、55.9、54.2、68.6、96.0；對照 ToG（n-d 1-w）為 42.9、63.6、54.9、54.0、64.2、95.4。
- **Table 2, p. 6：** Llama-3-70B-Instruct 下，g2t 對應 Accuracy 為 46.2、66.4、54.3、67.9、64.7、94.5；同列 ToG 對照為 40.3、62.4、51.6、64.8、61.2、93.3。模型與各資料集均限定於作者報告設定。
- **效率：** 論文以 LLM call count／平均推理深度衡量效率，並未報告完整硬體 latency 或 tokens/sec。Table 3, p. 7 顯示社群偵測算法間的準確率差異普遍小於 1%，random partition 較低；作者亦指出最大社群設為 8 時部分結果退步。
- **比較邊界：** 數字只可按各表中同模型、同資料集、同欄位比較；跨 GPT-4o-mini 與 Llama-3-70B 不作直接排名。

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 社群是多節點搜尋單位，可縮短推理鏈；局部 community search 避免每個 query 都全圖重分群。圖到文字方式保留部分結構提示，並可與較簡單的 triple 展平方式對照。
- **限制與成本：** 大社群會帶入雜訊、增加 community detection 時間且降低可解釋性；Graph-to-Text 本身可能產生 hallucination，作者的檢查亦指出此問題。文中效率主要以 LLM 呼叫次數代理，不能視為實際端到端時延／API 費用結論。此為 arXiv v1，尚無正式版本供比較。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 分類為 **D05 Query Understanding & Retrieval**，D04 記錄社群／子圖檢索單位，D07 記錄 community-to-text 對 evidence context 的序列化。paradigm tags 為 `graph_rag`、`multi_hop_rag`。與 ToG 的節點／relation 搜尋相比，FastToG 在局部圖中以 community 為擴展單位；它的檢索期 local communities 不等於 GraphRAG corpus indexing 階段預先建立的 community reports。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 原始預印本：[arXiv:2501.14300](https://arxiv.org/abs/2501.14300)；[arXiv-issued DOI](https://doi.org/10.48550/arXiv.2501.14300)（不是正式發表 DOI）。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(arXiv 2025-01) Fast Think-on-Graph - Wider, Deeper and Faster Reasoning of Large Language Model on Knowledge Graph.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Think-on-Graph - Deep and Responsible Reasoning of Large Language Model on Knowledge Graph]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2025-05) Think-on-Graph 2.0 - Deep and Faithful Large Language Model Reasoning with Knowledge-guided Retrieval Augmented Generation]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2024-04) From Local to Global - A Graph RAG Approach to Query-Focused Summarization]]。
