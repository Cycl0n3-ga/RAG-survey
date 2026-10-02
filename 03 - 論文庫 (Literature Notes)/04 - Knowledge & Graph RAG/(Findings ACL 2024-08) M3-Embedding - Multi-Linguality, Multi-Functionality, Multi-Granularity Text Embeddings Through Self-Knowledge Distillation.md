---
paper_id: "Chen2024_M3Embedding"
title: "M3-Embedding: Multi-Linguality, Multi-Functionality, Multi-Granularity Text Embeddings Through Self-Knowledge Distillation"
authors:
  - "Jianlyu Chen"
  - "Shitao Xiao"
  - "Peitian Zhang"
  - "Kun Luo"
  - "Defu Lian"
  - "Zheng Liu"
year: 2024
publication_year: 2024
venue: "Findings of the Association for Computational Linguistics: ACL 2024"
doi: "10.18653/v1/2024.findings-acl.137"
arxiv: "2402.03216"
url: "https://aclanthology.org/2024.findings-acl.137/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(Findings ACL 2024-08) M3-Embedding - Multi-Linguality, Multi-Functionality, Multi-Granularity Text Embeddings Through Self-Knowledge Distillation.pdf"
tags:
  - paper
  - text-embedding
  - hybrid-retrieval
verification_status: "verified"
last_verified: "2026-10-03"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D04"
primary_domain: "D04"
secondary_domains:
  - "D05"
paradigm_tags:
  - "hybrid_rag"
adjacent_interfaces: []
research_questions:
  - "multilingual_retrieval"
  - "embedding_representation"
  - "multi_vector_retrieval"
  - "cross_lingual_retrieval"
  - "multilingual_long_document_retrieval"
benchmark_ids:
  - "MIRACL"
  - "MKQA_retrieval"
  - "MLDR"
  - "NarrativeQA_retrieval"
dataset_ids:
  - "MIRACL"
  - "MKQA"
  - "MLDR"
  - "NarrativeQA"
metrics:
  - "nDCG@10"
  - "Recall@100"
source_version: arXiv:2402.03216v5
verified_version: arXiv:2402.03216v5
pdf_pages: 18
pdf_sha256: eb38e53565da260dc1f3d49708f45441936447a7f3c7d7ef025ff62ea3e1e575
additional_verified_versions:
  - "Findings ACL 2024 (official PDF text: title/authors, Sections 2–4, Tables 1–15, Limitations, Appendix B.1–B.3)"
version_comparison_status: "scoped_text_comparison"
author_name_note: "ACL bibliography lists Jianlyu Chen; both the official PDF title page and local arXiv v5 print Jianlv Chen."
---

# M3-Embedding: Multi-Linguality, Multi-Functionality, Multi-Granularity Text Embeddings Through Self-Knowledge Distillation

