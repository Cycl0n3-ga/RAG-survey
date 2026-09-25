---
paper_id: "Hsieh2024_RULER"
title: "RULER: What’s the Real Context Size of Your Long-Context Language Models?"
authors:
  - "Cheng-Ping Hsieh"
  - "Simeng Sun"
  - "Samuel Kriman"
  - "Shantanu Acharya"
  - "Dima Rekesh"
  - "Fei Jia"
  - "Boris Ginsburg"
year: 2024
publication_year: 2024
venue: "NVIDIA / arXiv"
doi: null
arxiv: "2404.06654"
url: "https://arxiv.org/abs/2404.06654"
pdf_file: "Papers/06 - Benchmarks & Evaluation/(arXiv 2024-04) RULER - What is the Real Context Size of Your Long-Context Language Models.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]"
tags:
  - "paper"
  - "behavioral-context-size-evaluation"
verification_status: "verified"
last_verified: "2026-09-24"
taxonomy_version: "v2"
taxonomy_home: "A01"
primary_domain: null
secondary_domains:
  - "D13"
paradigm_tags:
  - "long_context_evaluation"
adjacent_interfaces:
  - "A01"

---

# RULER: What’s the Real Context Size of Your Long-Context Language Models?

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Hsieh2024_RULER`
> - **作者**：Cheng-Ping Hsieh, Simeng Sun, Samuel Kriman, Shantanu Acharya, Dima Rekesh, Fei Jia, Boris Ginsburg
> - **預印本初次發布年份 (Preprint)**：2024
> - **正式發表年份 / 會議或期刊 (Venue)**：2024 (NVIDIA / arXiv)
> - **DOI**：無
> - **arXiv**：[2404.06654](https://arxiv.org/abs/2404.06654)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/06 - Benchmarks & Evaluation/(arXiv 2024-04) RULER - What is the Real Context Size of Your Long-Context Language Models.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**NVIDIA 提出 RULER，揭示 Needle In A Haystack 過於簡單的致命盲點，藉由多針檢索、變量追蹤與多跳聚合測量 LLM 的『真實有效上下文長度』。**

---

## 研究背景與問題定義 (Problem Statement)
標準的單針大海撈針（Single NIAH）測試太容易被模型過擬合（只要注意力矩陣捕捉到單一高權重即可），許多宣稱 128k 滿分的大模型在真實複雜長任務中迅速失效。

---

## 核心方法與技術架構 (Methodology & Architecture)
擴展 NIAH 複雜度維度：1. Multi-needle Retrieval（在長文中尋找多根針並綜合彙報）；2. Variable Tracking（跨超長距離追蹤變數的連續重賦值鏈條）；3. Common Words Extraction（統計分散在全文中的高頻實體）；4. Aggregation（長距離關聯歸納）。定義『模型準確率維持在 85% 以上的最大長度』為模型真實 Context 尺寸。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Behavioral Context Size Evaluation 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Table 1 & Figure 2 (Page 5-6): 評估 10 個開源/閉源長文本模型；發現幾乎所有宣稱支援 128k 的模型在 4 根針以上檢索與變數追蹤任務中，真實有效長度崩潰至不到 32k。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：極具說服力地揭露了名義 Context 與實際有效 Context 的巨大差距（許多 128k 模型實際真實長度不到 32k）；缺點：任務具備較強的合成特徵，仍需與現實場景問答配合驗證。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
成為業界評估長文本模型是否真正具備穩健注意力與長程推理能力的最嚴苛權威標準。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
