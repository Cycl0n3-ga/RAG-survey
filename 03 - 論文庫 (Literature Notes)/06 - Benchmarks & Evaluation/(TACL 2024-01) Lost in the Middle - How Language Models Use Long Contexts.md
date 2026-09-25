---
paper_id: "Liu2024_LostInTheMiddle"
title: "Lost in the Middle: How Language Models Use Long Contexts"
authors:
  - "Nelson F. Liu"
  - "Kevin Lin"
  - "John Hewitt"
  - "Ashwin Paranjape"
  - "Michele Bevilacqua"
  - "Fabio Petroni"
  - "Percy Liang"
year: 2023
publication_year: 2024
venue: "TACL 2024"
doi: "10.1162/tacl_a_00638"
arxiv: "2307.03172"
url: "https://arxiv.org/abs/2307.03172"
pdf_file: "Papers/06 - Benchmarks & Evaluation/(TACL 2024-01) Lost in the Middle - How Language Models Use Long Contexts.pdf"
tags:
  - "paper"
  - "long-context-evaluation-&-analysis"
verification_status: "verified"
last_verified: "2026-09-24"
artifact_type: "benchmark_paper"
taxonomy_version: "v2"
taxonomy_home: "D07"
primary_domain: "D07"
secondary_domains:
  - "D13"
paradigm_tags:
  - "context_utilization"
adjacent_interfaces:
  - "A01"

---

# Lost in the Middle: How Language Models Use Long Contexts

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Liu2024_LostInTheMiddle`
> - **作者**：Nelson F. Liu, Kevin Lin, John Hewitt, Ashwin Paranjape, Michele Bevilacqua, Fabio Petroni, Percy Liang
> - **預印本初次發布年份 (Preprint)**：2023
> - **正式發表年份 / 會議或期刊 (Venue)**：2024 (TACL 2024)
> - **DOI**：10.1162/tacl_a_00638
> - **arXiv**：[2307.03172](https://arxiv.org/abs/2307.03172)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/06 - Benchmarks & Evaluation/(TACL 2024-01) Lost in the Middle - How Language Models Use Long Contexts.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**揭示所有主流長文本 LLM 普遍存在的 U 型效應：模型在利用頭尾資訊時表現優異，但對位於長 Context 中間的關鍵資訊極易視而不見。**

---

## 研究背景與問題定義 (Problem Statement)
學界與業界盲目追求擴展 Context Window，卻未經嚴格檢驗模型是否能在百萬序列的『任何位置』都同等具備穩健的檢索與推理能力。

---

## 核心方法與技術架構 (Methodology & Architecture)
設計多文檔問答（Multi-document QA）與鍵值檢索實驗，精確控制包含答案的目標文檔在整個 Context Window 中的相對位置（0% 到 100%）。橫向評估了當時最強的各類開源與閉源模型（GPT-3.5、Claude、MPT-30B 等）。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Long Context Evaluation & Analysis 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Figure 1 & Figure 2 (Page 3-4): 實證展示主流 LLM 在處理長上下文時呈現顯著 U 型曲線：答案位於輸入頭部時準確率 >70%，位於中間時劇跌至 <30%。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：以嚴謹的實證數據打破了『長上下文窗口 = 完美長文本理解』的迷思；缺點：該現象在 2024 年後的頂級模型（如 Gemini 1.5 Pro）中藉由訓練改進有所緩解，但在複雜推理場景下依然潛伏存在。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
震撼整個 NLP 界，催生了後續 Needle In A Haystack 測試標準以及長文本 Prompt 重排技術（如把關鍵證據置於開頭或結尾）。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|A01 Long Context & Sequence Architecture]]
  - [[02 - 研究領域專題 (Research Domains)/Domain 13 - RAG Evaluation & Failure Attribution|D13 RAG Evaluation & Failure Attribution]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/RAG System Maps|RAG System Maps]]
