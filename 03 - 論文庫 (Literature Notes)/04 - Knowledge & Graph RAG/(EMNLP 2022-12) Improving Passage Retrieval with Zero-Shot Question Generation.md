---
paper_id: "Sachan2022_UPR"
title: "Improving Passage Retrieval with Zero-Shot Question Generation"
authors:
  - "Devendra Sachan"
  - "Mike Lewis"
  - "Mandar Joshi"
  - "Armen Aghajanyan"
  - "Wen-tau Yih"
  - "Joelle Pineau"
  - "Luke Zettlemoyer"
year: 2022
publication_year: 2022
venue: "EMNLP 2022"
doi: "10.18653/v1/2022.emnlp-main.249"
arxiv: "2204.07496"
url: "https://aclanthology.org/2022.emnlp-main.249/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(EMNLP 2022-12) Improving Passage Retrieval with Zero-Shot Question Generation.pdf"
tags:
  - paper
  - passage-reranking
  - zero-shot-retrieval
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains: []
paradigm_tags: []
adjacent_interfaces: []
research_questions:
  - "passage_reranking"
  - "zero_shot_retrieval"
benchmark_ids:
  - "BEIR"
dataset_ids:
  - "Natural Questions"
  - "TriviaQA"
  - "WebQuestions"
  - "SQuAD Open"
metrics:
  - "retrieval accuracy"
  - "nDCG@10"
  - "Recall@100"
  - "Exact Match"
source_version: arXiv:2204.07496v4
verified_version: arXiv:2204.07496v4
pdf_pages: 18
pdf_sha256: 3e8d200937c8acb25866f453d6354f473aa8e681958a2a281ea4edf43d7f81d4
---

# Improving Passage Retrieval with Zero-Shot Question Generation

> **版本與閱讀範圍：** arXiv:2204.07496 v4（2023-04-03，18 頁；record 註記為 EMNLP 2022 camera-ready version）全文已讀；ACL Anthology 正式書目已核，尚未逐項比對 proceedings PDF 差異。正式論文頁 3781–3797，DOI `10.18653/v1/2022.emnlp-main.249`。

## 一話摘要 (TL;DR)
UPR 對初步檢索出的 passage 計算其生成原始 query 的 zero-shot likelihood，作為無任務特定微調的 passage reranker。

## 研究背景與問題定義 (Problem Statement)
監督式 retriever／reranker 需要 query–passage labels 或任務訓練資料；作者研究預訓練生成式語言模型能否在不針對檢索 benchmark fine-tune 的條件下，重新排序第一階段檢索候選。問題是候選排序，不是新索引結構或 GraphRAG orchestration。[§1–2, arXiv PDF pp. 1–3]

## 核心方法與技術架構 (Methodology & Architecture)
給定問題 q 與候選 passage z，使用 T0 等 pretrained language model 的 log p(q|z) 作 relevance score，對 top-K 候選重排；沒有另以 query-passage relevance labels 訓練該 reranker。第一階段候選仍來自 BM25、Contriever 等 retrievers。評估另把 reranked evidence 輸入 FiD 等 reader 做 open-domain QA。[§2–3, arXiv PDF pp. 2–4]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 2, arXiv PDF p. 5：** 對 top-1,000 候選以 T0-3B rerank，四個 QA retrieval datasets（Natural Questions、TriviaQA、WebQuestions、SQuAD Open）合併平均 top-20 accuracy，BM25 由 68.2 升至 BM25+UPR 79.5；Contriever 由 70.0 升至 80.1。表內各資料集與 top-20/top-100 結果不同，不能只憑平均值推論每種 corpus 都有同幅改善。
- **Table 6, arXiv PDF p. 8：** BEIR macro-average nDCG@10 / Recall@100：Contriever 36.0/60.1，rerank 後 44.6/66.3；BM25 41.6/63.6，rerank 後 44.9/68.0。這些是論文採用的 BEIR evaluation 設定，和 Table 2 的 QA retrieval accuracy 不同，不可跨表直接比較。
- **§3.5, arXiv PDF p. 4：** 實驗於 V100-32GB GPU cluster 執行。**Limitations, arXiv PDF p. 10：** 對大量 passage 重排 latency 高，因 cross-attention 成本隨 query/passage token 長度和 PLM layers 增加；因此 top-1,000 設定不能視為免費 reranking。

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- 不需要目標資料集的 relevance fine-tuning，提供以生成式 PLM likelihood 進行 zero-shot reranking 的可重現基線。
- 高計算量限制可重排候選數；候選品質仍由第一階段 retriever 決定，reranking 無法找回未召回 passage。score 也依賴 PLM、tokenization 和 prompt/conditioning 實作。
- Retrieval 指標的提高不等於 reader answer accuracy、faithfulness 或端到端 latency 同比例改善；論文另報 QA 結果時須在各自設定下比較。[§4, Tables 2, 6–7]

## 對本專案研究領域的實際意義 (Implications for Research Domains)
D05 primary：方法直接排序 query 的候選 evidence。graph-based retrievers 可將 UPR 作文字段落 reranking baseline，但需要相同 first-stage candidate pool 才能隔離圖擴展／圖遍歷的作用；亦須報告候選預算與 reranker latency。僅使用 graph corpus 或被 GraphRAG 論文引用，不會令 UPR 本身成為 graph method。此 mapping 為 repo taxonomy 判斷。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式書目：[ACL Anthology](https://aclanthology.org/2022.emnlp-main.249/)；預印本與版本記錄：[arXiv:2204.07496](https://arxiv.org/abs/2204.07496)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(EMNLP 2022-12) Improving Passage Retrieval with Zero-Shot Question Generation.pdf|開啟本地 PDF 檔案]]（arXiv v4）。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(EMNLP 2020-11) Dense Passage Retrieval for Open-Domain Question Answering|DPR]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EACL 2021-04) Leveraging Passage Retrieval with Generative Models for Open Domain Question Answering|FiD]]。
