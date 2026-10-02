---
paper_id: "Mavromatis2025_GNNRAG"
title: "GNN-RAG: Graph Neural Retrieval for Efficient Large Language Model Reasoning on Knowledge Graphs"
authors:
  - "Costas Mavromatis"
  - "George Karypis"
year: 2024
publication_year: 2025
venue: "Findings of ACL 2025"
doi: "10.18653/v1/2025.findings-acl.856"
arxiv: "2405.20139"
url: "https://aclanthology.org/2025.findings-acl.856/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) GNN-RAG - Graph Neural Retrieval for Efficient Large Language Model Reasoning on Knowledge Graphs.pdf"
tags:
  - paper
  - kgqa
  - graph-neural-network
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
  - "kg_subgraph_retrieval"
  - "answer_entity_ranking"
  - "retrieval_efficiency"
benchmark_ids:
  - "WebQSP"
  - "CWQ"
  - "MetaQA-3"
dataset_ids:
  - "WebQSP"
  - "CWQ"
  - "MetaQA-3"
metrics:
  - "Hit"
  - "F1"
  - "H@1"
  - "Hit@k"
source_version: Findings ACL 2025 proceedings
verified_version: Findings ACL 2025 proceedings
pdf_pages: 18
pdf_sha256: 656e5eba9d188c31e2dc945746a41f3477df82ca9a8ddbc6711441ef91a661ba
---

# GNN-RAG: Graph Neural Retrieval for Efficient Large Language Model Reasoning on Knowledge Graphs

> **版本與來源：** arXiv 預印本於 2024 年發布；本地 PDF 為 Findings of ACL 2025 正式版，正式題名含 “Efficient”。筆記依 ACL 版頁碼與表格。

## 一話摘要 (TL;DR)
GNN-RAG 以問題條件化的圖神經網路在 KG 子圖中找答案候選，抽取 topic entity 至候選答案的最短路徑作文字證據，再由 LLM 回答。

## 研究背景與問題定義 (Problem Statement)
作者指出，LLM-based KG traversal 可能需要多次昂貴生成呼叫；直接把稠密圖子結構交給 LLM 又會帶來大量 context。本文研究如何把 GNN 用作圖檢索器，先在圖結構中推分答案節點，再只將候選答案相關路徑文字化供 LLM 使用。[§1、§3–4, pp. 16682–16686]

## 核心方法與技術架構 (Methodology & Architecture)
模型先連結問題實體並擷取局部子圖；問題與 KG relation 透過共享預訓練語言模型編碼，GNN 依問題關係語義反覆傳遞訊息，預測候選答案節點。接著抽取 question entities 到候選答案的 shortest paths，轉為自然語言 KG triples 放進 prompt 生成答案。可選的 Retrieval Augmentation (RA) 將 GNN 路徑和 RoG relation-path retriever 結果合併；另測試以 GNN 結果路由 query。[§4, pp. 16685–16687]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, p. 16687：** WebQSP / CWQ 上 GNN-RAG Hit 為 85.7 / 66.8、F1 為 71.3 / 59.4；加入 RA 後為 Hit 90.7 / 68.7、F1 73.5 / 60.4。表註指出 GNN-RAG、RoG 等使用微調 7B Llama2，長 context 組使用 Llama 3.1-8B；設定不同者不可直接排名。
- **Table 3, p. 16688：** CWQ 上 GNN-RAG 的中位 KG tokens 為 114、Hit@1 52.9、Hit@10 64.1、F1 59.4；RoG、SubgraphRAG 的取回 token 數及協議不同，應視為該表特定比較。
- **Table 7, p. 16689：** 在 WebQSP、7B Llama 生成器、A10G fp16 設定下，報告 retrieval / generation / total 分鐘：RoG 11/31/42、SubgraphRAG 0.1/58/58.1、GNN-RAG 0.9/29/30。該延遲比較限定在作者所列實作設定。
- **資源與設定：** 使用 WebQSP、CWQ、MetaQA-3；GNN 訓練報告在 GeForce RTX 3090、128GB RAM 機器進行；LLM 實驗使用 4 張 A100。Appendix D.3（p. 16698；PDF p. 17）將兩種訓練分開：下游 LLM 在 2 張 A100-80G 上以 30K 資料跑 1 epoch 需超過 12 小時；GNN 在 GeForce RTX 3090 上的相同資料量／epoch 設定需少於 15 分鐘、少於 8GB GPU memory。這是不同模型與硬體的資源報告，不能當作同硬體速度比較。評估包含 Hit、F1、H@1、Hit@k。[§5–6, pp. 16686–16689; Appendices C, D.3]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** GNN 可在表示空間中處理較深圖交互，避免每一步都由 LLM 導航；只把答案候選相關 shortest paths 傳給 LLM，控制圖 token 數。單一圖檢索流程可不增加 LLM 呼叫。
- **限制：** 作者明確指出它假設推理所用 KG 子圖含有答案節點；entity linking 出錯會違反此假設。路徑 context 使用簡單提示，且本文範圍是 KG retrieval，不包含專門的 GNN–LLM 迭代互動。GNN 訓練與建立問題子圖仍需計算資源。[§8, p. 16689]
- **比較邊界：** Table 1 主結果、Table 3 token 分析及 Table 7 latency 是不同切面；不可將各表的分數／資源混為單一排名。表中一些 baseline 為引用結果，需注意原實驗來源。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將其歸為 **D05 Query Understanding & Retrieval**，以 D04 表示 KG/GNN 表示與索引介面、D07 表示檢索路徑如何序列化供 LLM 使用；paradigm tags 為 `graph_rag`、`multi_hop_rag`。這是本 repo 的 mapping。它補足 ToG/RoG 的生成式圖搜尋路線，代表以 GNN 計算候選節點及證據鏈的檢索設計。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式全文：[ACL Anthology PDF](https://aclanthology.org/2025.findings-acl.856.pdf)；[ACL Anthology paper record / DOI](https://aclanthology.org/2025.findings-acl.856/)；[arXiv:2405.20139](https://arxiv.org/abs/2405.20139)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) GNN-RAG - Graph Neural Retrieval for Efficient Large Language Model Reasoning on Knowledge Graphs.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Reasoning on Graphs - Faithful and Interpretable Large Language Model Reasoning|RoG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2025-05) Simple is Effective - The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation|SubgraphRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2024-12) G-Retriever - Retrieval-Augmented Generation for Textual Graph Understanding and Question Answering|G-Retriever]]。
