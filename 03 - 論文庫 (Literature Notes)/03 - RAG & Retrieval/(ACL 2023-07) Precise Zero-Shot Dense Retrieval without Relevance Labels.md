---
paper_id: "Gao2023_HyDE"
title: "Precise Zero-Shot Dense Retrieval without Relevance Labels"
authors:
  - "Luyu Gao"
  - "Xueguang Ma"
  - "Jimmy Lin"
  - "Jamie Callan"
year: 2022
publication_year: 2023
venue: "ACL 2023"
doi: "10.18653/v1/2023.acl-long.99"
arxiv: "2212.10496"
url: "https://arxiv.org/abs/2212.10496"
pdf_file: "Papers/03 - RAG & Retrieval/(ACL 2023-07) Precise Zero-Shot Dense Retrieval without Relevance Labels.pdf"
tags:
  - "paper"
  - "query-expansion---hypothetical-generation"
verification_status: "verified"
last_verified: "2026-09-24"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains:
  - "D04"
paradigm_tags:
  - "retrieval"
adjacent_interfaces: []

---

# Precise Zero-Shot Dense Retrieval without Relevance Labels

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Gao2023_HyDE`
> - **作者**：Luyu Gao, Xueguang Ma, Jimmy Lin, Jamie Callan
> - **預印本初次發布年份 (Preprint)**：2022
> - **正式發表年份 / 會議或期刊 (Venue)**：2023 (ACL 2023)
> - **DOI**：10.18653/v1/2023.acl-long.99
> - **arXiv**：[2212.10496](https://arxiv.org/abs/2212.10496)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/03 - RAG & Retrieval/(ACL 2023-07) Precise Zero-Shot Dense Retrieval without Relevance Labels.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**HyDE 先由 instruction-following LLM 生成 hypothetical document，再以無監督 dense encoder 將其映射到 corpus embedding space；在論文測試中可改善 zero-shot dense retrieval，但不代表 query–document mismatch 已被完全解決。**

---

## 研究背景與問題定義 (Problem Statement)
使用者的查詢（Query）通常只有一句短話，而目標文檔（Passage）往往是數百字長段落，二者在向量空間中存在嚴重的幾何分佈不對稱（Asymmetry）。

---

## 核心方法與技術架構 (Methodology & Architecture)
透過 Instruction-tuned LLM 根據 Query 撰寫一篇假設性的回答文檔（Hypothetical Document）。即使假設文檔內包含事實錯誤，其文本模式、專業詞彙分佈與語法結構高度接近真實答案文檔。接著用無監督編碼器提取該假想文檔的向量去資料庫召回真實文檔。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Query Expansion / Hypothetical Generation 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **論文結論**：在無 relevance labels 的 zero-shot 設定下，HyDE 相較 Contriever 有顯著改善，並在多種 web search、QA、fact verification 與非英語檢索任務中呈現具競爭力的表現；不同 dataset / baseline 的結果應依原表逐項比較。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：零樣本（Zero-shot）檢索能力極強、無需訓練任何檢索模型；缺點：增加了一次 LLM 生成延遲與 API 費用，若模型產生嚴重的偏見反向誤導檢索目標。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
HyDE 是 query transformation / hypothetical-document retrieval 的代表性方法之一，適合作為 D05 中 query transformation 的 baseline / prior work。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Canonical RAG Domains/Domain 05 - Query Understanding & Retrieval|D05 Query Understanding & Retrieval]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
