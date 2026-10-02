---
paper_id: "Blecher2023_Nougat"
title: "Nougat: Neural Optical Understanding for Academic Documents"
authors:
  - "Lukas Blecher"
  - "Guillem Cucurull Preixens"
  - "Thomas Scialom"
  - "Robert Stojnic"
year: 2023
publication_year: 2024
venue: "ICLR 2024"
doi: null
arxiv: "2308.13418"
url: "https://proceedings.iclr.cc/paper_files/paper/2024/hash/a39a9aceda771cded859ae7560530e09-Abstract-Conference.html"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(ICLR 2024-05) Nougat - Neural Optical Understanding for Academic Documents.pdf"
tags:
  - paper
  - document-parsing
  - OCR-free
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D01"
primary_domain: "D01"
secondary_domains: []
paradigm_tags: []
adjacent_interfaces: []
research_questions:
  - "scientific_document_parsing"
  - "pdf_to_markup"
benchmark_ids: []
dataset_ids:
  - "Nougat arXiv test set"
metrics:
  - "edit distance"
  - "BLEU"
  - "METEOR"
  - "precision"
  - "recall"
  - "F1"
source_version: arXiv:2308.13418v1
verified_version: arXiv:2308.13418v1
pdf_pages: 17
pdf_sha256: 679be336ce8010d3dc86b9530f0a30d4d5ea2a13153c6f274601b40f4382745b
---

# Nougat: Neural Optical Understanding for Academic Documents

> **版本與閱讀範圍：** 已讀 arXiv:2308.13418 v1 全文（17 頁）；ICLR 2024 正式 metadata／作者名單已核，尚未逐項比對正式 proceedings PDF。arXiv 版本作者列為 “Guillem Cucurull”，正式 ICLR 頁列為 “Guillem Cucurull Preixens”；YAML 依正式出版記錄保存姓名。

## 一話摘要 (TL;DR)
Nougat 是 OCR-free 的 encoder–decoder 模型，從學術文件頁面影像直接產生含結構標記的 markup，目標在保留公式、表格與文章結構，而不只輸出平面文字。

## 研究背景與問題定義 (Problem Statement)
PDF 的 embedded text 可能遺失數學表達式、閱讀順序或版面層級；既有 OCR／parser 對高密度學術文件及公式表示有局限。Nougat 將每頁 raster image 作輸入、markup 作輸出，並以自動化方式建立 PDF image–markup 訓練資料。[§1, §3–4, arXiv PDF pp. 1–5]

## 核心方法與技術架構 (Methodology & Architecture)
論文以 Swin Transformer encoder 與 BART decoder 組成頁面到序列模型；頁面以 96 DPI rasterize，resize/pad 到 896×672，base 約 350M 參數、small 約 250M，輸出序列上限分別為 4,096 與 3,584 tokens。資料建構將 LaTeX／HTML / PMC markup 與 PDF 頁面對齊，並透過 page splitting 產生訓練樣本。[§3–4, arXiv PDF pp. 3–6]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, arXiv PDF p. 7：** arXiv test set 的 All text F1：Nougat base 93.1、small 92.9；表中 PDF embedded text 對照為 79.2。Math F1：base 76.5；Tables F1：base 78.0。該指標是與論文 markup reference 的文字／結構轉寫相似度，不是 downstream retrieval recall、語義正確性或 RAG answer quality。
- **§5.5, arXiv PDF p. 9：** A10G 24GB 上同時處理 6 頁，平均每批 19.5 秒（每頁約 1,400 tokens 的設定）；作者並報 GROBID 為 10.6 PDF/s，單位與硬體／處理條件未形成完整同條件比較，不能據此宣稱通用速度勝負。
- **§5.5, arXiv PDF p. 9：** 每頁獨立生成便於平行處理，但可能造成跨頁 bibliography 或 section numbering 不一致；作者亦指出 non-Latin scripts 會出現重複生成，英語學術文件最符合訓練分布。

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- 直接讀頁面影像，適用於沒有可靠 embedded text 的掃描件，也能輸出 LaTeX/表格等 markup；頁級推論可平行化。
- 作者觀察到 repetition failure；non-Latin script 支援不足，且以單頁為單位會犧牲跨頁一致性。[§5.4–5.5, arXiv PDF pp. 8–9]
- Table 1 的字面 markup metrics 可能懲罰語義等價但字面不同的公式表達；其 arXiv test set 結果不足以證明對任意 PDF、表格抽取或下游 GraphRAG 的收益。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
D01 primary：Nougat 解決原始頁面影像到結構化 source markup 的解析問題。對 graph-heavy RAG 可提供圖表、公式和正文抽取的文件前處理基線；parser quality 應與後續 entity/relation extraction（D03）、representation（D04）、retrieval（D05）分開評估，並控制來源文件與 OCR/parsing 錯誤傳播。該 domain mapping 為 repo taxonomy 判斷。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式書目：[ICLR 2024 proceedings](https://proceedings.iclr.cc/paper_files/paper/2024/hash/a39a9aceda771cded859ae7560530e09-Abstract-Conference.html)；預印本：[arXiv:2308.13418](https://arxiv.org/abs/2308.13418)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(ICLR 2024-05) Nougat - Neural Optical Understanding for Academic Documents.pdf|開啟本地 PDF 檔案]]（arXiv v1）。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(EMNLP 2025-11) Intelligent Document Parsing - Towards End-to-end Document Parsing via Decoupled Content Parsing and Layout Grounding|Intelligent Document Parsing]]、[[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(EMNLP 2024-11) PDF-to-Tree - Parsing PDF Text Blocks into a Tree|PDF-to-Tree]]。
