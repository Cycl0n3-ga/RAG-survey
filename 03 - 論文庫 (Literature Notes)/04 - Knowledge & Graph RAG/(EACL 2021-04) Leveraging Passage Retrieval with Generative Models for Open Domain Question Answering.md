---
paper_id: "Izacard2021_FusionInDecoder"
title: "Leveraging Passage Retrieval with Generative Models for Open Domain Question Answering"
authors:
  - "Gautier Izacard"
  - "Edouard Grave"
year: 2020
publication_year: 2021
venue: "Proceedings of the 16th Conference of the European Chapter of the Association for Computational Linguistics: Main Volume"
doi: "10.18653/v1/2021.eacl-main.74"
arxiv: "2007.01282"
url: "https://aclanthology.org/2021.eacl-main.74/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(EACL 2021-04) Leveraging Passage Retrieval with Generative Models for Open Domain Question Answering.pdf"
tags:
  - paper
  - passage-reader
  - evidence-fusion
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D07"
primary_domain: "D07"
secondary_domains:
  - "D09"
paradigm_tags: []
adjacent_interfaces: []
research_questions:
  - "multi_passage_evidence_fusion"
  - "retrieval_reader_architecture"
  - "context_utilization"
benchmark_ids:
  - "Natural Questions"
  - "TriviaQA"
  - "SQuAD Open"
dataset_ids:
  - "Natural Questions"
  - "TriviaQA"
  - "SQuAD v1.1"
metrics:
  - "Exact Match"
  - "F1"
---

# Leveraging Passage Retrieval with Generative Models for Open Domain Question Answering

> **版本與閱讀範圍：** arXiv:2007.01282 首次提交 2020-07-02；本地保存 arXiv 版本全文（6 頁）。正式論文刊於 EACL 2021 Main Volume，DOI `10.18653/v1/2021.eacl-main.74`。已讀本地全文並核對 ACL Anthology 正式書目；未逐段比對 proceedings PDF 與 arXiv 版本差異。以下表格位置採本地 PDF 頁碼。

## 一話摘要 (TL;DR)
Fusion-in-Decoder（FiD）分別編碼每篇檢索段落，再讓 decoder 跨段落注意力融合證據，使生成式 QA reader 能處理較多候選 passages。

## 研究背景與問題定義 (Problem Statement)
開放域 QA 需要從外部文件找答案；生成式 reader 有機會整合分散在多篇 passages 的資訊，但若把所有段落一起編碼，計算會隨上下文長度迅速增加。FiD 探討如何保留多篇段落間的證據融合，同時讓 encoder 對各 passage 分開計算。[§1–3, arXiv PDF pp. 1–3]

## 核心方法與技術架構 (Methodology & Architecture)
每篇檢索 passage 的標題、問題與內容串接後分開輸入 encoder；encoder 輸出表示再串接，供 decoder cross-attention 一起生成答案。因 encoder 不在 passages 之間做 self-attention，encoder 計算可隨 passage 數近線性擴展；decoder 仍可共同利用所有 passages 的表示。作者測試 BM25 與 DPR retrieval，reader 使用 T5 base 或 large。[§3, Figure 2, arXiv PDF pp. 2–3]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, arXiv PDF p. 3：** Fusion-in-Decoder large 在 Natural Questions、TriviaQA open test、TriviaQA hidden test、SQuAD Open test 的 Exact Match 分別為 `51.4, 67.6, 80.1, 56.7`，SQuAD F1 為 `63.2`；base 對應為 `48.2, 65.0, 77.1, 53.4`，F1 `60.6`。這是論文資料版本與其檢索、reader 設定下的結果。
- **Table 2, arXiv PDF p. 5：** 以 5 篇而非 100 篇 passages 訓練、評估時仍輸入 100 篇，NQ EM 為 45.0；額外以 100 passages 微調 1,000 steps 後可到 46.0。作者報告此 NQ 設定約 147 GPU-hours，對照從頭以 100 passages 訓練約 425 GPU-hours。該節是特定訓練預算比較。
- **評估條件：** T5 base/large 分別 220M/770M 參數；reader 以 100 篇 passage 為預設，passage 最長 250 word pieces。NQ 與 TriviaQA 使用 DPR，SQuAD 使用 BM25；訓練使用 64 張 Tesla V100 32GB GPU。Table 1 與其他研究使用不同資料切分／檢索設置時不可直接比較。[§4, arXiv PDF pp. 3–5]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- 獨立 passage encoding 降低 encoder 隨 passage 數增加的二次注意力負擔；decoder 集中融合編碼後的證據，讓多段落 reader 能直接生成答案。
- passage 數增加可提高表現，但會增加編碼與 decoder 的計算及記憶體需求；作者明確指出大量 passages 下仍需要提升效率。其 reader 依賴上游檢索品質，缺少正確證據時不會自動修正 retriever。[§3–5, arXiv PDF pp. 2–5]
- FiD 是 passage fusion reader 的基線，不包含 graph construction、graph retrieval 或 citation provenance，因此不能以它單獨代表現代 GraphRAG 整體系統。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將 FiD 主域列為 D07，因核心機制是 generator 如何利用多篇檢索 evidence；D09 表示答案由生成器彙整。它可作 graph-to-text 或 multi-source RAG 的 reader 對照，但比較時須固定 retriever、passage 數、reader 尺寸與資料集，並把檢索 recall 與 reader 的答案 EM/F1 分開。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式來源：[ACL Anthology 正式記錄與 PDF](https://aclanthology.org/2021.eacl-main.74/)；[arXiv:2007.01282](https://arxiv.org/abs/2007.01282)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(EACL 2021-04) Leveraging Passage Retrieval with Generative Models for Open Domain Question Answering.pdf|開啟本地 PDF 檔案]]（arXiv 版本）。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2022-05) KG-FiD - Infusing Knowledge Graph in Fusion-in-Decoder for Open-Domain Question Answering|KG-FiD]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2024-12) G-Retriever - Retrieval-Augmented Generation for Textual Graph Understanding and Question Answering|G-Retriever]]。
