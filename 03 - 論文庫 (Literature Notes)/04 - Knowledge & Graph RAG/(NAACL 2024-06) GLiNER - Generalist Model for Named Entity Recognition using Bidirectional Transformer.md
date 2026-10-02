---
paper_id: "Zaratiana2023_GLiNER"
title: "GLiNER: Generalist Model for Named Entity Recognition using Bidirectional Transformer"
authors:
  - "Urchade Zaratiana"
  - "Nadi Tomeh"
  - "Pierre Holat"
  - "Thierry Charnois"
year: 2023
publication_year: 2024
venue: "NAACL 2024 (Long Papers)"
doi: "10.18653/v1/2024.naacl-long.300"
arxiv: "2311.08526"
url: "https://aclanthology.org/2024.naacl-long.300/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(NAACL 2024-06) GLiNER - Generalist Model for Named Entity Recognition using Bidirectional Transformer.pdf"
tags:
  - paper
  - named-entity-recognition
  - information-extraction
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D03"
primary_domain: "D03"
secondary_domains: []
paradigm_tags: []
adjacent_interfaces: []
research_questions:
  - "open_type_entity_recognition"
  - "entity_extraction"
benchmark_ids: []
dataset_ids:
  - "Pile-NER"
metrics:
  - "micro-F1"
---

# GLiNER: Generalist Model for Named Entity Recognition using Bidirectional Transformer

> **版本與閱讀範圍：** arXiv:2311.08526 v1（2023-11-14，11 頁）全文已讀；NAACL Anthology 正式書目已核，尚未逐段比對正式 proceedings PDF 與 arXiv v1。正式出版作者資料為 Urchade Zaratiana、Nadi Tomeh、Pierre Holat、Thierry Charnois；頁 5364–5376，DOI `10.18653/v1/2024.naacl-long.300`。

## 一話摘要 (TL;DR)
GLiNER 以雙向 encoder 和文字化 entity type 做平行 span 分類，提供不需逐類微調的開放類型 NER 模型，作為知識抽取流程中的實體辨識元件。

## 研究背景與問題定義 (Problem Statement)
作者要處理傳統 NER 受限於預先定義標籤集，以及大型生成式 LLM 做任意類型抽取時推論成本較高的問題。GLiNER 將輸入文字和使用者指定的 entity types 一同編碼，再對文字 spans 與類型表示做匹配；這是 entity span 抽取，不負責關係抽取、entity linking 或跨文件 consolidation。[§1–2, arXiv PDF pp. 1–3]

## 核心方法與技術架構 (Methodology & Architecture)
模型以 bidirectional transformer encoder 分別編碼 token 序列與 entity type 描述，並以 span representations 和 type embeddings 計算相容分數，透過 span-level classification 找出實體。訓練使用 Pile-NER：從 Pile 抽樣文字並由 ChatGPT 生成多樣 entity annotations；作者另以不同 DeBERTa-v3 規模訓練 GLiNER-S/M/L。推論可一次處理多個類型，類型集合仍由使用者提供。[§2–3, Figure 1, arXiv PDF pp. 2–4]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, arXiv PDF p. 4：** out-of-domain NER benchmark 上 GLiNER-L（0.3B）平均 F1 為 60.9；GLiNER-M（90M）為 55.4。該表同時比較不同來源的 ChatGPT、instruction-tuned IE 與 NER systems，資料／prompt／模型條件不完全一致，不能視為同條件因果比較。
- **Table 2, arXiv PDF p. 5：** 20 個 NER dataset 的 zero-shot macro average F1，GLiNER-S/M/L 分別為 36.5/45.7/47.8。結果支持該模型在該組 benchmark 上的 zero-shot 能力，不代表對未見領域、標註政策或語言都同等可靠。
- 訓練資料部分說明 Pile-NER 由 50,000 段文本及 ChatGPT 抽取標註構成。[§3.1, arXiv PDF p. 4] 正式版硬體／延遲與部署成本未在本次版本核對中建立可比證據，故不作效率優越的量化宣稱。

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- 開放類型介面將 entity type 從固定分類頭改為文字條件，且 span-based 雙向編碼能平行處理候選實體；小型模型可作圖譜抽取 pipeline 的可控候選元件。
- 依賴上游合成標註資料的品質與訓練分布；NER F1 只測 span/type 產出，不涵蓋 entity linking、關係正確性、圖譜一致性或 RAG answer quality。
- 論文結論指出仍需改善模型設計及低資源語言適應。[§7, arXiv PDF p. 8] zero-shot 類型描述和 benchmark label/schema 的相容性也會影響結果。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
建議 D03 primary：核心輸出是從文字抽取 typed entity spans；下游若將 spans 對齊 canonical entities 或整併來源記錄，仍需另外評估。可作圖譜建構前段的 entity-recognition baseline，與 PURE、GoLLIE 等抽取方法比較；它不是 graph construction、relation extraction 或 GraphRAG 系統。此 domain mapping 為 repo 分類判斷。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式書目：[ACL Anthology](https://aclanthology.org/2024.naacl-long.300/)；預印本：[arXiv:2311.08526](https://arxiv.org/abs/2311.08526)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(NAACL 2024-06) GLiNER - Generalist Model for Named Entity Recognition using Bidirectional Transformer.pdf|開啟本地 PDF 檔案]]（arXiv v1）。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NAACL 2021-06) A Frustratingly Easy Approach for Entity and Relation Extraction|PURE]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) GoLLIE - Annotation Guidelines Improve Zero-Shot Information Extraction|GoLLIE]]。
