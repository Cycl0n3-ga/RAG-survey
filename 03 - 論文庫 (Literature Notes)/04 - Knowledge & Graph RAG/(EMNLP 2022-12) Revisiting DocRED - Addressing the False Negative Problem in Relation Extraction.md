---
paper_id: "Tan2022_ReDocRED"
title: "Revisiting DocRED - Addressing the False Negative Problem in Relation Extraction"
authors:
  - "Qingyu Tan"
  - "Lu Xu"
  - "Lidong Bing"
  - "Hwee Tou Ng"
  - "Sharifah Mahani Aljunied"
year: 2022
publication_year: 2022
venue: "Proceedings of the 2022 Conference on Empirical Methods in Natural Language Processing"
doi: "10.18653/v1/2022.emnlp-main.580"
arxiv: "2205.12696"
url: "https://aclanthology.org/2022.emnlp-main.580/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(EMNLP 2022-12) Revisiting DocRED - Addressing the False Negative Problem in Relation Extraction.pdf"
tags:
  - paper
  - relation-extraction
  - dataset-quality
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "dataset"
taxonomy_version: "v2"
taxonomy_home: "D03"
primary_domain: "D03"
secondary_domains:
  - "D13"
paradigm_tags: []
adjacent_interfaces: []
research_questions:
  - "relation_extraction_annotation_quality"
  - "false_negative_evaluation"
  - "knowledge_extraction_error"
benchmark_ids:
  - "DocRED"
dataset_ids:
  - "DocRED"
  - "Re-DocRED"
metrics:
  - "F1"
  - "Ign_F1"
  - "Precision"
  - "Recall"
source_version: arXiv:2205.12696v3
verified_version: arXiv:2205.12696v3
pdf_pages: 16
pdf_sha256: 43a61ddc83f84b5cc5cb6c2beca9baa0f88c3f928758589090663863b2c9ed87
---

# Revisiting DocRED - Addressing the False Negative Problem in Relation Extraction

> **版本與閱讀範圍：** arXiv:2205.12696 首次提交 2022-05-25；本地 PDF 為 arXiv v3（2023-06-16，16 頁）。正式論文刊於 EMNLP 2022，頁 8472–8487，DOI `10.18653/v1/2022.emnlp-main.580`。已讀 arXiv v3 全文並核對 ACL 正式 metadata；尚未逐項比對 v3 與正式版的正文差異，實驗頁碼以下採 arXiv PDF 頁碼。

## 一話摘要 (TL;DR)
Re-DocRED 重新標註 DocRED 文件中漏掉的關係三元組，顯示標註 false negatives 會壓低文件級關係抽取系統的測得分數。

## 研究背景與問題定義 (Problem Statement)
DocRED 採用 machine recommendation 再由人修訂，以擴大文件級 relation extraction 標註規模；作者指出此流程漏掉不少可由文件推出的 relation triples，導致原資料的負例中混入未標註正例，影響訓練與評測。論文分析漏標來源並建立修訂資料集，目標是更完整地測量文件級關係抽取。[§1–2, arXiv PDF pp. 1–4]

## 核心方法與技術架構 (Methodology & Architecture)
作者以 iterative annotation pipeline 重查 DocRED：先為實體對生成候選關係、利用規則與模型提出可能漏標三元組，再由人工閱讀文件判斷候選是否能由原文推出；每個候選由兩位標註者核對，意見衝突交由第三人處理。首輪重新標註 4,053 篇文件；最終 Re-DocRED 修訂原有訓練、開發與測試文件。[§3.1–3.2, Table 5, arXiv PDF pp. 5–6]

Re-DocRED 保留與 DocRED 相同的資料分割文件數（3,053 train、500 dev、500 test），但平均每篇文件的標註 triples 明顯增加：train/dev/test 為 28.1/34.6/34.9，原 DocRED train/dev 為 12.5/12.3。這代表它是重標註版本，不能和 DocRED 當作彼此獨立的新 benchmark 資料。[Table 5, arXiv PDF p. 6]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 6, arXiv PDF p. 7：** 在相同模型與分割下，ATLOP 的 Re-DocRED test F1 為 77.56，原 DocRED test F1 為 63.20（+14.36）；KD-DocRE 為 78.28 對 64.07（+14.21）。表中結果是論文所列模型的平均分數，並不表示資料集重標註本身提高模型能力；主要變化是標註內容與評分基準。
- **Table 8, arXiv PDF p. 8：** Re-DocRED 上 ATLOP 的 test F1 為 77.56，Ign_F1 為 76.82；該表另按頻繁／長尾、同句／跨句關係拆分表現。這些數值仍依論文資料、模型和評分協議解讀。
- **評估條件：** 文件級 relation extraction；報告 F1、Ign_F1，並另討論 positive relation classification 與人類評估。正文主要用 ATLOP、DocuNET、KD-DocRE、JEREX 等模型；未把 Re-DocRED 分數當成任何下游 RAG 準確度的估計。[§4, Tables 6–9, arXiv PDF pp. 7–9]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- 修訂標註為分析知識抽取錯誤提供更可靠的資料依據，也凸顯 `false negative` 會同時污染訓練負例與評測 gold labels。
- 全量人工檢查成本高；作者討論的推薦—修訂與多輪核驗仍仰賴標註者判讀。有限標註經人工複核仍可能漏掉由更長距離或隱含推理才可成立的關係。[§3、§6、Limitations, arXiv PDF pp. 5–6, 10]
- Re-DocRED 的分數提升不應解讀為所有 relation extraction 系統在新任務上自然更好；改變的是 gold annotation completeness 和評估條件。它也不是 GraphRAG 方法，不能單獨證明下游 graph construction 或 RAG 品質改善。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將資料集歸 D03，因核心貢獻是關係抽取標註修訂；D13 表示它提供評測標籤品質的證據。若知識圖譜建構或 GraphRAG 的圖來自自動抽取，這篇提醒應分開記錄抽取錯誤和標註漏失；不能把 benchmark 的關係抽取 F1 等同於圖檢索或生成品質。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式來源：[ACL Anthology 正式記錄與 PDF](https://aclanthology.org/2022.emnlp-main.580/)；[arXiv:2205.12696](https://arxiv.org/abs/2205.12696)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(EMNLP 2022-12) Revisiting DocRED - Addressing the False Negative Problem in Relation Extraction.pdf|開啟本地 PDF 檔案]]（arXiv v3）。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2019-07) DocRED - A Large-Scale Document-Level Relation Extraction Dataset|DocRED]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2025-12) KGGen - Extracting Knowledge Graphs from Plain Text with Language Models|KGGen]]。
