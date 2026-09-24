---
title: "Precise Zero-Shot Dense Retrieval without Relevance Labels"
authors: ["Luyu Gao", "Xueguang Ma", "Jimmy Lin", "Jamie Callan"]
year: 2022
venue: "ACL 2023"
arxiv: "2212.10496"
url: "https://arxiv.org/abs/2212.10496"
pdf_file: "Papers/03 - RAG & Retrieval/(ACL 2023-07) Precise Zero-Shot Dense Retrieval without Relevance Labels.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)]]"
tags:
  - paper
  - query-expansion---hypothetical-generation
---

# Precise Zero-Shot Dense Retrieval without Relevance Labels

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Luyu Gao, Xueguang Ma, Jimmy Lin, Jamie Callan
> - **年份 / 會議**：2022 (ACL 2023)
> - **arXiv**：[2212.10496](https://arxiv.org/abs/2212.10496)
> - **論文分類**：`Query Expansion / Hypothetical Generation`
> - **本地 PDF 連結**：[[Papers/03 - RAG & Retrieval/(ACL 2023-07) Precise Zero-Shot Dense Retrieval without Relevance Labels.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**先由 LLM 生成一份『虛構但語意完整的假想文檔』再進行向量檢索，徹底解決 Query 與 Document 長度與語意不對稱的痛點。**

---

## 核心痛點與研究背景 (Problem Statement)
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

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：零樣本（Zero-shot）檢索能力極強、無需訓練任何檢索模型；缺點：增加了一次 LLM 生成延遲與 API 費用，若模型產生嚴重的偏見反向誤導檢索目標。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
啟發了大量 Query Transformation 與 Query Expansion 技術，是現代高難度複雜檢索的標準手段之一。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
