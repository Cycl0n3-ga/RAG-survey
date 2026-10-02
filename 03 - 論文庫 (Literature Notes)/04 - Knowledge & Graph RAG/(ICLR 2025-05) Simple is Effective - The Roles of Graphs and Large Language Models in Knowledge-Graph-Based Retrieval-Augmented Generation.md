---
paper_id: "Li2025_SubgraphRAG"
title: "Simple is Effective: The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation"
authors:
  - "Mufei Li"
  - "Siqi Miao"
  - "Pan Li"
year: 2024
publication_year: 2025
venue: "ICLR 2025"
doi: null
arxiv: "2410.20724"
url: "https://proceedings.iclr.cc/paper_files/paper/2025/hash/11e1900e680f5fe1893a8e27362dbe2c-Abstract-Conference.html"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(ICLR 2025-05) Simple is Effective - The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation.pdf"
tags:
  - paper
  - kgqa
  - subgraph-retrieval
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains: []
paradigm_tags:
  - "graph_rag"
  - "multi_hop_rag"
adjacent_interfaces: []
research_questions:
  - "subgraph_retrieval"
  - "retrieval_granularity"
  - "retrieval_efficiency"
benchmark_ids:
  - "WebQSP"
  - "CWQ"
dataset_ids:
  - "WebQSP"
  - "CWQ"
  - "WebQSP-sub"
  - "CWQ-sub"
metrics:
  - "Macro-F1"
  - "Hit"
  - "Recall"
---

# Simple is Effective: The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation

> **版本與來源：** 預印本 arXiv:2410.20724 發布於 2024 年；本地 PDF 為 ICLR 2025 正式版。

## 一話摘要 (TL;DR)
SubgraphRAG 以訓練式三元組評分器挑選 query-specific 子圖，讓 LLM 在可調整的圖證據量上回答 KGQA 問題。

## 研究背景與問題定義 (Problem Statement)
作者聚焦 KG-based RAG 中的檢索效能與效率：路徑限制式檢索可能漏掉有用三元組，而大量候選圖資訊又會提高推理 token 與延遲。研究問題是如何從 query-centered KG 子圖中取得適量相關三元組，再交由 LLM 推理；本文並非從無結構文件建構知識圖譜的方法。[pp. 1–3, §1–2]

## 核心方法與技術架構 (Methodology & Architecture)
SubgraphRAG 以 topic entities 為中心縮小候選圖，使用預訓練文字 encoder 表示問題及圖三元組，訓練輕量 MLP 對候選 triples 作平行打分，依分數取 top-K 組成子圖，再用 LLM 讀取三元組並回答。訓練時沒有人工標註的 query–relevant-subgraph，作者以 question topic entity 到答案 entity 的 shortest-path triples 作弱監督；檢索子圖的 K 可調整。[§3, pp. 3–5; §4.1, pp. 6–7]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 3, p. 7：** WebQSP / CWQ 上，SubgraphRAG + GPT-4o（top 100 triples）報告 Macro-F1 76.46 / 59.08、Hit 89.80 / 66.69；同表不同生成器、top-K 與 cross-dataset 設定有不同數字，須分開解讀。
- **Table 1–2, pp. 6–7：** 檢索評估分別檢查 shortest-path triples、GPT-4o 標註 relevant triples、答案實體的 recall，並比較 wall-clock retrieval time。這些是不同 relevance 定義；作者亦說明 KG query time 未計入，預先計算全 KG embedding 的時間／記憶體 trade-off 需另列。
- **資源與模型：** 使用 gte-large-en-v1.5（434M）作文字 encoder；文中檢索時間在 48GB NVIDIA RTX 6000 Ada 上測量。LLM 比較包括 Llama 3.1 8B/70B-Instruct、GPT-4o-mini、GPT-4o 等，API 模型版本列於 §4.2。測試 KG 為 Freebase；資料集為 WebQSP、CWQ 及答案在 KG 中的子集。[§4, pp. 6–9]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** triple-level parallel scoring 不要求所有證據必須落在單一路徑；可調整 top-K 子圖大小；論文把檢索 recall、wall-clock 與下游 QA 分開量測。
- **限制與代價：** 弱監督使用最短路徑可能不涵蓋所有有效證據；全文稱 top-K 增加不保證每種 reasoner 都變好。KG query 時間被排除，整體系統延遲不可直接由其 retrieval time 代表；預計算 embedding 導致記憶體及建置成本亦需另計。資料和任務限於英文 Freebase KGQA。
- **比較邊界：** Table 3 混合引用基線和重跑基線、不同 LLM 與不同 context K。GPT-4o 數字不可和 ToG/RoG 的不同模型或資料協議直接排名。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將其歸為 **D05 Query Understanding & Retrieval**，paradigm tags 為 `graph_rag`、`multi_hop_rag`。它補足 relation-path planning（RoG）及 LLM-guided traversal（ToG）以外的可學習 triple scoring 檢索策略；`secondary_domains` 留空，避免把 downstream generation 當成主要研究問題。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式全文：[ICLR 2025 proceedings PDF](https://proceedings.iclr.cc/paper_files/paper/2025/file/11e1900e680f5fe1893a8e27362dbe2c-Paper-Conference.pdf)；[arXiv:2410.20724](https://arxiv.org/abs/2410.20724)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(ICLR 2025-05) Simple is Effective - The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Think-on-Graph - Deep and Responsible Reasoning of Large Language Model on Knowledge Graph|ToG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Reasoning on Graphs - Faithful and Interpretable Large Language Model Reasoning|RoG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2024-12) G-Retriever - Retrieval-Augmented Generation for Textual Graph Understanding and Question Answering|G-Retriever]]。
