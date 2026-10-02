---
paper_id: "Tan2024_PoG"
title: "Paths-over-Graph: Knowledge Graph Empowered Large Language Model Reasoning"
authors:
  - "Xingyu Tan"
  - "Xiaoyang Wang"
  - "Qing Liu"
  - "Xiwei Xu"
  - "Xin Yuan"
  - "Wenjie Zhang"
year: 2024
publication_year: 2025
venue: "The Web Conference 2025 (WWW 2025)"
doi: "10.1145/3696410.3714892"
arxiv: "2410.14211"
url: "https://doi.org/10.1145/3696410.3714892"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(WWW 2025-04) Paths-over-Graph - Knowledge Graph Empowered Large Language Model Reasoning.pdf"
tags:
  - paper
  - knowledge-graph
  - path-reasoning
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
  - "multi_entity_path_search"
  - "dynamic_path_exploration"
  - "path_pruning_cost_quality_tradeoff"
benchmark_ids:
  - "CWQ"
  - "WebQSP"
  - "GrailQA"
  - "Simple Questions"
  - "WebQuestions"
dataset_ids:
  - "CWQ"
  - "WebQSP"
  - "GrailQA"
  - "Simple Questions"
  - "WebQuestions"
metrics:
  - "Accuracy"
  - "LLM call count"
  - "Token input"
source_version: arXiv:2410.14211v4
verified_version: arXiv:2410.14211v4
pdf_pages: 18
pdf_sha256: c10d4fff7c6ba2b57df7241218f82c278cd1dadcbcfd8b0f0f717d71a6fd8029
---

# Paths-over-Graph: Knowledge Graph Empowered Large Language Model Reasoning

> **版本與閱讀範圍：** arXiv 首發 2024-10；目前本地全文為 arXiv v4（2025-03 修訂，18 頁），而非 ACM publisher PDF。已閱讀該全文；WWW 2025 正式出版 metadata（DOI、日期、頁碼）依 Crossref；正式 PDF 因 ACM 存取限制未取回，出版版差異待比對。

## 一話摘要 (TL;DR)
PoG 在 topic entities 的局部圖上動態找多跳路徑，結合 question decomposition、LLM 補充路徑與三級 pruning，為 multi-hop／multi-entity KGQA 提供可追溯 path evidence。

## 研究背景與問題定義 (Problem Statement)
常見 KG reasoning 將問題分成一條關係序列或逐個實體／relation 搜尋，可能忽視多 topic entities 間的連結，也可能把大量 KG 候選放進模型。PoG 研究如何依問題預估深度、找出連通 topic entities 的路徑，並用圖結構、語言模型及預訓練相似度模型分階段縮小候選。[§1–4, pp. 1–6]

## 核心方法與技術架構 (Methodology & Architecture)
初始化時辨識 topic entities、把問題切成子問題並預測探索深度，抽取其 Dmax-hop 局部子圖；先作 topic-entity path exploration，若不足則以 LLM prediction 補充可能 entities 形成新路徑，最後 node expansion。Path pruning 有 fuzzy semantic selection、LLM precise path selection 及利用 graph structure 的 BranchReduced selection。PoG-E 是採不同 entity/edge graph reduction 的變體。主實驗使用 Freebase，GPT-3.5-Turbo 與 GPT-4；Wmax=Dmax=3。[§4.1–4.3, pp. 4–7]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, p. 7：** GPT-3.5-Turbo 的 PoG / PoG-E Accuracy：CWQ 74.7/71.9，WebQSP 93.9/90.9，GrailQA 91.6/87.6，Simple Questions 80.8/78.3，WebQuestions 81.8/76.9；GPT-4 的 PoG / PoG-E 分別為 81.4/78.5、96.7/95.4、94.4/91.4、84.0/81.2、84.6/82.0。這些主要比較採 in-context learning；表內 supervised baseline 採不同訓練條件，不可直接按表格單列作同設定比較。
- **Table 3, p. 8：** 子圖縮減後實體數量在 CWQ 減少 54%、WebQSP 25%、GrailQA 52%、WebQuestions 26%。
- **Table 4, Appendix B.1, p. 11：** CWQ 上 PoG BranchReduced path selection Accuracy 79.3、輸入 tokens 101,455、平均 LLM calls 9.7；Fuzzy+Precise selection 為 81.4、216,884 tokens、9.1 calls。WebQSP 對應 93.0 / 328,742 / 9.3 與 93.9 / 617,448 / 7.5。這呈現 token 節省與精確度取捨，不等同於 GPU 推論延遲。
- **硬體與生成設定：** 作者報告 Intel Xeon Gold 6248R、NVIDIA A5000、512GB RAM；使用 OpenAI GPT-3.5／GPT-4 API，探索 temperature 0.4、回答 temperature 0、max generation 256 tokens。[Appendix B, pp. 14–15]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 明確處理多 topic entities 並保留可檢視的 KG reasoning paths；Graph-based BranchReduced selection 能降低 path context tokens，提供成本／準確率的可操作折衷。
- **限制與成本：** 依賴 entity linking 與 Freebase/SPARQL 查詢；局部圖擷取可能未涵蓋答案所需節點，作者指出 GrailQA 未連結 topic entity 會影響推理。探索需多次 LLM API calls，完整路徑 selection 也可能消耗大量輸入 tokens。GPT-4/GPT-3.5/API 成本無法直接從 tokens 表換算成通用部署價格。
- **版本限制：** arXiv v4 不是 publisher PDF；正式出版版逐表變更尚未核對。正式 publication metadata 與所讀 PDF 的版本角色已分開記錄。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 分類為 **D05 Query Understanding & Retrieval**，D04 表示局部 KG/path representation 與 pruning，D07 表示被保留的 reasoning path 如何組成 prompt context。paradigm tags 為 `graph_rag`、`multi_hop_rag`。PoG 的路徑在檢索後被用作證據，但它同時允許 LLM 預測與 KG evidence 結合；閱讀比較時應另看 path faithfulness/error analysis，而非只看 accuracy。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式 publication metadata：[Crossref DOI 10.1145/3696410.3714892](https://doi.org/10.1145/3696410.3714892)；正式會議與全文版本註記：[arXiv:2410.14211（接受 WWW 2025；本地 v4）](https://arxiv.org/abs/2410.14211)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(WWW 2025-04) Paths-over-Graph - Knowledge Graph Empowered Large Language Model Reasoning.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Reasoning on Graphs - Faithful and Interpretable Large Language Model Reasoning]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2025-05) Think-on-Graph 2.0 - Deep and Faithful Large Language Model Reasoning with Knowledge-guided Retrieval Augmented Generation]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) SimGRAG - Leveraging Similar Subgraphs for Knowledge Graphs Driven Retrieval-Augmented Generation]]。
