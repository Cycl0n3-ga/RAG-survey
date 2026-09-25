---
paper_id: "An2024_LEval"
title: "L-Eval: Instituting Standardized Evaluation for Long Context Language Models"
authors:
  - "Chenxin An"
  - "Shansan Gong"
  - "Ming Zhong"
  - "Xingjian Zhao"
  - "Mukai Li"
  - "Jun Zhang"
  - "Lingpeng Kong"
  - "Xipeng Qiu"
year: 2023
publication_year: 2024
venue: "ACL 2024"
doi: null
arxiv: "2307.11088"
url: "https://arxiv.org/abs/2307.11088"
pdf_file: "Papers/06 - Benchmarks & Evaluation/(ACL 2024-08) L-Eval - Instituting Standardized Evaluation for Long Context Language Models.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]"
tags:
  - "paper"
  - "long-context-evaluation-standard"
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

# L-Eval: Instituting Standardized Evaluation for Long Context Language Models

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`An2024_LEval`
> - **作者**：Chenxin An, Shansan Gong, Ming Zhong, Xingjian Zhao, Mukai Li, Jun Zhang, Lingpeng Kong, Xipeng Qiu
> - **預印本初次發布年份 (Preprint)**：2023
> - **正式發表年份 / 會議或期刊 (Venue)**：2024 (ACL 2024)
> - **DOI**：無
> - **arXiv**：[2307.11088](https://arxiv.org/abs/2307.11088)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/06 - Benchmarks & Evaluation/(ACL 2024-08) L-Eval - Instituting Standardized Evaluation for Long Context Language Models.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**復旦大學提出包含封閉式問答與開放式問答的標準化長文本評測基準，解決長文本傳統 n-gram 指標失真的難題。**

---

## 研究背景與問題定義 (Problem Statement)
長文本生成答案長度長、語義豐富，傳統 ROUGE/BLEU 無法準確判定模型是否真正推理出正確結論。

---

## 核心方法與技術架構 (Methodology & Architecture)
精選 18 個子任務，涵蓋 3k 到 200k tokens 的長度分佈。設計了雙重評估機制：1. 封閉式選擇題與提取題（可直接精確匹配驗證）；2. 經過人工細緻標註的長文本開放問答，結合基於規則的評分器與 LLM-as-a-Judge 混合評分方案。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Long Context Evaluation Standard 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Table 2 & Figure 3 (Page 6-7): 涵蓋 18 個子任務，測試長度達 200k；揭示長文本生成長答案與短答案在評測指標上的巨大方差，標準化 LLM-as-a-Judge 協議。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：有效區分了『檢索能力』與『推理總結能力』，長度跨度大；缺點：LLM 裁判自身對超長 context 的偏誤仍需持續校準。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
促進了長文本評測從粗糙的詞頻比對走向語意等級標準化驗證的成熟階段。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