> **版本與閱讀範圍：** 本地 PDF 保留 arXiv:2402.03216v5（2025-12-12，18 頁）。2026-10-03 已讀 Findings ACL 2024 官方 PDF 可抽取文字（頁 2318–2335，18 頁），核對核心方法、Tables 1–15 的文字／數值、Limitations 與 Appendix B；已核表格數值相符，書目與部分引用文字有差異，不能宣告兩版全文完全相同。正式 PDF binary 未保存本地、圖像未作正式版視覺比對。下述結果引用正式印刷頁碼，PDF 頁碼亦適用本地 v5。ACL 書目頁的第一作者為 “Jianlyu Chen”，兩版 PDF 封面均為 “Jianlv Chen”；`authors` 沿用正式書目索引，明示拼寫差異。[正式全文 (2024/08), pp. 2318–2335](https://aclanthology.org/2024.findings-acl.137.pdf)；[ACL 書目 (2024/08)](https://aclanthology.org/2024.findings-acl.137/)

## 一話摘要 (TL;DR)
M3-Embedding 將 dense、learned sparse、multi-vector 三種檢索功能、多語檢索及最長 8,192 token 的輸入支援整合於一個 embedding model，並以 self-knowledge distillation 融合各檢索頭的相關性訊號。

## 研究背景與問題定義 (Problem Statement)
單一 dense embedding、不同語言的 representation，以及 passage-level 與長文件檢索常由不同模型／流程處理；不同 retrieval head 的訓練目標也可能互不相容。作者提出共同模型及訓練方式，處理多語、跨語言、多功能檢索與不同文字粒度。[§1–3, arXiv PDF pp. 1–5]

## 核心方法與技術架構 (Methodology & Architecture)
模型由同一 encoder 產生 dense 向量、token importance weights（sparse retrieval）及 token-level vectors（late interaction）。訓練分階段收集無監督、多語監督與合成長文件資料；self-knowledge distillation 將不同檢索功能的融合分數轉為教師訊號，協調各 head。efficient batching／split-batch 用於訓練，與服務端檢索效率分開看。[正式全文 (2024/08), §3／Appendix B.3, pp. 2321–2323、2331–2333](https://aclanthology.org/2024.findings-acl.137.pdf)

**檢索協議不可略去：** §4.1 的 Dense 用 Faiss 取 top-1,000，Sparse 用 Lucene 取 top-1,000；Multi-vec 對 Dense top-200 rerank。Dense+Sparse 對兩者 top-1,000 聯集以權重 `(1, 0.3, 0)` 重排；All 對 Dense top-200 以 `(1, 0.3, 1)` 重排。All 不是三個通道以相同候選預算各自全庫搜尋。§4.3 長文件條件的兩組融合權重另為 `(0.2, 0.8, 0)` 與 `(0.15, 0.5, 0.35)`，不可將 §4.1 權重套到所有表格。[正式全文 (2024/08), §4.1／§4.3, pp. 2323、2325（PDF pp. 6、8）](https://aclanthology.org/2024.findings-acl.137.pdf)

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, p. 2323（PDF p. 6）：** MIRACL dev、18 語言，All macro average nDCG@10 為 71.5；Dense 69.2、Sparse **53.9**、Multi-vec 70.5。原筆記的 sparse 45.3 是誤植；45.3 實為 Table 2 的 MKQA Sparse Recall@100。這是指定 retrieval 協議的排序品質，不代表生成品質或成本效益。[正式全文 (2024/08), Tables 1–2, pp. 2323–2324](https://aclanthology.org/2024.findings-acl.137.pdf)
- **Table 2, p. 2324（PDF p. 7）：** MKQA 跨語言 retrieval、25 語言，All macro average Recall@100 為 75.5；這是將 MKQA 問題用於英文 Wikipedia 檢索的協議，不是 MKQA 原始 QA 生成分數。[正式全文 (2024/08), §4.2／Table 2](https://aclanthology.org/2024.findings-acl.137.pdf)
- **Tables 3–4, p. 2325（PDF p. 8）：** MLDR multilingual long-document test、13 語言的 All nDCG@10 平均為 65.0（輸入上限 8,192 token）；NarrativeQA 的 All nDCG@10 為 61.7，亦為 8,192 token。Table 7 將 MLDR 資料表題寫作 MultiLongDoc；`dataset_ids` 指資料，`benchmark_ids` 指上述評測協議。[正式全文 (2024/08), §4.3／Tables 3–4、7, pp. 2325、2332](https://aclanthology.org/2024.findings-acl.137.pdf)
- **Tables 5–6, p. 2326（PDF p. 9）：** MIRACL dev 消融中，加入 self-knowledge distillation 後 Sparse 為 53.9，移除該步為 36.7；Dense 69.2 對 68.7，Multi-vec 70.5 對 69.3。Dense 的多階段訓練消融依序為 fine-tune 60.5、RetroMAE+fine-tune 66.1、再加 unsupervised pre-training 69.2。[正式全文 (2024/08), Tables 5–6](https://aclanthology.org/2024.findings-acl.137.pdf)
- **訓練資源並非未提供：** Appendix B.1, p. 2331（PDF p. 14），RetroMAE 階段用 32×A100-40GB／20,000 steps；大量無監督階段用 96×A800-80GB／25,000 steps；fine-tuning 用 24×A800-80GB，先約 6,000 steps warm-up 再作 unified self-knowledge distillation（6,000 不是全部 fine-tuning steps）。Table 10, p. 2333（PDF p. 16）報 split-batch 的 per-device maximum batch size，不能解讀為服務吞吐量。論文未提供統一端到端 RAG latency、TTFT 或服務成本帳。[正式全文 (2024/08), Appendix B.1–B.3／Table 10, pp. 2331–2333](https://aclanthology.org/2024.findings-acl.137.pdf)

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- 單一 encoder 提供多種 retrieval score，便於在相同模型下測試通道互補性；All 在所報 benchmark 多數取得較高檢索分數，但實際融合仍增加索引型態與候選／打分管理複雜度。
- 作者指出真實資料泛化、超過 8,192 token 的文件，以及不同語言族的表現差異仍需研究；「支援超過 100 語言」不代表已全面評測這些語言。[正式全文 (2024/08), Limitations, p. 2326（PDF p. 9；原筆記誤標 p. 12）](https://aclanthology.org/2024.findings-acl.137.pdf)
- Table 1–4 的指標、語言和資料集不同，數字不可跨表直接排序；本文沒有提供足以對照所有模型的統一服務硬體／記憶體／延遲成本表。Table 11 的 BM25 Lucene Analyzer 在 MLDR 為 64.1，M3 Sparse 為 62.2；BM25 原主表採 XLM-R tokenizer（53.6）。因此不應把該表結果推廣為 sparse head 無條件優於 BM25。[正式全文 (2024/08), Table 11, p. 2333（PDF p. 16）](https://aclanthology.org/2024.findings-acl.137.pdf)
- 已核 Tables 1–15 數值及上述方法／資源一致，不等於全部文字一致：例如 v5 §4.2 的 BEIR 引用顯示 `(?)`，正式版為 Thakur et al. (2021)，references 也有格式／年份／條目差異。進行二次引用應回到各篇原始文獻，不能由 v5 的缺失推定正式版也缺失。詳見 [[00 - 導覽與心智圖 (Navigation & MOC)/GraphRAG Version Verification - 2026-10-03|版本核對報告]]。[正式全文 (2024/08), §4.2／References, pp. 2324、2326–2330](https://aclanthology.org/2024.findings-acl.137.pdf)

## 對本專案研究領域的實際意義 (Implications for Research Domains)
建議 D04 primary（共同 encoder 與 searchable representations），D05 secondary（多通道檢索與分數融合）。M3 可為 graph-heavy RAG 評估提供文字 retrieval baseline，用來分辨 graph index 的效果是否只是來自更佳 text retriever；必須固定 query、corpus、candidate budget 與 generator，並把索引資源／latency 單獨報告。它本身不是 GraphRAG 或圖譜表示方法。該定位是本 repo taxonomy 判斷。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式書目：[ACL Anthology](https://aclanthology.org/2024.findings-acl.137/)；[正式版 PDF（已核可抽取文字）](https://aclanthology.org/2024.findings-acl.137.pdf)；本地版本：[arXiv:2402.03216v5](https://arxiv.org/abs/2402.03216v5)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(Findings ACL 2024-08) M3-Embedding - Multi-Linguality, Multi-Functionality, Multi-Granularity Text Embeddings Through Self-Knowledge Distillation.pdf|開啟本地 PDF 檔案]]（arXiv v5）。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(SIGIR 2022-07) SPLADE v2 - Sparse Lexical and Expansion Model for Information Retrieval|SPLADE v2]]、[[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(NAACL 2022-07) ColBERTv2 - Effective and Efficient Retrieval via Lightweight Late Interaction|ColBERTv2]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2026-05) LinearRAG - Linear Graph Retrieval Augmented Generation on Large-scale Corpora|LinearRAG]]。
