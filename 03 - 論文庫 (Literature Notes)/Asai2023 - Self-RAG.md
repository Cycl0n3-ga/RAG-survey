---
paper_id: "Asai2024_SelfRAG"
title: "Self-RAG: Learning to Retrieve, Generate, and Critique through Self-Reflection"
authors:
  - "Akari Asai"
  - "Zeqiu Wu"
  - "Yizhong Wang"
  - "Avirup Sil"
  - "Hannaneh Hajishirzi"
year: 2023
publication_year: 2024
venue: "ICLR 2024"
doi: null
arxiv: "2310.11511"
url: "https://arxiv.org/abs/2310.11511"
pdf_file: "Papers/03 - RAG & Retrieval/(ICLR 2024-05) Self-RAG - Learning to Retrieve, Generate, and Critique through Self-Reflection.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)]]"
  - "[[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]"
tags:
  - "paper"
  - "adaptive-rag---self-reflection"
verification_status: "verified"
last_verified: "2026-09-24"
---

# Self-RAG: Learning to Retrieve, Generate, and Critique through Self-Reflection

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Asai2024_SelfRAG`
> - **作者**：Akari Asai, Zeqiu Wu, Yizhong Wang, Avirup Sil, Hannaneh Hajishirzi
> - **預印本初次發布年份 (Preprint)**：2023
> - **正式發表年份 / 會議或期刊 (Venue)**：2024 (ICLR 2024)
> - **DOI**：無
> - **arXiv**：[2310.11511](https://arxiv.org/abs/2310.11511)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/03 - RAG & Retrieval/(ICLR 2024-05) Self-RAG - Learning to Retrieve, Generate, and Critique through Self-Reflection.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**透過特殊的 Reflection Tokens 訓練 LLM 自主決定何時需要檢索、評估檢索相關性，並對自身生成的忠實度進行自我批判。**

---

## 研究背景與問題定義 (Problem Statement)
傳統 RAG 無論問題難易與自身知識庫存，盲目觸發檢索；且對檢索出的低品質文檔缺乏批判能力，容易被噪音誤導。

---

## 核心方法與技術架構 (Methodology & Architecture)
引入四種反思標記（Reflection Tokens）：1. `[Retrieve]`（是否需要檢索）；2. `[IsREL]`（文檔是否與主題相關）；3. `[IsSUP]`（生成的主張是否受到文檔支持）；4. `[IsUSE]`（生成內容是否實用）。訓練模型輸出這些標記，並在推論時利用 Beam Search 選擇最高質量路徑。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Adaptive RAG / Self-Reflection 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Table 1 (Page 6): 在 Pub/Bio/OpenQA 基準上，Self-RAG 7B 模型擊敗了未檢索的 70B 模型與常規 RAG 系統；生成引文忠實度 (Faithfulness) 提升超過 30%。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：動態自適應檢索並以 reflection tokens 評估 relevance / support / utility；缺點：需要專門的資料建立與 supervised fine-tuning，且推論時 reflection-token scoring 增加解碼複雜度。原論文的方法流程不以 reinforcement learning 作為必要訓練步驟。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
開創了『自省式檢索（Self-Reflective RAG）』範式，是現代高品質長文知識問答與反思 Agent 的核心理論來源。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)]]
  - [[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
